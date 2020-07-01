---
author: Samuel
categories:
  - Cloud
date: 2013-05-30 21:50:22+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.apptom.fr/?p=1531
id: 1531
permalink: /2013/05/premiers-tests-de-google-app-engine-en-php/
tags:
  - cloud
  - codeigniter
  - GAE
  - php
title: Premiers tests de Google App Engine en PHP
url: /2013/05/30/premiers-tests-de-google-app-engine-en-php/
---

C&#8217;est une des grosses annonces de la Google I/O 2013, Google App Engine supporte maintenant PHP. J&#8217;ai eu l&#8217;occasion de le tester sur un de mes projets. La première chose qu&#8217;il faut constater, c&#8217;est que l&#8217;utilisation du service en PHP n&#8217;est pas vraiment ouverte. Pour le moment il faut passer par une phase de validation de son projet pour avoir le droit d&#8217;utiliser le service. On est maintenant à 2 semaines de l&#8217;annonce et seulement 282 projets on été acceptés.

## Configuration

Qui dit PHP dit LAMP et donc mysql. Google a justement ouvert une offre Cloud SQL. Nous ne sommes plus limités à leur DataStore NoSql sur GAE (c&#8217;était déjà le cas depuis plusieurs mois). Par contre la facturation du service Cloud SQL se fait à l&#8217;heure alors que le DataStore facture à l&#8217;usage (nombre de read/write). C&#8217;est moins économique pour un petit projet mais plus facilement prédictif. Pour la sauvegarde de fichier il faut utiliser Google Cloud Storage qui n&#8217;est ni plus ni moins une copie du service S3 d&#8217;Amazon. Les APIs sont même compatibles.
  
Pour utiliser l&#8217;ensemble de ces services la console GAE n&#8217;est plus suffisante, il faut utiliser la &#8220;Cloud Console&#8221;. Et c&#8217;est là que commence le parcours du combattant.

![SNS](/images/uploads/2013/05/Console.png)

<p style="text-align: left;">
  Sur mon projet, au moment de vouloir créer mon premier Bucket sur Cloud Storage on me demande d&#8217;activer le Billing. J&#8217;ai donc entré mes informations personnelles et mon numéro de carte bleue. Rien d&#8217;exceptionnel s&#8217;il ne fallait pas le faire pour chaque projet ! A chaque fois on me redemande la même chose. Pire il faut aussi activer le billing sur la console Google App Engine. Donc pour chaque projet on va avoir 2 lignes de facturation ? La semaine dernière j&#8217;ai eu un débit de 0.15 € sur mon compte et 0.40€ de frais bancaires. Si j&#8217;ai 10 lignes à moins de 1€ sur mon compte par semaine, c&#8217;est mon comptable qui va être content :( J&#8217;ai l&#8217;impression que l&#8217;on peut simplifier les choses en souscrivant à une offre de support Google. La moins chère est à 150€ par mois, dans mon cas ça attendra.
</p>

<p style="text-align: left;">
  Une fois le billing activé, impossible de créer un bucket sur Cloud Storage. J&#8217;ai le message :
</p>

> <p style="text-align: left;">
>   The account for the specified project has been disabled.
> </p>

<p style="text-align: left;">
  Et oui car il y a une seconde console où il faut activer le Cloud Storage pour pouvoir l&#8217;utiliser ! Bien sûr aucun lien direct vers cette console que j&#8217;ai trouvée grâce à StackOverflow : <a href="https://code.google.com/apis/console">https://code.google.com/apis/console</a>
</p>

<h2 style="text-align: left;">
  Le code
</h2>

<p style="text-align: left;">
  Une fois cette partie gestion terminée, je peux enfin commencer à tester mon service PHP sur GAE. C&#8217;est une petite application facebook codée avec le framework codeigniter. Premier problème, il ne trouve pas la fonction php_sapi_name. Par défaut, beaucoup de fonctions PHP sont désactivées sur GAE, mais il est possible de les réactiver en ajoutant un fichier php.ini à la racine de votre projet :
</p>

> <p style="text-align: left;">
>   google_app_engine.enable_functions = &#8220;phpversion, phpinfo, php_sapi_name&#8221;
> </p>

<p style="text-align: left;">
  Ensuite j&#8217;ai un problème avec la variable $_SERVER, il ne trouve pas l&#8217;élément SCRIPT_NAME. Comme ce n&#8217;est pas structurant pour mon application je l&#8217;ai juste retiré du code. La connexion à la base se passe sans problème. J&#8217;ai juste du mettre l&#8217;option db_debug à FALSE pour que ça fonctionne. Attention aussi par défaut il n&#8217;y a que l&#8217;utilisateur root sur votre base, c&#8217;est à vous de créer votre user (comme sur votre mysql en fait).
</p>

> $db[&#8216;hostname&#8217;] = &#8216;:/cloudsql/<project\_name>:<sql\_name>&#8217;;
  
> $db[&#8216;username&#8217;] = &#8216;login&#8217;;
  
> $db[&#8216;password&#8217;] = &#8216;pass&#8217;;
  
> $db[&#8216;database&#8217;] = &#8216;basename&#8217;;
  
> $db[&#8216;dbdriver&#8217;] = &#8216;mysql&#8217;;
  
> $db[&#8216;dbprefix&#8217;] = &#8221;;
  
> $db[&#8216;pconnect&#8217;] = TRUE;
  
> $db[&#8216;db_debug&#8217;] = FALSE;
  
> $db[&#8216;cache_on&#8217;] = FALSE;
  
> $db[&#8216;cachedir&#8217;] = &#8221;;
  
> $db[&#8216;char_set&#8217;] = &#8216;utf8&#8217;;
  
> $db[&#8216;dbcollat&#8217;] = &#8216;utf8\_general\_ci&#8217;;
  
> $db[&#8216;swap_pre&#8217;] = &#8221;;
  
> $db[&#8216;autoinit&#8217;] = TRUE;
  
> $db[&#8216;stricton&#8217;] = FALSE;

Donc avec très peu de modifications mon application PHP tourne sur GAE. Il me reste à regarder le stockage sur Cloud Storage. La documentation est succinte mais nous avons les éléments pour le faire. Mes premiers tests n&#8217;étaient pas très concluants, j&#8217;avais un retour d&#8217;erreur sur l&#8217;adresse d&#8217;upload :

> 503 Service Unavailable

Et c&#8217;est à ce moment qu&#8217;il faut comprendre que &#8220;Service Unavailable&#8221; veut dire : &#8220;vous n&#8217;avez pas les bons droits d&#8217;accès&#8221;. Après avoir ajouté des droits d&#8217;accès sur le bucket l&#8217;upload de fichier fonctionne. La documentation est vraiment très pauvre quand même. Certaines fonctions php son implementées (comme unlink) et d&#8217;autre pas (pas de rename). Il y a un vrai manque de documentation pour utiliser Cloud Storage en PHP, il nous faut vraiment le même niveau de doc que ce qui est proposé en Python. J&#8217;ai aussi remonté un bug sur la méthode move\_uploaded\_file, pour le moment on perd l&#8217;info sur le type du fichier à la copie. C&#8217;est gênant surtout qu&#8217;aucune documentation ne nous dit comment modifier les metadata d&#8217;un fichier. Le [ticket](https://code.google.com/p/googleappengine/issues/detail?id=9407) a été validé par google.

Comme je l&#8217;ai dit au début, l&#8217;objectif est de réaliser une application FaceBook, il faut donc avoir un service disponible en HTTPS. Là rien de très compliqué techniquement, il faut utiliser la console de gestion de domaine (oui une quatrième console !). Ce tuto explique très bien les différentes étapes d&#8217;installation. Par contre j&#8217;ai eu la surprise de découvrir qu&#8217;il fallait payer 9$ par mois pour pouvoir ajouter un certificat SSL (en plus du prix du certificat bien sûr).

Une fois que l&#8217;ensemble fonctionne, on peut se concentrer sur le point important : Les temps de réponse. Est-ce que le gros problème de temps de démarrage d&#8217;instance Java que j&#8217;ai décrit [ici](/2012/07/google-app-engine-suite/) il y a 1 an (toujours d&#8217;actualité  :() se retrouve aussi en PHP ? La réponse est mitigée. Oui c&#8217;est plus rapide, on est souvent autour d&#8217;une seconde pour démarrer une nouvelle instance. Par contre il faut 6,5s pour uploader un fichier de 300ko ! Quand je dis uploader, je compte l&#8217;ensemble du traitement comme il est noté dans la doc à savoir : upload + move\_uploaded\_file + unlink du fichier temp. C&#8217;est vraiment l&#8217;upload qui est long puisque je descends à 5,5s de temps d&#8217;exécution si je retire move\_uploaded\_file et unlink. Cette lenteur est complètement bloquante dans certains cas et difficilement explicable.

## Conclusion

La bonne nouvelle est que j&#8217;ai pu installer une application PHP existante assez rapidement sur GAE. Je n&#8217;ai dû recoder que la partie upload de fichiers. Par contre l&#8217;offre Cloud de Google reste encore un peu lourde. On voit bien que  c&#8217;est le début et que tout n&#8217;est pas encore intégré. Le fait d&#8217;avoir 4 consoles différentes montre qu&#8217;il y a encore du travail :

  * Console GAE : les logs, la gestion des versions, du billing
  * Cloud Console : Gestion de Cloud SQL, Cloud Storage
  * Console API : Pour activer les services visibles dans la Cloud Console
  * Domain manager : Gestion des domaines et donc des certificats SSL pour GAE

On est donc loin de la maturité d&#8217;Amazon mais l&#8217;offre est intéressante. Elle a au moins eu l&#8217;avantage d&#8217;ouvrir une guerre des prix entre les 2 géants :)

**Points positifs :**

  * Scalable à l&#8217;infini
  * Codeigniter fonctionne dessus
  * Coût proche de zéro en début de projet

**Points négatifs :**

  * Documentation très pauvre
  * Encore des lenteurs
  * 4 consoles c&#8217;est 3 de trop
  * Environnement de dev plus complexe qu&#8217;un simple LAMP