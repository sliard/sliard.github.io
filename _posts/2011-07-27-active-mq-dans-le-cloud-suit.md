---
theme: java
author: Samuel
categories:
  - Java
date: 2011-07-27 17:33:09+00:00
guid: http://www.net-liard.com/blog/?p=991
id: 991
permalink: /2011/07/active-mq-dans-le-cloud-suit/
tags:
  - ActiveMQ
  - cloud
  - Cloud Foundry
  - CloudBees
  - JMS
title: Active MQ dans le cloud - suite
url: /2011/07/27/active-mq-dans-le-cloud-suit/
---

Comme vous avez pu le lire [dans le précédent article](http://www.net-liard.com/blog/2011/07/active-mq-dans-le-cloud/) je n&#8217;étais pas arrivé au bout de l&#8217;exercice pour déployer ActiveMQ sur des offres PAAS. Et bien c&#8217;est chose faite, ça marche ! :)

Mon erreur a été de me focaliser sur un problème réseau entre les VM (configuration, firewall&#8230;) En fait le problème était au niveau de l&#8217;ouverture des sockets. J&#8217;ai donc modifié le code du TCPConnector d&#8217;Active MQ pour l&#8217;adapter à mes contraintes.

Il faut juste changer le bind dans org.apache.activemq.transport.tcp.TcpTransportServer

<pre name="code" class="java:nogutter:nocontrols">public void bind() throws IOException {
  URI bind = getBindLocation();

  String host = bind.getHost();
  host = (host == null || host.length() == 0) ? "localhost" : host;
  InetAddress addr = InetAddress.getByName(host);</pre>

en

<pre name="code" class="java:nogutter:nocontrols">public void bind() throws IOException {
  URI bind = getBindLocation();

  InetAddress addr = InetAddress.getLocalHost();</pre>

C&#8217;est plus restrictif, mais suffisant pour mon cas.

J&#8217;ai repackagé cela dans un protocole tcpcloud et hop ça fonctionne sur cloudbees du premier coup. Maintenant ma charge est partagée sur les n instances (n=2 pour le moment comme j&#8217;utilise l&#8217;offre gratuite).

Pour CloudFoundry j&#8217;ai eu un peu plus de mal car même si je note dans le fichier de config &#8220;localhost&#8221;, il passe le nom de la machine au runtime. Ca doit être le même système qui remplace l&#8217;url et le login/pass de la base de données. Ce côté un peu magique me dérange. Je dois aussi dépendre de leur lib cloudfoundry-runtime pour trouver l&#8217;adresse IP de la VM. En plus leur beau plug-in eclipse ne fonctionne pas sur Eclipse Indigo :(

Je vais pouvoir partir en vacances sereinement ! 😉