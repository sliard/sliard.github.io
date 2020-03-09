---
author: Samuel
categories:
  - Agile
  - Java
date: 2011-03-11 17:52:32+00:00
guid: http://www.net-liard.com/blog/?p=821
id: 821
permalink: /2011/03/peut-on-reussir-un-forfait/
tags:
  - Agile
  - forfait
  - prestation
title: Peut-on réussir un forfait ?
url: /2011/03/11/peut-on-reussir-un-forfait/
---

Plus je travaille avec des SSII et plus je trouve que les projets gérés au forfait se passent mal. Les torts sont souvent partagés, mais je constate plusieurs causes d&#8217;échec :

### Le client est incapable de rédiger un cahier des charges

Là je sais de quoi je parle, j&#8217;ai souvent le rôle de client en ce moment <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

Le besoin évolue, n&#8217;est pas forcément clair et donc il est très dur de rédiger un cahier des charges exhaustif. Le client est obsédé par la garantie de réalisation qu&#8217;apporte le forfait, alors qu&#8217;il est incapable d&#8217;exprimer correctement son besoin. Pire je vois de plus en plus de forfait où on demande au prestataire de rédiger le cahier des charges : on rêve.

### Les acheteurs : price killer

Oui c&#8217;est une bonne chose de tirer les prix vers le bas, mais il faut aussi rester raisonnable. Comment voulez-vous travailler sereinement avec des prestataires à qui on a mis le couteau sous la gorge.  Pourquoi pas des enchères inversées pendant qu&#8217;on y est ? -souvenir-

### Le réflexe &#8220;perdant &#8211; perdant&#8221;

J&#8217;ai l&#8217;impression d&#8217;être le seul à demander aux SSII d&#8217;augmenter leur chiffrage quand j&#8217;ai l&#8217;impression que c&#8217;est un peu juste. Une fois j&#8217;en parlais à un chef de projet, il m&#8217;a même répondu : &#8220;Ne leur dis rien, s&#8217;ils se plantent c&#8217;est pour leur pomme !&#8221;. On sait très bien que ça ne se passe pas comme cela. A un moment si le prestataire s&#8217;est vraiment planté, c&#8217;est le projet qui va en pâtir (qualité de code, test unitaire, bug..)

### L&#8217;inter-contrat

Même si les commerciaux sont les spécialistes pour vous faire de beaux discours sur leur &#8220;cellule forfait&#8221; avec des personnes dédiées. Il ne faut pas se leurrer, le forfait c&#8217;est l&#8217;idéal pour occuper une personne en inter-contrat. Le problème pour le projet c&#8217;est que l&#8217;on n&#8217;a jamais les mêmes développeurs en face. C&#8217;est dur d&#8217;assurer une continuité des développements.

### Junior en solo

C&#8217;est un peu lié au problème des prix tirés vers le bas mais je vois de plus en plus de débutants seuls sur des projets. J&#8217;ai absolument rien contre les débutants mais il faut les encadrer. Le problème c&#8217;est qu&#8217;en SSII des développeurs avec 10 ans d&#8217;expérience c&#8217;est super rare. Et oui, on vend plus cher un mauvais chef de projet qu&#8217;un bon développeur avec de l&#8217;expérience.

### Le Mythe du forfait de service

Depuis un certain temps on nous a mis en place des &#8220;forfaits de services&#8221;. Alors ça c&#8217;est encore une belle invention d&#8217;acheteur qui n&#8217;a pas du travailler dans le monde du développement. En gros le principe c&#8217;est d&#8217;envoyer une demande par email et d&#8217;attendre le livrable 2 mois plus tard. Vous ne savez pas qui travaille sur le projet, c&#8217;est une boite noire. Et donc on retombe dans les travers des deux précédents points et on va avoir des développeurs Flex juniors qui vont coder du J2EE.

## Des solutions ?

Je sors justement d&#8217;une expérience forfait un peu difficile. A la signature du contrat tout est beau, c&#8217;est une société avec qui je travaille souvent, ils mettent en avant le fait qu&#8217;il sont CMMI niveau 3, on parle même d&#8217;intégration continue avec Hudson. Bref on est en confiance. Au final on nous livre du code Java d&#8217;une qualité affligeante (si si c&#8217;est le bon mot quand je trouve des noms de variable avec des accents), zéro test unitaire et cerise sur le gâteau le livrable ne compile pas car il manque des sources.

Malgré tout ça je vais continuer à travailler avec cette société. Car déjà elle n&#8217;est pas la seule responsable de cet &#8220;échec&#8221; mais surtout je pense que c&#8217;est avant tout un problème de mauvaise personne au mauvais endroit.

Mais comment faire en sorte que la future prestation se passe bien :

### Travailler gagnant &#8211; gagnant

Partager les risques avec le prestataire, s&#8217;impliquer dans le chiffrage, travailler ensemble.

### Choisir les intervenants

Il faut vraiment intégrer que la réussite d&#8217;un projet n&#8217;est pas lié à la société mais bien aux personnes qui réalisent. Faire passer des entretiens est donc primordial pour sélectionner son équipe. C&#8217;est le seul moyen d&#8217;être sûr que l&#8217;on va pas mettre un Flexeur à gérer des transactions JTA ( oui oui c&#8217;est du vécu&#8230;).

### Faire des revues de code périodiquement

Les chefs de projets qui regardent la qualité du code livré sont rares, mais le faire à la livraison c&#8217;est surtout trop tard. Il est très important de bien suivre la qualité du code tout au long de la vie du projet pour s&#8217;assurer que ça ne diverge pas.

Et non coder un &#8220;proto&#8221; n&#8217;autorise pas à faire n&#8217;importe quoi ! (si je retrouve le gars qui a codé la gestion des transactions à la main dans un filtre HTTP je l&#8217;étripe <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

## Conclusion

C&#8217;est bête à dire mais pour réussir il faut juste travailler en bonne intelligence avec le prestataire. Arrêter ce rapport maitre/esclave qui ne peut que mal finir et discuter d&#8217;égal à égal.

Le client devrait passer plus de temps sur son expression de besoins que sur les petites lignes du contrat cadre. Arrêtez d&#8217;être obsédé par la garantie de résultat et de date de livraison complètement illusoire pour vous reconcentrer sur l&#8217;essentiel : le produit.

Le développement agile permet de résoudre beaucoup de problèmes. Mais quand je vois que l&#8217;on demande à des prestataires de travailler de façon Agile mais en gardant un cadre type forfait avec engagement de résultat, c&#8217;est complètement antinomique !