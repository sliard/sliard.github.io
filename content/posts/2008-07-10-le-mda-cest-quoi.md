---
author: Samuel
categories:
  - Modelisation
date: 2008-07-10 15:23:05+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.apptom.fr/?p=1569
id: 1569
permalink: /2008/07/le-mda-cest-quoi/
tags:
  - MDA
title: Le MDA c'est quoi ?
url: /2008/07/10/le-mda-cest-quoi/
---

Je suis toujours étonné de lire autant de réticences à propos du MDA. Cette méthode est peut être victime d&#8217;une communication trop éloignée des problèmes concrets des développeurs. Alors soyons clairs, moi non plus je ne suis pas en phase avec les grands théoritiens. Deux exemples concrets :

J&#8217;ai participé il y a 3 ans à une présentation d&#8217;une thèse sur le MDA. J&#8217;ai vu pendant 1 heure des séries d&#8217;équations pour m&#8217;expliquer le principe du MDA. Au final, je n&#8217;ai pas vu une ligne de code et je suis sorti avec un beau mal de crâne.

Un autre expert MDA m&#8217;a très sérieusement expliqué qu&#8217;il passait par 3 à 4 transformations successives pour arriver au code Java. De plus pour lui le principe du &#8220;round trip&#8221; ne sert à rien car son modèle ne change jamais. Bien sûr son super architecte a pensé à tout et les petits développeurs n&#8217;ont pas besoin de réfléchir&#8230; On rève..

Si on vous a présenté le MDA de cette façon je comprends mieux vos griefs.

Mais pour moi le MDA c&#8217;est :

  * **Mettre le modèle au centre du pojet.**
  * **Un outil pour produire mieux et plus vite.**
  * **Une façon d&#8217;abstraire des mécanismes techniques complexes.**

Il faut que le passage du modèle au code soit simple et rapide. Il faut aussi que ce soit le transformateur qui s&#8217;adapte au projet et non l&#8217;inverse. Là aussi j&#8217;ai vu trop d&#8217;outils imposer une façon de faire qui rebutait l&#8217;équipe de développeurs.

Oui on m&#8217;a déjà reproché de faire des PIM orientés Java et c&#8217;est aussi pour cette raison que l&#8217;on parle maintenant plutôt de MDD Model Driven Developpment. Mais mon objectif n&#8217;est pas d&#8217;être conforme à 100% avec la définition du MDA rédigée par l&#8217;OMG, mais bien de réaliser les trois points notés plus haut.

C&#8217;est assez paradoxal de pousser la modélisation UML et de mettre nos beaux modèles au placard lorsqu&#8217;ils sont terminés. C&#8217;est ça le MDA : s&#8217;appuyer sur un modèle pour structurer son développement.