---
author: Samuel
categories:
  - Java
date: 2020-07-29 15:25:05+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
id: 1571
permalink: /2020/07/spring-cloud-steam/
tags:
  - MDA
title: Spring Cloud Steam
url: /2020/07/spring-cloud-steam/
---

Après une journée à rechercher comment fonctionne Spring Cloud Stream, je me rends compte que la dernière version a changé pas mal de choses.

En effet depuis la version 3, la gestion des streams s'est orienté vers du code fonctionnel et on trouve encore beaucoup d'exemples utilisant "l'ancienne" méthode basée sur les annotations. Même dans la documentation officielle, je ne trouve pas ça super clair.

Du coup je vous propose d'étudier un petit exemple de mise en place simple avec cette nouvelle façon de faire.

## La création d'évènements

Souvent dans les tutos les évènements sont créés par des Suppliers comme ça :

{% highlight java %}
@Bean
public Supplier<Item> sendItem() {
  return () -> new Item("tomato", 10);
}
{% endhighlight %}


Mais dans un projet pour une API, c'est souvent créé par un call HTTP.
Dans ce cas il faut utiliser un StreamBridge

{% highlight java %}
streamBridge.send("sendItem-out-0", new Item("tomato", 10));
{% endhighlight %}

Avec la nouvelle version fonctionnelle de spring cloud stream, la
gestion des définitions des files de message n'est plus faite par
annotation mais par la configuration basée sur des règles de nommage.

Donc mon code signifie que je vais envoyer l'object Item comme premier
élément de sortie de la fonction sendItem.
Il faudra aussi ajouter dans le fichier application.properties la ligne

{% highlight properties %}
spring.cloud.stream.bindings.sendItem-out-0.destination=listItems
{% endhighlight %}

On était habitué à faire toute la configuration via annotation, ce n'est
plus le cas.

## Consommer un évènement

Toujours avec un code fonctionnel, un exemple de consommateur :

{% highlight java %}
@Bean
public Consumer<Item> printItem() {
    return data -> LOG.info("Item " + data.name + "(" + data.price + ")");
}
{% endhighlight %}

Dans cet exemple on consomme un object Item pour l'afficher dans les
logs. Il ne fonctionnera que si dans la configuration on ajoute :

{% highlight properties %}
spring.cloud.stream.function.definition=printItem
spring.cloud.stream.bindings.printItem-in-0.destination=listItems
{% endhighlight %}

Il faut donc définir la fonction printItem comme fonction gérant un
stream et ensuite dire qu'elle consomme les objets de la file
"listItems"

## Transformer un événement

En plus des consommateurs et des producteurs, on peut faire des
fonctions de composition.

{% highlight java %}
@Bean
public Function<Item, Integer> getPrice() {
    return item -> item.price;
}
{% endhighlight %}

Dans cet exemple, la fonction transforme un object Item et entier. La
encore il faut le configurer

{% highlight properties %}
spring.cloud.stream.function.definition=getPrice;printItem
spring.cloud.stream.bindings.getPrice-in-0.destination=buyItems
spring.cloud.stream.bindings.getPrice-out-0.destination=addPrices
{% endhighlight %}

Donc on ajoute le nom de la méthode getPrice dans la liste des
fonctions gérant des stream et on ajoute le nom de la file dans 
laquelle on consomme un évènement et celle où on envoie le résultat

## Test unitaire

Pour tester que la configuration et le routage fonctionnent correctement
on teste qu'en fonction d'une donnée en entrée on récupère bien le bon
résultat en sortie pour une fonction de composition

{% highlight java %}
@Test
void testMessages() {
  input.send(new GenericMessage<>(new Item("Tomato", 20)));
  BlockingQueue<Message<?>> messages = collector.forChannel(output);
  assertThat(messages,receivesPayloadThat(CoreMatchers.is("20")));
}
{% endhighlight %}

En sachant qu'il est aussi assez simple de tester unitairement la
fonction en direct :

{% highlight java %}
@Test
void testFunction() {
  assertEquals(20,service.getPrice().apply(new Item("Tomato",20)).intValue());
}
{% endhighlight %}

Et voilà, c'est juste un petit exemple mais j'ai personnellement eu du mal à retrouver tous ces points dans un autre tuto.
L'ensemble du code est sur [ce repo github](https://github.com/sliard/spring-cloud-stream-basic).

Dans mon exemple, il y a un docker-compose.yml pour lancer une
instance de RabbiMQ avec un compte sécurisé avec un mot de passe et la
configuration en découlant dans le fichier application.properties. Et
oui je n'utilise pas de YAML pour la configuration de spring, je suis
beaucoup trop vieux pour ça !

## Références

[Doc spring](https://cloud.spring.io/spring-cloud-static/spring-cloud-stream/current/reference/html/spring-cloud-stream.html#_functional_composition)

[Bon exemple en Kotlin](https://piotrminkowski.com/2020/06/05/introduction-to-event-driven-microservices-with-spring-cloud-stream/)

[Exemples officiels](https://github.com/spring-cloud/spring-cloud-stream-samples)