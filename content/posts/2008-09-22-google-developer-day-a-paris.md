---
author: Samuel
categories:
  - Java
date: 2008-09-22 10:01:57+00:00
guid: http://www.net-liard.com/blog/?p=37
id: 112
permalink: /2008/09/google-developer-day-a-paris/
tags:
  - Chrome
  - Gear
  - Google
title: Google Developer Day à Paris
url: /2008/09/22/google-developer-day-a-paris/
---

Jeudi 18 avait lieu le google developer day à Paris. Petit résumé de la journée.

# Accueil

Après avoir montré patte blanche deux fois, on peut enfin entrer dans le hall, un petit déjeûner est offert. C&#8217;est entre deux petits fours que je croise [Grégory Weinbach](http://mdblog.fr/blog/) d&#8217;object Direct.

Une fois bien rassasié je continue le tour du bâtiment pour me diriger vers la salle de repos. Et pour une salle de repos c&#8217;est une belle salle de repos ! 4 écrans plats avec des Wii, deux baby-foot, un mikado géant, un domino géant, un puissance 4 géant, un jeu d&#8217;échec géant.. rien que ca ! Et le top du top c&#8217;est un tas de gros coussins aux couleurs de Google.

Après deux parties de Wii Tennis, il est temps d&#8217;assister au discours d&#8217;ouverture.

# Message d&#8217;introduction

Pour démarrer la journée, [Patrick Chanezon](http://wordpress.chanezon.com/) nous présente très rapidement l&#8217;ensemble des outils Google :

  * Chrome
  * Gears
  * App engine
  * GWT
  * OpenSocial
  * Androide

A chaque démo il faut switcher du Mac qui à les slides au PC, car Chrome ne fonctionne que sous Windows :). Et en plus de ces petites démonstrations, plusieurs sociétés nous présentent leur produit basé sur des outils Google :

  * [Mapeed](http://mapeed.com/) est un outil pour fusionner des marqueurs en fonction du niveau de zoom basé sur Google Maps.
  * MYerp.com est comme son nom l&#8217;indique un ERP en ligne ecrit avec GWT. 
  * [Viadeo](http://www.viadeo.com/) annonce l&#8217;ouverture de ses nouvelles APIs compatible OpenSocial

Par contre la petite démo d&#8217;android n&#8217;a pas été spectaculaire, l&#8217;application &#8220;blue dot&#8221; est beaucoup moins spectaculaire qu&#8217;à [Londres](http://www.youtube.com/watch?v=nmniBnVB6wA) où ils avaient un vrai téléphone.

J&#8217;ai ensuite choisi de participer au code lab sur App Engine.

# Code lab App Engine

App Engine est une solution d&#8217;hébergement fiable basé sur le langage python. Et la première question qui nous vient tous à l&#8217;esprit est bien sûr : &#8220;Pourquoi en Python ??&#8221; Et la l&#8217;équipe google nous répond que c&#8217;est peut être en lien avec l&#8217;arrivée de [Guido van Rossum](http://fr.wikipedia.org/wiki/Guido_van_Rossum) chez eux&#8230; Pas très technique comme explication.

Sinon App Engine propose plusieurs briques intéressantes :

  * Gestion de l&#8217;authentifcation Google
  * Gestion d&#8217;une base objet
  * Api d&#8217;envoi de mail

Le Code lab est bien fait, le but est de développer une application wiki avec le kit de dev. Il permet de tester son application en local.

En sortant du bâtiment j&#8217;ai même trouvé le scooter d&#8217;un Googler 😉

Même si ce code lab était bien fait, je suis resté un peu sur ma faim. J&#8217;attendais beaucoup plus d&#8217;explications sur la gestion de l&#8217;hébergement.

# Repas

J&#8217;ai profité du repas pour rencontrer Julien Dubois de [spring source](http://www.springsource.com/fr) et [Ludovic Toinel](http://www.geeek.org/) de Capgemini qui travaille sur les [API Orange Partner](http://www.orangepartner.com/site/frfr/home/p_home.jsp). Un moment d&#8217;échange très intéressant.

Ensuite j&#8217;ai participé à deux sessions sur Gear et Chrome.

# Gear

C&#8217;est Aaron Boodman qui nous présente Gear. C&#8217;est aussi l&#8217;occasion de fêter les un an de l&#8217;application. Gear offre des fonctionnalités avancées pour les applications web et notamment de pouvoir rendre en partie l&#8217;application accessible Offline.

Plusieurs points sont présentés :

**Desktop shortcuts**

Ca permet d&#8217;ajouter un icon sur le bureau pour ouvrir directement l&#8217;application Web. Le seul avantage par rapport à un lien http &#8220;normal&#8221; est de sauvegarder le navigateur utilisé et donc de ne pas simplement d&#8217;ouvir l&#8217;URL avec celui par défaut (intérêt très limité je trouve&#8230;)

**Gestionnaire de fichiers**

Gear offre une boite de dialogue qui permet d&#8217;utiliser des filtres et de sélectionner plusieurs fichiers. Encore mieux il gère une reprise sur erreur au niveau de l&#8217;upload de ces fichiers, très pratique en cas de transfert de gros fichiers (utilisé par Youtube bien-sûr)

**GeoLoc**

Une API de géolocalisation est aussi présente (via un GPS, une cellule GSM ou une IP)

# Chrome

Même si le titre de la session était nommée &#8220;Google Chrome&#8221;, c&#8217;était plus une présentation du moteur de JavaScripts V8.

D&#8217;abord les objectifs de Chrome (très bien illustré dans leur superbe [BD](http://www.google.com/googlebooks/chrome/small_00.html)) :

  * Stabilité
  * rapidité
  * intuitivité

Kevin Milinkin a fait la présentation la plus technique de la journée. On a même eu droit à un slide montrant le code assembler utilisé.

Déjà pourquoi faire un nouveau moteur de JavaScript ? La réponse est simple, au début des développements de Chrome il y a deux ans, la performance des moteurs Java Script existants n&#8217;etaient pas satisfaisante. C&#8217;est pour cette raison qu&#8217;ils ont lancé la réalisation de V8.

Il nous présente ensuite les clés de la rapidité du moteur :

  * Hidden class hidden transition
  * Inline caching
  * Dynamic Machine Code Generation
  * Efficient Garbage Collection

Ces points sont très bien expliqués [ici](http://code.google.com/apis/v8/design.html). V8 a aussi acceleré le temps de démarrage de la machine virtuelle en permettant le chargement d&#8217;objets en mémoire depuis un SnapShot.

Malheureusement il n&#8217;y a toujours pas de date pour la version Mac.

# Bilan

Même si je n&#8217;ai pas été seduit par le CodeLab, j&#8217;ai passé une excellente journée. C&#8217;est toujours intéressant d&#8217;échanger avec d&#8217;autres développeurs.