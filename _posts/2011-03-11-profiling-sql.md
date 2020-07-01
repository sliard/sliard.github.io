---
author: Samuel
categories:
  - Java
date: 2011-03-11 00:04:54+00:00
guid: http://www.net-liard.com/blog/?p=806
id: 806
permalink: /2011/03/profiling-sql/
tags:
  - ironsql
  - Java
  - p6spy
title: Profiling SQL
url: /2011/03/11/profiling-sql/
---

C&#8217;est une étape souvent négligée par les projets utilisant des librairies de mapping objet. Mais faire de l&#8217;Hibernate c&#8217;est bien, regarder les requêtes générées sur la base c&#8217;est mieux.

J&#8217;ai le souvenir d&#8217;un vieux projet utilisant des EJB Entity 2 où à un moment on ajoutait un objet dans une liste. En regardant les requêtes on s&#8217;est aperçu que le conteneur chargeait toute la liste avant de faire l&#8217;insert. C&#8217;était complètement inutile.

Donc comment étudier correctement les requêtes ? Déjà si vous utilisez hibernate mettez la property &#8220;show_sql&#8221; à true de temps en temps. Après pour avoir plus d&#8217;informations j&#8217;utilise **p6spy** et **IronEye SQL**.

p6Spy est une librairie qui remplace votre driver de base de données. C&#8217;est en quelque sorte un driver proxy de BDD. IronEye apporte juste une vue graphique des informations récoltées par p6spy. Pour trouver de la doc c&#8217;est un peu dur [p6spy](https://p6spy.github.io/p6spy/2.0/install.html "Project Home"){.link-external} ne fonctionne plus mais j&#8217;ai trouvé un site expliquant la [mise en place de p6spy et de IronSql](http://www.javaperformancetuning.com/tools/ironeyesql/index.shtml).

Par contre ce sont deux outils un peu &#8220;vieux&#8221;. p6spy n&#8217;a pas été mis à jour depuis 2003 et pour IronEye SQL la société IronGrid a disparu. Comme il est maintenant impossible de trouver IronEye en téléchargement je vous propose la version 1.2.359 que j&#8217;avais heureusement conservée : [ironeyesql-installer-1\_2\_359.jar]({{ site.url }}{{ site.baseurl }}images/uploads/2011/03/ironeyesql-installer-1_2_359.jar). (fonctionne que sur Windows chez moi). Le site [sourceForge de p6spy](http://sourceforge.net/projects/p6spy/) est toujours up.

Sans refaire la doc, installer p6spy c&#8217;est simple, il faut juste remplacer le nom de votre driver jdbc par **com.p6spy.engine.spy.P6SpyDriver** et de mettre le nom du vrai driver dans le fichier spy.properties : <span><strong>realdriver = oracle.jdbc.driver.OracleDriver</strong></span><span>. Pour utiliser IronEye il faut en plus activer un port d&#8217;écoute dans le spy.properties :<br /> <strong>module.monitor=com.irongrid.monitor.server.MonitorFactory<br /> monitorport=2000</strong></span>

<span>Et voilà ! vous pouvez observer toutes les requêtes faites sur votre base. IronSQL va les regrouper, les compter et calculer le temps moyen d&#8217;exécution.</span>

<span>Sans être DBA vous allez très vite voir quelles requêtes sont faites souvent et les plus longues à s&#8217;exécuter. Très pratique pour voir si un cache L2 fonctionne bien ou si on a oublié un index sur une table.</span>

<span>Un exemple concret que j&#8217;ai corrigé hier :</span>

<span>Dans un service REST on passe en paramètre l&#8217;id d&#8217;un objet. C&#8217;est un service de monitoring appelé par du matériel pour lui passer des infos et s&#8217;assurer qu&#8217;il est encore en vie (du polling à défaut de push en gros)</span>

<pre name="code" class="java:nogutter:nocontrols">Truc t = trucDao.getById(tid);
t.setLastAccess(now);</pre>

<span>Assez logique en java avec hibernate, mais l&#8217;objet t n&#8217;est jamais utilisé après. Le problème c&#8217;est qu&#8217;au niveau SQL on a un SELECT qui récupère toutes les informations de l&#8217;objet pour ensuite faire un UPDATE. Si en plus vous avez configuré des associations de votre objet en lazzy, ça peut être vraiment problématique.</span>

<span>J&#8217;ai changé ce code par :</span>

<pre name="code" class="java:nogutter:nocontrols">trucDao.updateDateById(tid, now);</pre>

<span>Maintenant il ne reste que la requête UPDATE. Lorsque l&#8217;on sait que nous allons avoir plusieurs milliers de &#8220;Truc&#8221; et qu&#8217;ils font cette requète toutes les 15 secondes. Je vous laisse calculer le gain en perf. </span>Dans la même fonction j&#8217;ai aussi trouvé une requête SQL faite uniquement pour un log debug : no comment.