---
author: Samuel
categories:
  - HTML
  - iPhone
date: 2011-10-20 22:36:04+00:00
guid: http://www.net-liard.com/blog/?p=1031
id: 1031
permalink: /2011/10/premier-essai-phonegap/
tags:
  - CSS
  - iPhone
  - Javascript
  - PhoneGap
title: Premier essai de PhoneGap
url: /2011/10/20/premier-essai-phonegap/
---

![photo](/images/uploads/2011/10/PhoneGap.gif)

Dernièrement j&#8217;avais à développer une application mobile sans grosse difficulté technique. J&#8217;ai donc eu envie d&#8217;essayer de la réaliser avec PhoneGap.

Je ne vais pas faire d&#8217;article pour expliquer comment fonctionne PhoneGap car beaucoup l&#8217;on déjà fait mieux que je ne peux le faire (comme [octo par exemple](http://blog.octo.com/applications-mobiles-multi-plateformes-les-approches-phonegap-et-titanium-mobile/)) mais juste faire un petit retour d&#8217;expérience.

La base de PhoneGap c&#8217;est de pouvoir faire des applications mobiles mutliplate-forme en développement en HTML/CSS/Javascript.

Je ne suis vraiment pas un spécialiste du HTML et encore moins du Javascript. Mais je pense qu&#8217;il est grand temps de s&#8217;y mettre et ce petit projet est une bonne occasion.

Je débute donc et rapidement je tombe sur un premier problème : le titre dans la nav bar en haut de page est tronqué. J&#8217;ai rapidement trouvé où changer le CSS pour corriger cela. Ouf <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

Je développe avec Dreamweaver et c&#8217;est assez agréable. En effet il supporte JQuery et PhoneGap. Ca me permet d&#8217;avoir un aperçu direct du rendu de mon code et en 2 cliques ça me génère un projet XCode et lance directement le simulateur iPhone pour tester l&#8217;application.

Par contre on arrive vite aux limites de Dreamweaver au moment où on utilise du javascript PhoneGap. Par exemple, j&#8217;avais besoin de gérer le changement d&#8217;état de l&#8217;application (passage en background, retour au premier plan..). Pour ça il faut utiliser la méthode :

`document.addEventListener("resume", onResume, false);`

Mais impossible de le tester dans un navigateur ou dans Dreamweaver. Ca ne fonctionne bien sûr que sur l&#8217;iPhone.

Et là, re-problème, ma méthode onResume ne se lance jamais  <img src="http://www.apptom.fr/wp-includes/images/smilies/frownie.png" alt=":(" class="wp-smiley" style="height: 1em; max-height: 1em;" />Je suis donc parti sur une longue demi-journée de debug à base de alert(&#8220;je passe là&#8221;) pour finir par comprendre que Dreamweaver utilise une ancienne version de PhoneGap ne gérant pas l&#8217;évènement &#8220;resume&#8221;. Impossible de trouver le numéro de version PhoneGap utilisé ! Et pas d&#8217;explication non plus sur comment utiliser une autre version. J&#8217;ai même bêtement intégré le fichier phonegap-1.1.0.js dans mon projet : marche pas car c&#8217;est la lib PhoneGap du projet XCode généré qu&#8217;il faut changer.

J&#8217;ai donc fini par abandonner la génération PhoneGap intégré par DreamWeaver. J&#8217;utilise PhoneGap normalement dans XCode et Dream ne me sert que d&#8217;éditeur de texte car la complétion et l&#8217;aperçu c&#8217;est quand même bien pratique.

J&#8217;avais l&#8217;impression d&#8217;avoir réalisé le plus dur. Il me restait à ouvrir une simple petite fenêtre popup. Et là, catastrophe, le rendu sur un navigateur est différent de celui sur l&#8217;iPhone. Plus grave la transition au moment de la fermeture de la popup fonctionne si elle est ouverte depuis la première page mais pas depuis les autres. Je pense que c&#8217;est un problème JQuery et pas PhoneGap puisque je constate le même problème sur un navigateur.

Comment faire pour débugger ??

C&#8217;était trop pour moi, j&#8217;ai préféré abandonner et repasser sur de l&#8217;Objective-C. En une journée j&#8217;ai refait ce que j&#8217;avais mis 3 jours à faire en Javascript (normal, je maitrise mieux) et hop ça marche !

Donc non PhoneGap ne m&#8217;a pas convaincu. En fait pour être plus juste, c&#8217;est plus le Javascript qui m&#8217;a bloqué. Déjà je n&#8217;ai pas assez d&#8217;expérience avec ce langage, mais c&#8217;est surtout une vraie galère à débugger !