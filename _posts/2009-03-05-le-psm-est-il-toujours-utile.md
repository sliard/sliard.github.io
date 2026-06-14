---
theme: modelisation
author: Samuel
categories:
  - Modelisation
date: 2009-03-05 23:49:05+00:00
guid: http://www.net-liard.com/blog/?p=214
id: 214
permalink: /2009/03/le-psm-est-il-toujours-utile/
tags:
  - Enterprise Architect
  - MDA
  - PIM
  - PSM
title: Le PSM est-il toujours utile ?
url: /2009/03/05/le-psm-est-il-toujours-utile/
---

Pendant plus de 4 ans nous avons travaillé sur un projet avec un outillage MDA en utilisant le mécanisme suivant pour générer du code :

![photo](/images/uploads/2009/03/psm1.png)

Sur le papier nous respections bien les concepts MDA avec une séparation du modèle abstrait de haut niveau (le PIM) et un autre spécifique à nos contraintes techniques (le PSM).

Mais si on regarde de plus près on trouve dans notre PIM des informations liées à nos choix technologiques que l&#8217;on ajoute grâce à un profil (stéréotype finder, tagged value sql_name, etc). A quoi sert notre PSM du coup ? Comme notre modeleur offrait une solution de génération de code Java, nous pensions intéressant de l&#8217;utiliser. Nous avons donc réalisé un transformateur modèle vers modèle pour construire un PSM collant aux besoins du générateur Java. Dans les faits le PSM nous a aussi permis de pallier à certains bugs de ce générateur en modifiant à la main le PSM pour obtenir du code Java correct. Mais notre PSM est une image un pour un du code java. 

Lorsque je montre cela à nos experts MDA, j&#8217;ai le droit systématiquement au discours : &#8220;Samuel t&#8217;as tout faux, il faut séparer les concepts. Regarde comment il faut faire&#8221;

![photo](/images/uploads/2009/03/psm2.png)

Effectivement sur le papier c&#8217;est une bonne idée. Il faut mettre les bonnes informations au bon niveau.

La première question que je pose à cette personne c&#8217;est : &#8220;Dis moi, ça fait combien de temps que tu n&#8217;as pas écrit une ligne de code ?&#8221;

C&#8217;est bien beau de philosopher sur MDA, mais on oublie vite la finalité : mieux produire du code. Si à chaque modification de modèle il faut faire trois transformations, c&#8217;est inutilisable ! Pour moi, dix secondes et deux clicks c&#8217;est le maximum acceptable par une équipe de développement pour passer du modèle au code. Si on met plus de temps ou s&#8217;il y a plus d&#8217;étapes l&#8217;outil est inexploitable.

C&#8217;est dans l&#8217;optique d&#8217;avoir moins d&#8217;étapes et de simplifier notre chaine de développement que nous utilisons maintenant une transformation Modèle vers Texte.

![photo](/images/uploads/2009/03/psm3.png)

Vous remarquerez que je n&#8217;utilise plus le mot PIM pour ne plus me faire taper sur les doigts 😉 Mais même si notre modèle n&#8217;est pas vraiment un PIM, il ne colle pas non plus au code et on peut s&#8217;appuyer dessus pour générer une belle documentation de haut niveau.

Dans ce cas il faut par contre réécrire un générateur Java. Mais le gros avantage est que ce générateur va répondre à 100% de vos exigences en terme de règle de codage et de formatage. De plus si l&#8217;outil de transformation est bien fait il offre de bonnes boites à outils (transformer une opération UML en signature de méthode Java par exemple). Si réécrire ce générateur est plus rapide et plus facile à maintenir qu&#8217;un tranformateur Modèle vers Modèle, cette méthode est plus intéressante. Et pourquoi utiliser des mécanismes complexes pour résoudre un problème simple ?

Concrètement nous avions presque 15 000 lignes de code J à maintenir juste pour notre transformateur Modèle vers Modèle, nous avons maintenant moins de 3 000 lignes de scripts acceleo pour générer le même code Java.

Donc aux vues de notre utilisation, avoir un modèle PSM n&#8217;apporte rien. Notre PSM c&#8217;est le code Java, après tout c&#8217;est un modèle comme un autre 😉