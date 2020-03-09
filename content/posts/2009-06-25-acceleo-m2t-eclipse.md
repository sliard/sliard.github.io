---
author: Samuel
categories:
  - Modelisation
date: 2009-06-25 23:14:01+00:00
guid: http://www.net-liard.com/blog/?p=421
id: 421
permalink: /2009/06/acceleo-m2t-eclipse/
tags:
  - Acceleo
  - Eclipse
  - MDA
title: Acceleo M2T et Eclipse 3.5
url: /2009/06/25/acceleo-m2t-eclipse/
---

Comme vous le savez Eclipse 3.5 Galileo est sorti le 24 Juin.

Une des nouveautés est l&#8217;intégration d&#8217;Acceleo M2T directement dans la version &#8220;Eclipse Modeling Tools&#8221;.
  
Je n&#8217;ai pas passé beaucoup de temps à l&#8217;essayer, mais on peut déjà noter plusieurs grosses améliorations. Bien sur la plus importante est le changement de langage de script. On passe d&#8217;un format spécifique Acceleo à du MTL standard défini par l&#8217;OMG pour les transformations Model to Text.

Je vais plus me focaliser sur les nouveautés au niveaux outillage.

## Installation facile

Avant je n&#8217;avais jamais réussit à installer Acceleo sur mon Eclipse via leur update site. Il y avait toujours des problèmes avec les versions d&#8217;emf, uml2&#8230; J&#8217;ai perdu beaucoup de temps et le seul moyen de le faire fonctionner rapidement était de récupérer leur package Eclipse+Acceleo.

Cette fois j&#8217;ai installé un Eclipse 3.5 vierge et via l&#8217;update site de Galileo je peux installer Acceleo 0.8. Au moment de l&#8217;installation il m&#8217;a installé toutes les dépendances nécessaires (emf&#8230;) En 5 minutes ça marche. Seul petit hic, il ne tire pas les dépendances vers le plugin uml2 et l&#8217;exemple ne fonctionne pas sans. Mais si vous avez téléchargé la version &#8220;Eclipse Modeling Tools&#8221; tout fonctionne sans passer par l&#8217;update.

## Exécution en standAlone

Même si cette fonctionnalité existe depuis la version 2.4.0 d&#8217;Acceleo, on note maintenant la disparition complète des chaines de lancement Acceleo. Pour générer notre code on peut donc utiliser au choix :

  * Du Java
  * Une tache ant
  * Un runner Eclipse

Il ne manque plus qu&#8217;un plug-in Maven 2, mais vu que l&#8217;équipe d&#8217;acceleo utilise plus ivy que Maven il faudra peut être le réaliser nous-même.

## Debug

Je gardais le meilleur pour la fin, il est enfin possible de mettre des points d&#8217;arrêt dans nos templates. Ca marche très bien et on peut facilement naviguer dans notre model comme on le fait avec des objets en debug Java.
  
C&#8217;était le gros manque au niveau outillage d&#8217;Acceleo, c&#8217;est maintenant très bien fait.

Une grosse évolution très intéressante d&#8217;Acceleo donc. Je suis même étonné qu&#8217;il n&#8217;y ait pas plus d&#8217;infos à ce propos sur leur site Web. Ils sont trop occupés à préparer [l&#8217;Acceleo Day](http://www.acceleo.org/wiki/index.php/Eclipse_Acceleo_Day) du 10 Juillet peut être  <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />Journée annoncée sur la page d&#8217;acceuil d&#8217;Eclipse, la classe !

![photo](/images/uploads/2009/06/acceleoday.jpg)
