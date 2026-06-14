---
theme: modelisation
author: Samuel
categories:
  - Modelisation
date: 2011-06-29 15:32:46+00:00
guid: http://www.net-liard.com/blog/?p=892
id: 892
permalink: /2011/06/obeo-designer-roadshow/
title: Obeo Designer Roadshow
url: /2011/06/29/obeo-designer-roadshow/
---

<!-- p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Helvetica} p.p2 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Helvetica; min-height: 14.0px} -->

![photo](/images/uploads/2011/06/bus_203x104.png)

Hier se déroulait à Brest le ObeoDesigner roadshow.

Avant de présenter l&#8217;outil, il faut commencer par la base.

**Le DSL : Domaine Specific Language**

Le principe est de définir son propre langage pour modéliser son environnement. Là où en UML on a (pratiquement) que des classes, dans un DSL on peut utiliser notre langage métier et parler de &#8220;Portable&#8221;, d'&#8221;Avion&#8221; etc.. Mais qui dit nouveau langage dit nouvelle représentation graphique. Avec un DSL il faut aussi réinventer vos propres représentations graphiques. Lorsqu&#8217;on utilise UML on a l&#8217;avantage d&#8217;avoir pléthore d&#8217;éditeurs graphiques sur le marché.

Mais plus grave à mon avis : on ne partage plus la même représentation graphique. Lorsque je lis un diagramme de séquence UML je sais si un appel est synchrone ou asynchrone en fonction de sa représentation. Avec les DSL il faut non seulement redévelopper ses diagrammes, mais il faut en plus les expliquer à chaque fois.

**Obeo Designer**

Obeo Designer propose une solution pour le premier problème : réaliser des diagrammes personnalisés s&#8217;appuyant sur votre DSL.

Il est basé sur 5 types de représentation :

  * Tree
  * Edition Table
  * Cross Table
  * Diagram
  * Sequence Diagram

Pour l&#8217;avoir pratiqué une après midi, on arrive assez rapidement à construire un diagramme. L&#8217;outil est très pratique; dès que l&#8217;on fait une modification on peut voir le résultat en live sur le diagramme.

![photo](/images/uploads/2011/06/obeodesigner11-300x151.jpg)

Le gros point faible de l&#8217;outil est, à mon avis, le manque d&#8217;aide (complétion, coloration..) pour écrire les scripts Acceleo. En plus ce sont des scripts Acceleo 2 (alors que le générateur de code est en Acceleo 3).

www.obeonetwork**.com**

Cette journée a été aussi l&#8217;occasion d&#8217;annoncer l&#8217;ouverture du site www.obeonetwork.com. Cet espace collaboratif va nous permettre de partager nos réalisations Acceleo / Obeo Designer. Même si je pense qu&#8217;il vaut mieux réaliser un générateur différent par projet qu&#8217;essayer de faire LE générateur générique, rien n&#8217;empêche de partir d&#8217;un existant pour le spécifier à son besoin (le transformateur hibernate par exemple).

&nbsp;

Pour conclure j&#8217;ai passé une bonne journée et c&#8217;est toujours un plaisir de rencontrer [Frederic Madio](http://twitter.com/#!/fmadiot) et [Etienne Julio](http://twitter.com/#!/ejuliot) (la star sur [les cast codeurs](http://lescastcodeurs.com/2011/06/les-cast-codeurs-podcast-episode-41-interview-detienne-juliot-sur-eclipse/) 😉 ). Je reste quand même assez attaché à UML. Même si UML est beaucoup trop vaste et très compliqué il a le mérite d&#8217;apporter un langage normalisé et beaucoup d&#8217;outils s&#8217;appuient dessus.

C&#8217;est donc sûrement pour me faire plaisir qu&#8217;Obeo a annoncé Mardi qu&#8217;ils allaient donner gratuitement un modeleur UML construit avec Obeo Designer. Ce module UML est publié sur le [MarketPlace obeonetwork](http://marketplace.obeonetwork.com/module/uml) et le code source est sur [GitHub](https://github.com/ObeoNetwork/UML-Modeling). C&#8217;est donc un exemple très complet sur lequel on peut s&#8217;appuyer.

Cerise sur le gâteau, on a eu un bon de réduction de 20% que j&#8217;ai bien sur immédiatement mis en vente [sur ebay](http://cgi.ebay.fr/ws/eBayISAPI.dll?ViewItem&item=320720998796#ht_500wt_990) :)

![photo](/images/uploads/2011/06/ebay-300x142.jpg)