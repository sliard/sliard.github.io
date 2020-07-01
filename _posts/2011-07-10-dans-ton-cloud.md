---
author: Samuel
categories:
  - Java
date: 2011-07-10 23:09:03+00:00
guid: http://www.net-liard.com/blog/?p=926
id: 926
permalink: /2011/07/dans-ton-cloud/
tags:
  - cloud
  - Cloud Foundry
  - CloudBees
title: Dans Ton Cloud
url: /2011/07/10/dans-ton-cloud/
---

Depuis 2 semaines je regarde différentes solutions de cloud computing.

Dans un premier temps j&#8217;ai regardé les offres &#8220;bas niveau&#8221; :

**[MiniCloud d&#8217;OVH](http://www.ovh.com/fr/cloud/)**

C&#8217;est une offre abordable mais qui est en test depuis plus d&#8217;un an. C&#8217;est une facturation &#8220;Pay as you go&#8221; mais il manque deux fonctionnalités importantes : le load balancing et le clonage d&#8217;instance. L&#8217;adresse IP des instances change à chaque arrêt/relance ce qui peut être génant.

**[Amazon EC2](http://aws.amazon.com/fr/ec2/)**

L&#8217;offre cloud la plus célèbre, j&#8217;ai arrêté l&#8217;inscription au moment d&#8217;entrer un numéro de carte bleue. Impossible de faire sans et comme le détail des tarifs est assez flou j&#8217;ai préféré ne pas le faire.

**So Privé**

Le site So privé est fermé pour ouvrir [OUTSCALE](http://www.outscale.com/).

**[Rackspacecloud](http://www.rackspace.com/cloud/)**

L&#8217;offre la plus intéressante pour le moment, load-Balancing clonage de VM, &#8220;Pay as you go&#8221;. Il manque juste des images un peu plus complètes avec par exemple un tomcat ou mysql.

**[ikoula](http://express.ikoula.com/vm)**

Grosse pub pour leur VM à 1 Euro mais c&#8217;est uniquement des VM Windows -> Fail

&nbsp;

Obtenir une VM avec un OS c&#8217;est bien, malheureusement je ne suis pas ingé système mais développeur Java donc si je pouvais utiliser des offres clouds faites pour déployer un war je gagnerais du temps. Et c&#8217;est exactement ce que propose Cloud Foundry et CloudBees. Oui Google App Engine le fait aussi mais dans mon cas j&#8217;ai besoin d&#8217;ouvrir une socket vers un serveur distant et donc GAE est out :)

**[Cloud Foundry](http://www.cloudfoundry.com/)**

C&#8217;est l&#8217;offre de VM Ware et Spring Source en version Beta pour le moment. En quelques minutes j&#8217;ai mis en ligne l&#8217;exemple Hello Word. Le plus long c&#8217;est de recevoir l&#8217;email d&#8217;inscription. Le SDK s&#8217;installe en 2 minutes grace à ruby (gem est pré-installé sur Mac).

Après le Hello Word j&#8217;ai déployé un war plus complexe très rapidement. Le plug-in eclipse est aussi très bien fait, on peut voir les ressources consommées par les applications, ajouter des instances (2 max pour le moment), les arrêter. Par contre j&#8217;ai eu un problème au niveau de l&#8217;affichage des logs. Sur Eclipse ce n&#8217;était pas à jour contrairement à ce qu&#8217;affichait la commande &#8220;vmc logs&#8221;.

**[CloudBees](http://www.cloudbees.com/)**

Là encore CloudBees propose une solution pour déployer du code Java simplement. Le plus par rapport à Cloud Foundry c&#8217;est l&#8217;offre DEV@cloud qui propose une solution de GConf (GIT ou SVN) et une plate-forme d&#8217;intégration continue Jenkins. Ils sont placés pour Jenkins puisque [Kohsuke Kawaguchi](http://twitter.com/#!/kohsukekawa) a intégré leur équipe.

RUN@cloud est proche de l&#8217;offre de Cloud Foundry en se limitant au Java. Le plus c&#8217;est le monitoring des instances et la possibilité d&#8217;uploader un war depuis l&#8217;interface web. Par contre j&#8217;ai trouvé le SDK et le plug-in eclipse beaucoup moins faciles à utiliser comparés à ceux de Cloud Foundry.

Le gros problème de ces deux solutions, pour héberger mon application, c&#8217;est qu&#8217;elles ne supportent pas le multicast UDP. Je vais faire un autre poste plus tard pour détailler mon problème.

**Conclusion**

J&#8217;ai bien aimé tester ces offres rapidement et gratuitement. On peut enfin déployer du code java facilement. Avant il fallait louer un serveur privé pour pouvoir installer un serveur tomcat et ce n&#8217;était pas une solution économique (minimum 15 Euros par mois). Maintenant en quelques minutes notre war est disponible sur le net.

Après peut-on utiliser CloudBees ou Cloud Foundry pour déployer une application pro?  C&#8217;est à voir puisque je n&#8217;ai pas regardé comment affiner la configuration du serveur d&#8217;application. En tout cas c&#8217;est très prometteur.

Autres articles :

  * [Premiers pas sur CloudBees](http://blog.courtine.org/2011/07/10/premiers-pas-sur-cloudbees/) par Benoit Courtine
  * Blog de Xebia : [Lancement du projet PAAS cloud foundry de spring source](http://blog.xebia.fr/2011/04/13/lancement-du-projet-platform-as-a-service-cloud-foundry-de-spring-source/)
  * Blog d&#8217;octo : [Et si nous definissions simplement le cloud computing](http://blog.octo.com/et-si-nous-definissions-simplement-le-cloud-computing/)