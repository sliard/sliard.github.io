---
theme: java
author: Samuel
categories:
  - Java
date: 2011-07-21 23:33:18+00:00
guid: http://www.net-liard.com/blog/?p=940
id: 940
permalink: /2011/07/active-mq-dans-le-cloud/
tags:
  - ActiveMQ
  - cloud
  - CloudBees
  - CloudFoundry
  - JMS
title: Active MQ dans le cloud
url: /2011/07/21/active-mq-dans-le-cloud/
---

En ce moment je regarde pour développer une plateforme de push notification iPhone. Le but est d&#8217;offrir une surcouche applicative plus simple à utiliser que les sockets d&#8217;Apple. Un peu comme le service offert par [urbanairship](http://urbanairship.com/).

Ce qu&#8217;il faut bien comprendre avec le push d&#8217;Apple, c&#8217;est que pour envoyer une notification à 400 000 iPhone il faut ouvrir une socket chez eux et envoyer 400 000 trames avec un token différent par iPhone. En sachant qu&#8217;Apple peut banir une IP serveur si on envoie plus de 200 messages par seconde, il est important de répartir la charge sur plusieurs serveurs (ou au moins plusieurs IP publiques).

Donc j&#8217;ai pensé à mettre en place une architecture [MOM](http://fr.wikipedia.org/wiki/Message-Oriented_Middleware) :

![photo](/images/uploads/2011/07/activemq11.jpg)

Avec cette architecture on peut ajouter des Brokers JMS en fonction de la charge à absorber. L&#8217;idée est de profiter au maximum des services de cloud computing et offrant la possibilité d&#8217;ajouter/retirer au runtime des VM avec un Broker. C&#8217;est donc pour héberger cette solution que j&#8217;ai creusé les différentes offres de cloud computing (cf ce post). Mais c&#8217;est au moment du déploiement que j&#8217;ai rencontré des difficultés (bah oui comme d&#8217;habitude en fait&#8230;).

Le code qui va envoyer les messages JMS doit connaitre la liste de Broker. Or comme nous sommes dans le cloud, cette liste peut être modifiée au bon vouloir de l&#8217;administrateur. Pire je ne connais même pas forcément à l&#8217;avance les IP des Broker que je vais ajouter.

Donc imaginez si dans la configuration client je définis une URI du type :

<pre>failover:(tcp://primary:61616,tcp://secondary:61616)</pre>

Il va falloir modifier le code du client à chaque ajout d&#8217;un nouveau Broker. C&#8217;est donc impossible. Heureusement pour ce genre de cas Active MQ propose un système de multicast. Ce qui donne au niveau URI du client :

<pre>discovery:(multicast://default)</pre>

Là c&#8217;est magique sur mon serveur en local ça marche très bien. Et oui mais non  :(Sur les offres cloud le multicast (sur UDP) n&#8217;est pas souvent supporté. Sur Amazon EC2 (donc sur CloudBees) et CloudFoundry (VMWare) impossible de faire fonctionner le multicast.

Donc comment faire ? Le client JMS a besoin de récupérer une liste de Broker. Il faut donc que chaque Broker vienne se faire connaitre au moment de leur lancement. Comme j&#8217;ai déjà un BDD autant l&#8217;utiliser pour référencer ces Brokers. J&#8217;ai donc développer un module de multicast via une BDD : [multicasdb](https://github.com/sliard/multicastdb).

Donc on arrive sur une architecture comme celle-ci :

![photo](/images/uploads/2011/07/activemq2.jpg)

Pour le faire je me suis beaucoup inspiré du code du multicast UDP. Ca fonctionne bien sur mes serveurs de test mais là encore je tombe sur des problèmes spécifiques aux serveurs cloud : l&#8217;adresse du serveur. Comme c&#8217;est le même war qui est déployé sur tous les serveurs la configuration du broker doit être générique. Pas de pb : j&#8217;utilise localhost comme nom de serveur :

<!-- p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 11.0px Monaco; color: #3834ff} p.p2 {margin: 0.0px 0.0px 0.0px 0.0px; font: 11.0px Monaco; color: #4d9192} span.s1 {color: #000000} span.s2 {color: #009193} span.s3 {color: #4d9192} span.s4 {color: #932192} span.Apple-tab-span {white-space:pre} -->

<pre name="code" class="xml:nogutter:nocontrols">&lt;broker persistent="false">
  &lt;networkConnectors>
    &lt;networkConnector uri="multicastdb://default?dataSource=myDataSource">
&lt;/networkConnector>
  &lt;transportConnectors>
     &lt;transportConnector uri="http://localhost:8080"   
discoveryUri="multicastdb://default?dataSource=myDataSource">
    &lt;/transportConnector>
  &lt;/transportConnectors>
&lt;/broker>
</pre>

Donc oui je peux utiliser cette configuration sur tous les serveurs, mais si je persiste &#8220;localhost:8080&#8221; en base le client ne pourra pas y accéder depuis un autre serveur. Donc il faut que mon code trouve l&#8217;IP du serveur pour le persister au runtime.

Aujourd&#8217;hui même si le code n&#8217;est pas finalisé, il fonctionne. Malheureusement j&#8217;ai toujours des problèmes pour l&#8217;héberger.

Chez **Cloudbees** la communication tcp entre VM est bloquée. Même si leur support affirme que ça peut fonctionner j&#8217;ai toujours des erreurs : java.net.ConnectException: Connection refused

Chez **CloudFoundry** j&#8217;ai même eu du mal à obtenir l&#8217;IP des VM. Le code qui fonctionne sur Cloudbees retourne 127.0.0.1 comme IP chez CloudFoundry. Pour trouver cette IP il faut utiliser un SDK fourni. Mais là encore :Connection refused :(

## Bilan

Au final je n&#8217;ai pas réussi à faire fonctionner mon code comme je le voulais. Par contre cette petite expérience m&#8217;a permis de faire mes premiers pas sur 2 offres de cloud intéressantes. Aujourd&#8217;hui je trouve CloudFoundry beaucoup plus agréable à utiliser que CloudBees. Son SDK est très simple et en 20 secondes je peux redéployer une version. Avec CloudBees j&#8217;ai beaucoup de mal avec le SDK. Déjà c&#8217;est basé sur un script Ant&#8230; Alors il y a aussi un plug-in maven mais je n&#8217;ai pas pu l&#8217;utiliser en mode &#8220;Delta&#8221; du coup il faut uploader totalement mon War à chaque modification : 10 minutes. Je trouve aussi le plug-in Eclipse de CloudFoundry mieux fait. Par contre CloudBees possède une vrai interface d&#8217;administration web et son offre DEV@Cloud est vraiment intéressante. Un bon point pour les 2 : la réactivité du support. Une réponse dans la journée, pour mon compte gratuit de test, c&#8217;est vraiment bien (n&#8217;est ce pas [Nicolas](http://twitter.com/#!/ndeloof) 😉 )

Pour revenir à mon problème initial, je vais continuer à creuser ce problème de communication inter VM et si je n&#8217;avance pas je vais revoir l&#8217;architecture. Peut-être persister les messages à envoyer: c&#8217;est moins performant mais ça peut aussi répondre à un besoin de suivi de diffusion.

La phase d&#8217;intégration d&#8217;un projet est toujours sous estimée J&#8217;ai vu des projets où cette phase était même plus importante en terme d&#8217;homme/jour que la phase de développement. Mais pour un hébergement dans le cloud il faut vraiment prendre cette problématique dès le début de la conception. C&#8217;est loin d&#8217;être un détail :)