---
theme: modelisation
author: Samuel
categories:
  - Modelisation
date: 2008-07-09 15:25:05+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.apptom.fr/?p=1571
id: 1571
permalink: /2008/07/le-mda-cest-agile/
tags:
  - MDA
title: Le MDA c'est Agile !
url: /2008/07/09/le-mda-cest-agile/
---

Je viens de lire [Je viens de lire](http://www.touilleur-express.fr/2008/07/09/debriefing-comme-dhabitude-a-pas-dheure-de-la-soiree-paris-jug/) résumant la soirée Paris JUG d&#8217;hier soir.

Et au milieu on peut lire : &#8220;_non MDA n’est pas une méthode Agile_&#8220;

Horreur ! Je ne peux donc pas m&#8217;empecher de réagir 

Bien sur que le MDA aide à être plus agile ! Mais attention, il ne faut pas non plus trop écouter les puristes&#8230;
  
Je ne crois pas non plus à la notion &#8220;d&#8217;indépendance du langage&#8221;&#8230; c&#8217;est utopique, mais ça permet une certaine abstraction. C&#8217;est aussi une absurdité de mettre un fossé entre les développeurs et les architectes. L&#8217;architecte va oublier des choses dans le modèle, il faut laisser les développeurs l&#8217;aider à le compléter.

Un exemple concret :
  
Il y a 4 ans j&#8217;ai commencé un projet avec des EJB 2 session et entity. Pour les personnes qui n&#8217;ont pas la chance de connaitre les EJB 2&#8230;. c&#8217;est atroce. Pour persister une classe il faut écrire 4 classes Java + des descripteurs xml.
  
Pour nous simplifier la vie nous avons modélisé notre système sans parler d&#8217;EJB. Un modele de haut niveau donc&#8230; un PIM.
  
Ensuite nous avons écrit un transformateur PIM-> PSM EJB 2 (15j de travail )
  
On génère classe Java + descripteurs EJB + script SQL.

Et la c&#8217;était magique !!
  
**1 &#8211;** A la fin de la phase de modélisation, j&#8217;ai appuyé sur UN bouton et j&#8217;ai obtenu 100 % de mes squelettes de code Java. Sans aucun codage j&#8217;avais un EAR deployable !

Attention ! cet EAR était bien une coquille vide, il est pour moi hors de question de modéliser le comportement. Il restait donc à notre équipe de développeurs à coder les services EJB.
  
Mais il était déjà deployable, on pouvait donc écrire des JUnits avant d&#8217;écrire l&#8217;implémentation.

**2 &#8211;** Justement à propos de l&#8217;équipe&#8230; allez trouver sur le marché des développeurs EJB 2. (pas chers donc débutants&#8230;)
  
Et bien grâce à l&#8217;approche MDA nous avons pu prendre des débutants. En effet le coté EJB était transparent au début ils codaient de simples méthodes Java.

Et au fur et à mesure ils sont montés en compétences sur les EJB 2 bien sur.

**3 &#8211;** Notre modèle est en phase avec notre code après 4 ans de dev&#8230; qui dit mieux ? 😉

**4 &#8211;** Le MDA est agile !!
  
C&#8217;est une approche qui nous aide à être plus agile car elle facilite les changements.
  
Ajouter un attribut à un entity, c&#8217;est modifier 2 classes Java + un descripteur Java + un script SQL. Soit 4 chances d&#8217;oublier une modif ou de faire une erreur.
  
Avec nos outils MDA : une modif dans le modele + un clic = c&#8217;est fini.

Pour finir : la cerise sur le gâteau.
  
L&#8217;année dernière nous avons migré nos EJB 2 vers de l&#8217;hibernate. Et bien nous avons juste changé de transformateur MDA&#8230; zero modif dans notre code.

C&#8217;est pas de l&#8217;agilité ça ! :)