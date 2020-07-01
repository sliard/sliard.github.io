---
author: Samuel
categories:
  - iPhone
date: 2010-01-08 12:00:59+00:00
guid: http://www.net-liard.com/blog/?p=532
id: 532
permalink: /2010/01/etape-3-publier-lapplication/
tags:
  - Apple
  - iPhone
title: "Etape 3 : publier l'application"
url: /2010/01/08/etape-3-publier-lapplication/
---

Voilà, j&#8217;ai une application qui fonctionne, un beau site web, il est temps de passer à la phase importante : publier l&#8217;application.

Dans un premier temps il faut rejoindre le &#8220;iPhone developer programme&#8221; pour obtenir un certificat Apple.

C&#8217;est ce certificat qui vous permet aussi de tester l&#8217;application sur un vrai iPhone. Avant de payer vous avez accès au SDK et au simulateur iPhone. Le SDK est gratuit, mais ne fonctionne que sur Mac bien-sûr.

J&#8217;ai donc payé 79 Euros pour avoir le droit pendant 1 an de développer sur iPhone. Une fois la commande passée il faut compter maxi 24 heures pour que votre compte soit activé.

Une fois dans le programme vous avez accès à un site web où vous pouvez déclarer vos applications et les UDID de vos iPhones de tests. C&#8217;est assez complet mais Apple fournit une très bonne documentation, je ne vais donc pas ré-expliquer la démarche en détail.

J&#8217;ai mis un peu de temps au début pour déclarer mon certificat de développement. Les échanges de clé publique/clé privée c&#8217;est un peu long. Pour la petite histoire j&#8217;ai cherché longtemps l&#8217;application &#8220;Keychain&#8221; sur mon Mac. Et oui sur un Mac français l&#8217;application se nomme &#8220;Trousseau d&#8217;accès&#8221;.

Une fois le certificat bien installé, mon application déclarée et la configuration d&#8217;un fichier de provisionning faite, j&#8217;ai pu tester iMovies Collection sur mon iPhone.

Passons maintenant aux choses sérieuses, la déclaration dans l&#8217;appStore.

Déjà il faut créer un nouveau certificat et un provisionning spécifique pour l&#8217;application à diffuser.

Ensuite on passe sur une nouvelle interface : iTunes Connect. C&#8217;est dans celle-ci que l&#8217;on propose nos applications pour diffusion.

Première chose importante : **Attention à votre première déclaration !**

En effet au moment de proposer votre première application on vous demande le langage principal et le nom de l&#8217;auteur. Une fois validé c&#8217;est définitif ! Ces informations seront utilisées pour toutes vos applications.

Par exemple j&#8217;ai fait l&#8217;erreur de choisir French comme langue de base. Et bien je dois copier / coller la description de mon application en Anglais dans toutes les langues gérées par Apple&#8230; Si j&#8217;avais déclaré Anglais comme langue de base je n&#8217;aurais eu qu&#8217;à définir une description spécifique en Français.

Bref j&#8217;ai du remplir 16 formulaires :

  * English
  * Dutch
  * Australian English
  * Canadian English
  * UK English
  * German
  * Italian
  * Japanese
  * Korean
  * Portuguese
  * Russian
  * Simplified Chinese
  * Spanish
  * Mexican
  * Spanish
  * Swedish
  * Brazilian
  * Portuguese

Attention aussi à la case &#8220;Keywords&#8221;, une fois le formulaire validé et même si vous n&#8217;avez pas encore uploadé votre binaire, il n&#8217;est plus possible de les changer avec une nouvelle livraison. Sur les autres langues vous pouvez mais pas sur la langue principale. C&#8217;est quand même étonnant pour un site Apple, marque connue et reconnue pour son ergonomie. Au niveau du site iTunes Connect je trouve ça très moyen.

Sinon pour le reste de la déclaration rien de bien compliqué, là aussi c&#8217;est bien documenté.

Comme j&#8217;ai décidé de vendre 1$ l&#8217;application je dois remplir des informations sur mon compte bancaire. J&#8217;ai perdu beaucoup de temps pour trouver le bon formulaire. En fait je l&#8217;avais trouvé dès le début mais mon navigateur Google Chrome ne savait pas le gérer. Une fois passé sur Safari, je n&#8217;ai plus eu de problème.

Voilà c&#8217;est fait, mon application est en cours de validation. Histoire à suivre donc <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />