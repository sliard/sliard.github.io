---
theme: perso
author: Samuel
categories:
  - Perso
date: 2012-01-30 22:10:07+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.net-liard.com/blog/?p=1158
id: 1158
permalink: /2012/01/global-game-jam/
tags:
  - game
  - ggj12
  - global
  - jam
  - jeux video
title: Global Game JAM
url: /2012/01/30/global-game-jam/
wp_plus_one_redirect:
  - null
---

Ce week-end avait lieu le Global Game JAM. Cet évènement avait lieu dans 246 villes à travers le monde. Il était organisé sur Rennes au Jardin moderne par 2 associations :

  * [3hitcombo](http://www.3hitcombo.fr/ "http://www.3hitcombo.fr")
  * [west indie collective](http://westindiecollective.org/ "http://westindiecollective.org/")


![photo](/images/uploads/2012/01/ggj.png)

Je vais vous résumer comment ça c&#8217;est passé :

<!--more-->

## Vendredi 27

Après les annonces générales et quelques conseils, on passe directement au thème imposé par la Global. Cette année c&#8217;est une illustration :

![photo](/images/uploads/2012/01/200px-Ouroboros-simple.svg_.png)

On enchaine ensuite sur une séance de brainstorm collectif autour de ce thème, 1 heure où les idées fusent. Ensuite il est temps de constituer des équipes. Trois &#8220;mouvances&#8221; se constituent :

  * Les jeux de plateau
  * Les jeux vidéo multi-joueur
  * Les minis jeux / pixelart

On se regroupe donc en fonction de nos envies et de nos compétences. Je choisi de participé au groupe &#8220;mini jeux&#8221;. Nous sommes rapidement 9 avec des profils bien différents et donc complémentaires :  3 Graphistes, 3 Développeurs, 1 Game designer et 2 Sound designer. Reste maintenant à trouver une idée de jeux : un thème et un game play. Donc on recommence un long brainstorm pour ensuite tenter de trouver un consensus. L&#8217;exercice n&#8217;est pas simple à 9. Nous arrivons au final à vouloir faire un jeu de plateforme autour d&#8217;un personnage cherchant des toilettes de façon urgente. Ne me demandez pas ni pourquoi ni comment nous en sommes arrivés là, la fatigue sûrement&#8230;. La non consommation d&#8217;alcool ou de stupéfiant peut aussi expliquer ce manque de créativité.

A 23h il y avait 4 équipes de créées :

  * Un jeu de plateau avec des canards et des bombes
  * Un jeu de 3D temps réel
  * Un jeu de plateforme
  * Un jeu multijoueur PC et android.

Personnellement j&#8217;ai décidé de dormir la première nuit pour garder mes forces.

## Samedi 28

Dès 9h on a commencé à coder (c&#8217;est très tôt pour un samedi matin). Coder oui mais avec quel langage ? Nous sommes 3 développeurs maitrisant des technos différentes. Là on a deux choix, soit on choisit une techno neutre que personne ne maitrise vraiment bien pour s&#8217;y mettre à 3, ou on laisse un des développeurs prendre le lead et les 2 autres essaient de suivre. On a clairement choisi cette dernière solution et Christopher est parti sur une solution HTML/CSS/Javascript avec le framework [melonJS](http://www.melonjs.org/) (il a codé une bonne partie de la nuit de vendredi à samedi en fait).

De mon côté j&#8217;ai essayé de développer en parallèle une version sur iPhone basée sur [cocos2d](http://cocos2d.org/).

Notre WarRoom :

![photo](/images/uploads/2012/01/war.jpg)

En fait notre équipe a continué toute la journée à discuter autour du game play. Ca fusait dans tous les sens sur des idées de jauges de vie, objectif du jeu. Personnellement ça m&#8217;inquietait un peu de ne rien voir converger, je me suis donc concentré sur la version iPhone et la maitrise de cocos2d. Je n&#8217;avais jamais fait de jeu de plateforme avant, je suis donc parti de zéro. J&#8217;ai commencé par coder le défilement des différents niveaux d&#8217;image d&#8217;arrière plan pour donner un effet de profondeur. Heureusement la gestion des animations de sprite est de base dans cocos2d. Un moteur physique est aussi disponible, ce qui permet de faire rapidement sauter mon sprite de façon assez fluide.

L&#8217;objectif du jeu est super simple, le personnage cours et il doit éviter des obstacles. Je ne me voyais faire beaucoup plus en 48h.

J&#8217;ai commencé à avoir des problèmes avec la gestion des collisions. Je voulais utiliser un Tiled Map pour que ce soit éditable plus facilement. Mais après plusieurs heures, j&#8217;ai abandonné la gestion des fichiers TMX pour partir sur quelque chose de bien plus simple. Le positionnement des obstacles est géré à la main et la gestion de collision se limite à vérifier si mon personnage est au dessus d&#8217;une certaine hauteur au passage de l&#8217;obstacle.

A 1h30 du matin j&#8217;avais :

  * La gestion de 2 niveaux d&#8217;image de fond
  * La gestion du saut du sprite
  * L&#8217;ajout de façon aléatoire d&#8217;obstacles dans le jeu
  * La gestion de collision

et là il était temps de dormir, je n&#8217;ai plus 20 ans :)

## Dimanche 29

Reprise du code à 9h30 pas super frais. Pendant cette matinée les graphistes ont donné un coup de boost pour faire 4 nouveaux décors et finir les sprites des différents obstacles. J&#8217;ai donc passé ma matinée à intégrer leur boulot. Les sounds designer aussi ont pas mal bossé pour nous fournir du son pour chaque écran du jeu. Il fallait aussi faire l&#8217;enchainement des pages : Accueil, crédits, jeux, écran game over.

Quand nous avons compris vers 12h que notre développeur principal avait décidé de faire la grasse matinée la version HTML du jeu était très fortement compromise. Nous risquions donc de n&#8217;avoir que la version iPhone à montrer ce qui ajoutait un poil de stress.

On a terminé en intégrant le boulot des sounds designer pour avoir une application totalement terminée. Alors soit, le game play est plus que minimaliste, le thème est loin d&#8217;être très classe mais on a quand même le mérite de l&#8217;avoir terminé en 48h 😉

A 15h on publiait une vidéo sur youtube pour montrer ce que ça donne :

Ca a le mérite au moins de beaucoup faire rire mes enfants 

En plus de notre application iPhone, 3 jeux ont été présentés ce dimanche

### Aux quatre coin coin

Jeux de plateau très bien fait. Un gas a même pris le temps de sculter de superbes petites pièces de jeu. Admirez ce superbe plateau fait en aquarelle :

####Jörmungand

[![photo](/images/uploads/2012/01/photo_board_preview-300x214.jpg)](http://globalgamejam.org/2012/aux-quatre-coin-coin)

Je n&#8217;avais pas bien compris le principe de ce jeu lorsqu&#8217;ils l&#8217;avaient présenté la première fois. Mais j&#8217;ai été bluffé par leur démo le dimanche après midi. Ils ont codé un jeu en 3D avec une partie reconnaissance de tag via une webcam.

####STRAT

[![photo](/images/uploads/2012/01/jurmungand-300x175.png)](http://globalgamejam.org/2012/j%C3%B6rmungand)

Là par contre leur démo n&#8217;a pas été transcendante  :)Mais ils ont développé un jeux multi-joueur sur Android avec un écran principal sur un PC. C&#8217;était la seule équipe avec des développeurs travaillant sur la même techno et ça les a bien aidé.

####Bilan

[![photo](/images/uploads/2012/01/Visu-300x240.png)](http://globalgamejam.org/2012/strat)

J&#8217;ai beaucoup aimé ce week-end. C&#8217;est très stimulant d&#8217;avoir une forte contrainte de temps. En tant que développeur j&#8217;ai aussi bien apprécié d&#8217;être entouré de graphistes et de sound designer. C&#8217;est super enrichissant de voir comment ils travaillent vu que c&#8217;est un monde qui m&#8217;est complètement inconu.

Si je pouvais vous donner un seul conseil pour bien réussir ce type de week-end c&#8217;est d&#8217;essayer d&#8217;avoir une équipe de développeurs homogène. Ca permet de mieux se partager le travail et de ne pas être dépendant d&#8217;une seule personne.

L&#8217;objectif du startup week-end c&#8217;est de construire une startup en 56 heures. Etablir un business model cohérent c&#8217;est ça la priorité numéro 1 pour finir sur le podium. L&#8217;objectif du week-end Global Game JAM c&#8217;est de créer un jeu, de s&#8217;amuser. Il n&#8217;y a pas de gagnant, pas de podium. Là les développeurs ont vraiment leur place (contrairement au [startup weekend à mon avis](/2011/11/startup-week-end-bretagne/)). J&#8217;y ai fait de belles rencontres et je commence à réfléchir pour l&#8217;organiser sur Lannion en 2013.