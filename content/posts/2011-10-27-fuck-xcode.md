---
author: Samuel
categories:
  - iPhone
date: 2011-10-27 21:55:58+00:00
guid: http://www.net-liard.com/blog/?p=1055
id: 1055
permalink: /2011/10/fuck-xcode/
tags:
  - armv6
  - iPhone
  - XCode
title: Fuck XCode !
url: /2011/10/27/fuck-xcode/
---

![photo](/images/uploads/2011/10/Logo_xcode1.jpg)
Oui le titre est vulgaire, mais ça fait du bien de se défouler! Dans le précedent post j&#8217;expliquais pourquoi j&#8217;avais abandonner PhoneGap pour faire mon application. J&#8217;étais alors loin d&#8217;imaginer la galère que ça allait être en natif avec XCode.

Notez que j&#8217;avais mis à jour mon XCode à la sortie de iOS 5 pour avoir la dernière version 4.2.

&nbsp;

Donc je me lance : &#8220;Fichier -> nouveau projet&#8221; et je tombe sur un nouveau type d&#8217;application &#8220;Page-Based Application&#8221;. Comme c&#8217;est exactement ce que je souhaite faire, je décide de le tester. A la fin de ma journée c&#8217;est plié mon application est terminée. Ca fonctionne sur le simulateur et sur mon iPhone mais juste avant de rentrer chez moi je relance rapidement un test mais avec le simulateur iOS 4.3 cette fois. Surprise, ça ne compile pas  <img src="http://www.apptom.fr/wp-includes/images/smilies/frownie.png" alt=":(" class="wp-smiley" style="height: 1em; max-height: 1em;" />Et oui la classe UIPageViewController n&#8217;existe qu&#8217;à partir de iOS 5. Ok, je poubellise ma journée..

Le lendemain je recommence un projet &#8220;Single View Application&#8221; et on me propose une option &#8220;Use storyBoard&#8221;. Ok pourquoi pas, ça a l&#8217;air plus simple de gérer ses XIB avec un storyBoard. Et donc après une demie journée de travail je termine de nouveau mon application. Et de nouveau ça ne fonctionne pas sur iOS 4.3. J&#8217;ai mis plus de temps avant de comprendre que ça venait des storyboards compatibles uniquement iOS 5. Quelqu&#8217;un peut m&#8217;expliquer pourquoi une nouvelle représentation graphique des vues ne pourrait pas générer du binaire compatible iOS 3 ??

Donc merci Apple pour toutes ces nouveautés d&#8217;XCode 4.2, vraiment merci ! J&#8217;ai hâte de pouvoir les utiliser dans 3 ou 4 ans lorsque nos clients sauront tous au moins sur iOS 5. Car aujourd&#8217;hui nous avons encore beaucoup de clients avec des iPhones 3G qui ne passeront donc jamais sur iOS 5. Et je ne parle même pas de ceux qui ne mettent jamais leur iPhone à jour.

Sortir aujourd&#8217;hui une application uniquement compatible iOS 5 c&#8217;est juste stupide !

Bref ! J&#8217;ai donc recodé mes vues avec de beaux XIB et enfin mon application fonctionnait sous iOS 3 et 4. Miracle !! Je la passe donc à notre équipe de validation. 10 minutes plus tard j&#8217;ai un email &#8220;impossible de l&#8217;installer sur mon iPhone 3G sous iOS4.1&#8221;. Mince je l&#8217;ai pourtant testée sur un 3GS avec le même OS. Donc je me balade de bureau en bureau pour enfin trouver un iPhone 3G : en effet, impossible de l&#8217;installer. Après des recherches sur le net je trouve ([sur ce site](http://stackoverflow.com/questions/4198676/warning-iphone-apps-should-include-an-armv6-architecture-even-with-build-config)) les options de compilations à ajouter. Car à partir de l&#8217;iPhone 3GS l&#8217;architecture est basée sur du armv7 alors que l&#8217;iPhone 3G est armv6.

Là c&#8217;est clair Apple a définitivement oublié l&#8217;iPhone 3G. Par défaut votre application ne fonctionnera pas sur ce terminal.

Avec ces options j&#8217;arrive enfin à installer l&#8217;application sur un iPhone 3G ! Mais resurprise : elle se lance mais ne fonctionne pas correctement. Mes 3 vues qui étaient côte à côte dans une UIScrollView se superposent. A ne rien y comprendre. Après une longue soirée à débugguer j&#8217;ai trouvé une solution en modifiant mon code :

<pre>if ([device isEqualToString:IPHONE_3G]) {
    frame.origin.x = 0;
    frame.origin.y = frame.size.width * i;
} else {
    frame.origin.x = frame.size.width * i;
    frame.origin.y = 0;
}</pre>

Ne me demandez pas pourquoi, mais sur le 3G l&#8217;axe des X et l&#8217;axe des Y de ma ScrollView sont inversés. Je ne cherche même plus à comprendre à ce niveau&#8230;

Je retourne donc une nouvelle version pour validation et j&#8217;ai comme retour :

  * 3G ios 4.2.1<span style="color: #00ff00;"><span style="color: #000000;"> -> </span>OK</span>
  * 3G ios 4.0.2 -> <span style="color: #ff0000;">KO</span>
  * <span style="color: #ff0000;"><span style="color: #000000;">3G ios 3.1.3 -></span> KO</span>
  * <span style="color: #00ff00;"><span style="color: #000000;">3GS ios 3.1.3 -></span> OK</span>

Je tente donc un dernier changement au niveau de ma compilation. XCode 4.2 utilise par défaut le compilateur &#8221; Apple LLVM compiler 3.0&#8243;. Je passe donc en &#8220;LLVM GCC 4.2&#8221;

  * 3G ios 4.2.1 = <span style="color: #00ff00;">installation OK,</span> et <span style="color: #00ff00;">icône OK</span>
  * 3G ios 4.0.2 = <span style="color: #00ff00;">installation OK</span>, mais <span style="color: #ff0000;">icône KO</span>
  * 3G ios 3.1.3 = <span style="color: #ff0000;">installation KO</span>

C&#8217;est un peu mieux et cette fois j&#8217;abandonne, je vais en rester là.

Moralité de l&#8217;histoire : réfléchissez avant de passer sur XCode 4.2. C&#8217;est beaucoup de problèmes et les nouveautés sont juste inutilisables pour le moment.

Et oui il y a des semaines comme ça où : **FUCK XCODE** !