---
author: Samuel
categories:
  - Modelisation
date: 2009-02-19 22:26:32+00:00
guid: http://www.net-liard.com/blog/?p=188
id: 188
keywords:
  - Modelio, Objecteering, UML, MDA
permalink: /2009/02/premier-test-de-modelio/
tags:
  - MDA
  - Modelio
  - objecteering
  - UML
title: Premier test de Modelio
url: /2009/02/19/premier-test-de-modelio/
---

Après avoir passé quelques heures à tester Modelio je vous en fais un petit retour. 

## Installation

La première bonne nouvelle est qu&#8217;il est possible d&#8217;avoir sur un même poste plusieurs versions différentes de Modelio. J&#8217;ai installé la version Free et la version Java sur mon poste sans problème. Bien-sûr un projet créé avec la version Java n&#8217;est pas utilisable avec la version free (l&#8217;inverse est possible par contre).

L&#8217;empreinte mémoire est assez faible (100Mo). Ca reste raisonnable. Par contre l&#8217;ouverture et la création de projet est vraiment lent et le fichier contenant le modèle est déjà gros même vide.

## Utilisation

La première chose que je remarque c&#8217;est la disparition de la barre action gauche au niveau du modèle Explorer.

![photo](/images/uploads/2009/02/modelio1.jpg)

A la place il faut utiliser les menus pop-up du click droit comme avec l&#8217;éditeur de modèle emf d&#8217;Eclipse. C&#8217;est vraiment dommage et je trouve que l&#8217;on perd beaucoup de temps pour construire un modèle.

Ensuite il manque toujours une aide à l&#8217;édition sur les diagrammes au niveau de la création des liens entre item (association, dépendances et autre). Je parle de cette petite flèche qui apparait en haut à droite de l&#8217;élément d&#8217;un diagramme lorsque la souris est au dessus et qui permet de créer une association ou un autre type de lien avec un autre item. RSM et EA le propose depuis pas mal de temps et je m&#8217;y suis bien habitué.

Attention aussi à la gestion du delete, maintenant lorsqu&#8217;on supprime un élément d&#8217;un diagramme, il est aussi supprimé sur modèle.

## Génération Java

Une des nouveautés est l&#8217;utilisation d&#8217;annotation Java5 pour remplacer les marqueurs en commentaire.

![photo](/images/uploads/2009/02/modelio21.jpg)

C&#8217;est plus lisible, mais il faut accepter d&#8217;être dépendant d&#8217;un jar medelio. L&#8217;utilisation des annotations n&#8217;est possible qu&#8217;en mode &#8220;Round Trip&#8221;, lorsque l&#8217;on passe en mode &#8220;Model Driven&#8221; on revient sur une utilisation de commentaires Java.

La gestion des attributs d&#8217;une classe Java ne semble pas vraiment pratique. A partir du moment où un attribut est noté privé, les méthodes get et set de celui-ci apparaissent comme par magie ! (en fonction de son mode d&#8217;accès quand même). C&#8217;est très troublant. On peut bien sûr les effacer mais à la moindre modification de l&#8217;attribut elles réapparaissent ! L&#8217;avantage est de pouvoir customizer le code java des getter et setter, ce qui était impossible avec Objecteering. Par contre maintenant le modèle est vraiment une représentation du code à l&#8217;identique. Je ne suis pas très fan de cette approche, je préfère avoir un modèle assez haut niveau (un PIM si on veut) qui peut se mapper sur mon code (le PSM du coup). 

Par contre les produits de génération n&#8217;existent plus. On ne peut configurer qu&#8217;un seul répertoire de génération de code. Donc maintenant un projet UML = un projet Java. C&#8217;est très génant si comme moi vous représentez plusieurs couches de votre application dans un seul modèle mais que chaque couche a son propre projet java.

## Conclusion

Mes premiers essais sont assez mitigés, les nouveautés de Modelio sont loin de compenser les fonctions retirées d&#8217;objecteering (produit de génération, barre d&#8217;action etc&#8230;).

Au niveau UML 2, rien à dire, le méta-modèle est bon. Modelio contrôle bien la validité du modèle. Pour moi c&#8217;est un plus. Même si des outils comme EA où on peut faire tout et n&#8217;importe quoi paressent plus simples à prendre en main, au final ils engendrent souvent des modèles inutilisables. 

Par contre le plus grave aujourd&#8217;hui est que l&#8217;import XMI ne fonctionne pas et il n&#8217;y a même pas d&#8217;export XMI. Sans export XMI, le modèle est emprisonné dans Modelio. Pour moi il est hors de question d&#8217;utiliser un outil sans avoir une solution pour exploiter le modèle avec d&#8217;autres outils de transformation de modèle ou de génération de code (comme Acceleo par exemple). J&#8217;ai fait cette erreur avec Objecteering 6 qui n&#8217;avait pas d&#8217;export XMI, on ne m&#8217;y remprendra pas ! :)

J&#8217;attends toujours de tester la partie MDA et multi-user avec SVN de Modelio. Mais il faut attendre la version entreprise en Mars-Avril pour ça.

Affaire à suivre donc !