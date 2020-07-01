---
author: Samuel
categories:
  - Cloud
date: 2012-07-18 22:01:10+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.apptom.fr/?p=1290
id: 1290
permalink: /2012/07/google-app-engine-suite/
tags:
  - cloud
  - GAE
  - Google
  - Goole App Engine
title: Google App Engine Suite
url: /2012/07/18/google-app-engine-suite/
---

Comme expliqué dans le premier article j&#8217;ai rencontré certaines difficultés au niveau du développement avec Google App Engine. L&#8217;intégration et la gestion de la plate-forme a aussi amené son lot de surprises.

## Gestion des instances

Nous utilisons GAE pour un service qui a peu de trafic. En mode gratuit aucune instance n&#8217;est lancée par défaut, donc chaque utilisateur a un risque de déclencher le lancement d&#8217;une instance. Il faut 18 secondes pour démarrer mon instance: 18 secondes ce n’est pas énorme pour démarrer un serveur d&#8217;applications, par contre pour répondre à une requête HTTP c&#8217;est une éternité.

Pourquoi ces 18 secondes ? J&#8217;ai décomposé un peu les choses :

  * 2s &#8211; GAE avec juste une servlet
  * 11s &#8211; Spring (MVC + Security)
  * 2s &#8211; URLRewrite
  * 2s &#8211; objectify

C&#8217;est donc clairement Spring qui prend le plus de temps au démarrage. Mais d&#8217;un autre côté, même sans 6 secondes pour répondre à une requête c&#8217;est déjà trop.

Pour éviter ce problème, il faut donc minimiser le nombre de démarrages d&#8217;instance. La solution &#8220;lowcost&#8221; est de configurer un cron toutes les minutes sur votre application. De cette façon vous avez une chance d&#8217;avoir toujours une instance en ligne et vos clients ont des temps de réponse corrects. Mais ce n&#8217;est pas une science exacte, j&#8217;ai quand même eu des problèmes. L&#8217;autre solution est d&#8217;activer la facturation (2,10$ par semaine au minimum) pour utiliser les instances &#8220;idle&#8221;. Vous pouvez garder N instances démarrées sans arrêt. Mais même avec cette option je n&#8217;ai pas un comportement satisfaisant. Déjà certains clients tombent encore sur une requête de 18s, c&#8217;est très rare heureusement, mais ce qui m&#8217;inquiète le plus c&#8217;est de voir GAE devoir lancer 3 instances pour répondre à 2 clients ! Sur les 24 dernières heures j&#8217;ai eu 400 requêtes (statiques et dynamiques), je pense que même un simple apache sur une instance micro Amazon est capable d&#8217;encaisser cette charge et bien GAE a eu besoin de lancer 2 instances.

D&#8217;un autre côté, la notion d&#8217;instance &#8220;idle&#8221; veut bien dire ce qu&#8217;elle veut dire : &#8220;instance inactive&#8221;. C&#8217;est un moyen de pouvoir anticiper un pic de charge. Donc dès qu&#8217;un utilisateur arrive sur mon service, une seconde instance est lancée (par une requête /_ah/warmup). Donc il est assez logique de voir souvent 2 instances. Mais pourquoi GAE en lance régulièrement une troisième !?

J&#8217;ai donc beaucoup de mal à comprendre ce fonctionnement difficilement prévisible, les joies du PAAS :)

## Un problème avec la 3G

On a eu un autre problème heureusement passager. Le 18 juin pendant plusieurs heures tous les services hébergés sur GAE n&#8217;étaient plus accessibles sur les réseaux 3G Bouygues et Orange. J&#8217;ai fait le test sur plusieurs services utilisant GAE en wifi, sur une box ou sur le réseau SFR aucun problème, mais sur les réseaux Orange et Bouygues on avait la page :

![photo](/images/uploads/2012/07/photo-217x300.png)

Aucun retour de google sur ce problème qui heureusement ne s&#8217;est pas reproduit.

## Conclusion

C&#8217;est donc une expérience un peu mitigée. Ce manque de contrôle me gêne un peu. Si on ajoute à cela que le développement réalisé est complètement dédié à GAE, il faut vraiment réfléchir avant de choisir cette plateforme. En tout cas si vous tentez l&#8217;aventure, surtout pensez au temps de démarrage de l&#8217;instance dès le début. Mais oubliez Spring ou Play qui ne fait pas mieux à ce niveau-là.