---
author: Samuel
categories:
  - Cloud
date: 2012-06-19 22:07:32+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.net-liard.com/blog/?p=1225
id: 1225
permalink: /2012/06/developper-sur-google-app-engine/
tags:
  - cloud
  - Cloud Computing
  - GAE
  - Google
  - Google App Engine
title: Développer sur Google App Engine
url: /2012/06/19/developper-sur-google-app-engine/
wp_plus_one_redirect:
  - null
---

Depuis 1 mois je teste le déploiement de services sur Google App Engine. Le moins que l&#8217;on puisse dire c&#8217;est que c&#8217;est loin d&#8217;être aussi simple que ce que j&#8217;avais vu pendant la Devoxx France. Je vous propose un petit tour sur ce que j&#8217;ai remarqué.

## Le Data Store

Même si Google propose une base SQL en version Beta, j&#8217;ai utilisé le datastore No SQL par défaut. Pour simplifier la gestion de la persistance, la librairie [Objectify](http://code.google.com/p/objectify-appengine/) est très bien adaptée. La première chose à faire est de bien identifier les champs à indexer. Par défaut un paramètre est indexé, mais plus il y a d&#8217;index plus le coût d&#8217;écriture est important.

Attention aussi à la notion d&#8217;objet embeded. On ne peut le faire qu&#8217;à un niveau. Donc une classe embeded ne peut pas avoir d&#8217;attribut List.

Mais la plus grosse surprise que j&#8217;ai eue c&#8217;est que l&#8217;écriture se fait de façon asynchrone. Après avoir persisté un objet il faut attendre 5-6s pour pouvoir le lire en base. Il faut donc ruser et utiliser des caches pour masquer ce délai.

## Le Blobstore

C&#8217;est une des fonctions intéressantes du service. Elle permet de stocker facilement des fichiers, des images par exemple. Et pour les images justement il y a même une astuce pour les redimensionner.

<pre class="nogutter:nocontrols">// Resize the image to 32 pixels (aspect-ratio preserved)
http://<em>your_app_id</em>.appspot.com/randomStringImageId<strong>=s32</strong>
// Crop the image to 32 pixels
http://<em>your_app_id</em>.appspot.com/randomStringImageId=s32<strong>-c</strong></pre>

Pour trouver de l&#8217;information sur cette fonction, il faut lire la version Anglaise de la doc. En effet au début on apprécie le fait que toute la doc de Google App Engine ait été traduite en Français. On déchante vite lorsqu&#8217;on s&#8217;aperçoit que cette dernière n&#8217;est pas au même niveau que la version anglaise. Donc n&#8217;oubliez pas de lire la VO <img src="http://www.apptom.fr/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

Pour revenir au BlobStore, j&#8217;ai eu un problème pour gérer les fichiers non renseignés dans un formulaire. Sur un formulaire où l&#8217;utilisateur peut éventuellement uploader 1 fichier, un blobstore vide est créé s&#8217;il n&#8217;y a pas de fichier.

Ce comportement est d&#8217;autant plus étrange qu&#8217;on ne le retrouve pas sur le serveur local en mode dev. Une autre leçon à retenir : tester au plus tôt en production votre code.

Pour résoudre le problème, il faut tester la taille du fichier uploadé pour ensuite le supprimer s&#8217;il est vide.

<pre class="java:nogutter:nocontrols">if (blobs.get("uploadFile") != null) {
 BlobKey blobKey = blobs.get("uploadFile").get(0);
 BlobInfo blobInfo = new BlobInfoFactory().loadBlobInfo(blobKey);
 if (blobInfo.getSize() &gt; 0) {
  uploadFileUrl = imagesService.getServingUrl(blobKey);
 } else {
  blobstoreService.delete(blobKey);
 }
}</pre>

## A suivre

Je termine là mes remarques sur la partie purement dev de Google App Engine. Mais j&#8217;ai eu d&#8217;autres surprises que je vous détaillerai prochainement.