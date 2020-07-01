---
author: Samuel
categories:
  - Arcade
date: 2009-09-07 08:15:23+00:00
guid: http://www.net-liard.com/blog/?p=466
id: 466
permalink: /2009/09/dreamcast-to-jamma-la-video/
tags:
  - Dreamcast
  - Dreamcast2Jamma
  - Jamma
  - PCB
title: "Dreamcast to Jamma : la video"
url: /2009/09/07/dreamcast-to-jamma-la-video/
---

Comme je l&#8217;ai noté dans l&#8217;article précédent, je compte retaper une borne d&#8217;arcade. Dans un premier temps j&#8217;ai envie d&#8217;utiliser ma vieille Dreamcast qui prenait la poussière dans cette borne. Et bien croyez moi, on est loin du plug and play !

Je débarque un peu dans ce monde et il y a pas mal de choses à connaitre.

## Le port Jamma

<img class="aligncenter" title="jamma" src="http://farm3.static.flickr.com/2590/3887595296_f0b61d6317_m.jpg" alt="" width="240" height="180" />

Au milieu des années 80 les constructeurs ont eu la bonne idée de normaliser les branchements de leurs bornes. Grâce à ça un jeu avec un connecteur Jamma peut être utilisé dans toutes les bornes compatibles. Dans une borne, ce connecteur Jamma est relié au panel (manettes et boutons), à l&#8217;ecran, au haut parleur et à une alimentation fournissant du +5V, -5V et 12V. C&#8217;est un peu comme si on avait regroupé les ports VGA, PS2 et l&#8217;alim ATX sur un seul connecteur.

## Les PCB

<p style="text-align: center;">
  <img class="aligncenter" title="pcb" src="http://farm3.static.flickr.com/2622/3838709143_f5630b9b49_m.jpg" alt="" width="240" height="180" />
</p>

Printed Circuit Board, c&#8217;est la plaque électronique qui contient un jeu, les plus répandues se plug  dans le port Jamma. Elle rassemble CPU, mémoire ROM avec le code du jeu et mémoire RAM. Il y a même un petit espace de stockage pour sauvegarder les meilleurs scores, en général une EEPROM.

Ma borne est compatible Jamma et j&#8217;ai deux jeux en PCB, un tetris et World Cup 90. C&#8217;est pas les meilleurs jeux, mais si je veux en mettre d&#8217;autres il faut trouver les PCB. C&#8217;est pas forcément évident à trouver si on cherche un jeu précis et ça peut valoir cher (entre 50 et 150 Euros).

En lisant les forums j&#8217;ai découvert que beaucoup branchaient leur dreamcast dans leur borne. C&#8217;est plus simple pour trouver des jeux. Et là, coup de chance, j&#8217;ai justement une dreamcast dans un carton au garage. Je me décide donc à la brancher dans la borne.

Premier objectif, afficher le jeu sur l&#8217;écran de la borne d&#8217;arcade. Il faut donc convertir le signal vidéo de la péritel pour le mettre sur le connecteur Jamma. La bonne nouvelle c&#8217;est que la dreamcast sort la vidéo en RGB ce qui est justement la norme Jamma. Mais il y a un hic (et oui trop simple sinon) il faut un signal de synchro vidéo qui n&#8217;est pas sur la péritel. Heureusement il est possible de le reconstruire à partir du signal de vidéo composite à l&#8217;aide d&#8217;un petit montage électronique.

![photo](/images/uploads/2009/09/circuit1.gif)

Un petit CI, deux condos et une résistance, ça ne me paraissait pas bien sorcier. Je ressors donc mon fer à souder pour la réaliser. La dernière fois que j&#8217;ai soudé des composants c&#8217;était chez Bull à Angers dans l&#8217;équipe de diagnostic/réparation de carte mère de PC en 1997 (douze ans deja !). A la base j&#8217;ai quand même un DUT d&#8217;électronique, ça peut servir :)

Une fois cablé, je place ce montage entre la péritel Dreamcast et le port Jamma. La première fois j&#8217;ai encore un problème de synchro verticale. Aprés avoir cherché sur des forums, on a fini par m&#8217;aider à trouver un potentiomètre de règlage de l&#8217;écran et comme par magie l&#8217;image se stabilise !

Même stable l&#8217;image était super sombre. Le problème c&#8217;est que les télévisions intègrent un ampli vidéo que la borne d&#8217;arcade n&#8217;a pas. Le signal en sortie de la Dreamcast est donc trop faible. Encore une fois grâce aux sites spécialisés dans l&#8217;arcade je trouve un schéma d&#8217;ampli.

![photo](/images/uploads/2009/09/vamp.gif)

Bon là c&#8217;est un peu plus costaud quand même. Premier problème, il faut utiliser deux transistors BC108B et BC178B, impossible d&#8217;en trouver chez les revendeurs. Il faut donc chercher encore une fois sur les forums pour savoir que l&#8217;on peut les remplacer par des BC548B et BC558B. Une fois les composants réunis, j&#8217;ai utilisé une platine d&#8217;essai pour tester le montage une première fois. Vous savez les plaques blanches dans lesquelles on peut piquer des composants. Ca évite d&#8217;avoir à les souder pour un premier essai. Et là par chance ça marche du premier coup ! Il faut donc refaire le circuit sur une plaque adéquate. Le schéma noté plus haut ne me convient pas. Déjà la plaque que j&#8217;ai achetée est moins large, je ne peux pas mettre les trois amplis alignés. L&#8217;espace laissé pour les résistances est beaucoup trop faible, il faut au moins 1 cm pour en placer une correctement. Et pour finir j&#8217;aimerais bien avoir le LM1881 sur la même plaque. J&#8217;ai donc réalisé un nouveau schéma.

![photo](/images/uploads/2009/09/plaque.png)

Une fois les composants soudés ça donne cela :

<img class="aligncenter" title="plaque" src="http://farm3.static.flickr.com/2588/3890593366_a740afcf2f_m.jpg" alt="" width="180" height="240" />

Et voilà je peux jouer à la Dreamcast sur l&#8217;écran de la borne d&#8217;arcade ! La prochaine étape est de pouvoir utiliser les joysticks de la borne à la place des manettes et d&#8217;y mettre le son.

Les sites que j&#8217;ai utilisés :

Le site avec tous les montages : [mameWorld](http://pc2jamma.mameworld.info/hardware.html)

Un bon tutoriel en francais : [tuto](http://www.gamoover.net/tuto/brancher-une-dreamcast-dans-une-borne-video-son-controles)

un forum bien pratique : [gameoover](http://www.gamoover.net/Forums/index.php)