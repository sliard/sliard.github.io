---
author: Samuel
categories:
  - Non classé
date: 2012-04-23 10:14:58+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.net-liard.com/blog/?p=1187
id: 1187
permalink: /2012/04/devoxx-france/
title: Devoxx France
url: /2012/04/23/devoxx-france/
wp_plus_one_redirect:
  - null
---

La première édition de Devoxx France a eu lieu les 18, 19 et 20 avril 2012. Un grand rassemblement de développeurs français (essentiellement) et donc beaucoup de geeks !

Sans vous refaire toutes les conférences en détail (il y aura des vidéos sur [parleys](http://www.parleys.com/) pour ça) revenons sur ce que j&#8217;ai vu et l&#8217;ambiance générale.

## Mercredi

Venant de province (Lannion), réveil à 5h30 pour prendre l&#8217;avion et arriver juste avant 9h à l&#8217;hôtel Marriott. Le checking est rapide et sans pb. On entre ensuite dans le vive du sujet, 3 heures de conférence ou de labs. En effet la première journée est taggée &#8220;University&#8221;. Le principe est de prendre du temps pour approfondir un sujet technique. C&#8217;est vrai qu&#8217;avec 3 heures on entre plus dans le détail que pendant des présentations de 50 minutes.

#### Google App Engine

L&#8217;objectif de cette session est de réaliser un site web pour annoncer les résultats de l&#8217;élection présidentielle. Donc de prouver la capacité de monter en charge de Google App Engine. Parmi les ingénieurs Google présents il y avait [Ludovic Champenois](http://twitter.com/#/ludoch). Il développe la plateforme, donc forcément il la maitrise <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

Google App Engine utilise les mêmes data center que ceux utilisés par le fameux moteur de recherche pour héberger vos applications. La présentation commence donc par un avertissement amusant :

> Faites attention, on va forcément arriver à absorber votre trafic.

L&#8217;avertissement est en fait par rapport à la facturation. En effet la charge n&#8217;est pas un problème, vous pouvez avoir des pics de charges énormes google va les absorber&#8230; Mais après il va falloir payer. Les quotas d&#8217;utilisation sont journaliers et il est donc très fortement conseillé de mettre une limite en $ par jour en fonction de votre budget.

Cette session est animée sous forme de TP. Vous pouvez retrouver le code [ici](http://code.google.com/p/devoxx-france-appengine/).

J&#8217;aime vraiment utiliser Google App Engine. Pour un développeur Java c&#8217;est très simple. Le gros problème c&#8217;est l&#8217;impossibilité d&#8217;estimer le coût de la solution pour une application pro. Il y a tellement de paramètre qui rentre en compte que l&#8217;on ne peut pas vraiment le faire précisément.

#### Developing, Deploying and Scaling in the Cloud with Play par James Ward, Nicolas Leroux et Guillaume Bort

En fait j&#8217;avais commencé à la présentation CDI, mais je n&#8217;ai vraiment pas accroché au début avec l&#8217;explication des échanges OAuth. J&#8217;ai donc rapidement migré sur Play.

J&#8217;ai trouvé ça intéressant mais assez superficiel. Le problème c&#8217;est que j&#8217;ai déjà un peu testé play et donc cette présentation qui a déroulé le tutoriel de base ne m&#8217;a rien appris.

A partir de 17h ont commencé les présentations &#8220;Tool in action&#8221;. Ce sont des sessions de 30 minutes pour présenter un outil. J&#8217;ai participé à deux sessions :

  * Tester une application Web avec Selenium 2, Selenium Grid et TestNG
  * Continuous deployement : Rackspace, Chef et capistrano en action

Une demi-heure c&#8217;est vraiment court. On a juste le temps de comprendre à quoi sert l&#8217;outil. Je ne suis pas super fan de ce concept.

Ensuite il y avait des BOF (Birds-of-a-Feather). Ce sont des rencontres informelles de passionés autour d&#8217;un sujet. Des sessions jusqu&#8217;à 21h. Mais pour moi réveillé depuis 5h30 et avec 450 Km de trajet dans les pattes, dès 18h j&#8217;en avais plein la tête, je n&#8217;ai donc pas participé à ces &#8220;BOF&#8221;.

## Jeudi

On commence donc par une keynote dans une salle immense. Après une petite intro expliquant la génèse du projet Devoxx France, nous avons droit à 2 belles présentations.

#### Fier d&#8217;être développeur ? par Pierre Pezziardi

Co-fondateur d’OCTO Technology Pierre Pezziardi a une très belle vision du métier de développeur et nous parle de notre problème à faire partager notre passion. Sa réponse est simple : Arrêtez de vous plaindre que le développement est un métier dévalorisé et changez déjà votre propre façon de penser avant de demander aux autres de changer la leur.

Pour cela il nous présente le &#8220;egoless programming manifesto&#8221;. 1o règles que l&#8217;on peut traduire comme cela :

  1. Comprendre et accepter que l&#8217;on fait des erreurs
  2. Vous n&#8217;êtes pas votre code
  3. Peut-importe votre niveau de kung fu, quelqu&#8217;un est meilleur
  4. Ne pas réécrire le code d&#8217;un autre développeur sans concertation
  5. Traitez les personnes qui en connaissent moins que vous avec respect et patience
  6. La seule constante dans le monde c&#8217;est le changement
  7. La seule autorité réelle découle de la connaissance, pas de la hiérarchie
  8. Battez vous pour vos convictions mais pitié acceptez la défaite
  9. Ne soyez pas &#8220;le gars dans le bureau&#8221;
 10. Critiquez le code pas le codeur. Soyez tolérant avec le codeur et sans pitié avec le code

Des règles à respecter dans tout bon open space qui se respecte ! <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

#### This could be Heaven or this could be Hell by Ben Evans and Martijn Verburg

Style complètement différent mais présentation très bien faite. On a eu droit à un vrai show sur comment peut évoluer le monde java dans les prochaines années.

On enchaine sur les conférences.

#### ElasticSearch par David Pilato

ElasticSearch est une plateforme utilisable pour indexer de gros volumes de données et expose une interface REST pour requêter. C&#8217;est super puissant et très scalable car il gère des mécanismes de réplication et de clustering. Le seule chose qu&#8217;il faut bien comprendre c&#8217;est que les données indexées sont stockées par ElasticSearch. Donc indexer un gros volume de twitter c&#8217;est bien, mais il faut ensuite assurer au niveau de l&#8217;espace disque.

#### Nouveau look pour une nouvelle vie: Spring, JQuery et HTML5 par Julien Dubois

Bon là, rien de vraiment nouveau pour moi, mais j&#8217;étais curieux de voir ce que donnait le projet [Tatami](http://blog.ippon.fr/2012/04/11/resultat-du-concours-tatami-pour-devoxx-france/) de Ippon et j&#8217;aime bien les présentations de Julien. Ce qu&#8217;il faut savoir c&#8217;est que spring n&#8217;a pas vraiment la cote à Devoxx. D&#8217;ailleurs la conf de Julien n&#8217;avait pas été retenue au &#8220;Call for paper&#8221;. Mais comme Ippon est sponsor Julien a habilement utilisé leur slot partenaire pour la faire.

A la fin de la présentation il lance donc un test de charge comparatif entre son service Tatami (Jquery, Spring, Casandra avec persistance sur disque) contre le service démo de Play utilisant une base de données en mémoire. Et là c&#8217;est le drame  <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />Julien explose le score avec Spring alors que Play plante sous la charge. Je peux vous assurer qu&#8217;il ne s&#8217;est pas fait que des copains dans la salle.

#### Programmation concurrente en Java dans la pratique par Alex Snaps

Une bonne présentation des différents moyens de faire du code thead safe et comment c&#8217;est mis en place dans l&#8217;implémentation de EhCache. Ca a été pour moi une bonne piqure de rappel.

#### Pour une fois soyons physiques ! Une introduction à Arduino par David Delabassee

Depuis le temps que j&#8217;entends parler de arduino j&#8217;ai enfin pu voir à quoi ça ressemblait. Enfin un peu de matériel ça fait du bien. Passer de Google App Engine où on parle d&#8217;espace disque en Téra à Arduino avec un processeur 8 bits et 16k de mémoire c&#8217;est un peu le grand écart <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

Arduino est une petite plaque avec un micro controller et des connecteurs d&#8217;entrée/sortie. Ensuite en fonction des constructeurs et du niveau de gamme il y a plus ou moins de mémoire, d&#8217;adaptateurs (USB, RJ45 ou autre). Pour étendre les possibilités il faut ajouter des &#8220;Shields&#8221;. Un Shield est une extension spécifique avec par exemple un écran LCD ou des relais pour contrôler des appareils 220V.

A savoir aussi que le fameux Hello Word en arduino consiste à allumer une LED <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

#### Cloud et PaaS: les développeurs reprennent le pouvoir par Sacha Labourey

Sacha est CEO de CloudBees, il nous a présenté sa vision du cloud. Pour lui les développeurs ne devraient se préoccuper uniquement du code et laisser la gestion de l&#8217;IT à des pros : les fournisseurs PAAS.

## Vendredi

On commence la dernière matinée par trois Keynotes. La première d&#8217;IBM était atroce, des slides illisibles avec une tonne d&#8217;informations inintéressantes et un speaker &#8220;mou du slip&#8221;. 30 minutes de perdues. Ca pestait tellement sur twitter que les organisateurs n&#8217;ont pas affiché de tweet wall après son passage. Heureusement les 2 autres présentations étaient vraiment de haut niveau.

Patrick Chanezon de VMWare nous a retracé le parcours assez classique d&#8217;un développeur en France pour bien mettre en avant qu&#8217;il est vital dans notre metier de bien suivre [l&#8217;évolution des technos](http://www.slideshare.net/chanezon/devoxx-france-2012-portrait-du-developeur-en-the-artist).

Neal Ford nous a ensuite fait une présentation très dynamique sur comment on se laisse distraire par des abstractions en oubliant l&#8217;essentiel.

#### sizeOf en Java — parce que la taille… ça compte! par Alex Snaps

Encore une petite piqûre de rappel sur comment la JVM gère la mémoire. Alex Snaps travaille chez Terracotta sur EhCache donc la gestion du HEAP c&#8217;est son dada !

Après le repas il y avait une session sur JavaFX. J&#8217;ai d&#8217;abord pensé à une bonne blague des organisateurs, mais non ! Je n&#8217;y suis pas allé car j&#8217;avais déjà eu une démo à une conf en Floride en 2008. A mon avis ça n&#8217;a pas évoluer <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

A la place j&#8217;ai fait 2 autres sessions

  * Changeons la conception de nos applications grâce aux services Cloud par Cyrille Le clerc
  * Java sur Amazon Web Services par Carlos Conde

Je suis un peu déçu, je pensais que l&#8217;on allait rentrer un peu plus dans des problèmes spécifiques au développement pour du cloud, mais on a juste eu une énumération des différents services disponibles.

La dernière conférence sur Google App Engine a été plus intéressante même si j&#8217;avais déjà eu la plupart des infos lors du TP mercredi matin.

## Conclusion

J&#8217;ai vraiment passé 3 très bonnes journées. C&#8217;est toujours enrichissant d&#8217;écouter ce type de conférence, de rencontrer les spécialistes de leur domaine.

Bien sûr, on peut noter quelques points négatifs (des axes d&#8217;amélioration disent les RH  <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />). L&#8217;organisation a été un peu victime de son succès. Il était difficile de se déplacer autour des stands tellement il y avait de monde. J&#8217;ai aussi trouvé le programme très chargé. J&#8217;ai rarement vu des conférences finir après 17h un vendredi. C&#8217;est aussi sur ces détails que l&#8217;on ressent le côté très parisien des organisateurs. Ca peut être sympa de penser aux personnes qui ont 4-5 heures de train pour rentrer chez eux. Personnellement j&#8217;ai loupé les deux dernières conf pour pouvoir prendre mon avion.

Mais à part ça je tire mon chapeau aux organisateurs. Pour avoir participé à quelques conférences aux USA j&#8217;ai retrouvé exactement le même niveau de prestation. Jamais je n&#8217;avais vu une conférence comme celle-ci en France (bon ok, je ne les fais pas toutes non plus&#8230;). Merci aux organisateurs et bonne chance pour l&#8217;organisation de devoxx 2013 !