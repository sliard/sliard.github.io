---
author: Samuel
categories:
  - Cloud
date: 2014-02-05 09:32:50+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.apptom.fr/?p=1579
id: 1579
permalink: /2014/02/creation-dun-cron-avec-sns/
tags:
  - AWS
title: Création d'un cron avec SNS
url: /2014/02/05/creation-dun-cron-avec-sns/
---

Ou comment complètement détourner l&#8217;usage du service Amazon SNS.

Mon besoin est simple : pouvoir exécuter du code toutes les 30s. Cette tâche commencera et s&#8217;arrêtera en fonction d&#8217;actions utilisateur. En java j&#8217;aurais simplement utilisé Quartz, mais là mon code est en PHP et hébergé sur Beanstalk d&#8217;Amazon.

Je n&#8217;ai pas trouvé de service simple à utiliser sur AWS pour faire ça. On trouve bien un peu de doc pour le faire avec Data Pipeline mais c&#8217;est loin d&#8217;être trivial. Après beaucoup d&#8217;hésitation j&#8217;ai décidé d&#8217;utiliser le service SNS.

Pour faire simple, SNS est un service de diffusion de message multi-canal. (doc complète [ici](http://docs.aws.amazon.com/sns/latest/dg/welcome.html "SNS") )

![SNS](/images/uploads/2014/02/sns-how-works.png)

Par contre il n&#8217;est pas fait pour envoyer un message périodiquement. Avec SNS on ne peut pas non plus dire &#8220;envoie ce message dans 30s&#8221;, le message est distribué de suite. Donc pour mon cas d&#8217;usage ce n&#8217;est pas vraiment l&#8217;idéal. J&#8217;aurais tellement aimé pouvoir dans mon code avoir un consommateur de message qui une fois le traitement fini s&#8217;envoie un nouveau message à lui même mais pour dans 30s.

Malheureusement ce n&#8217;est pas aussi simple et c&#8217;est lorsque j&#8217;ai regardé les politiques de retry pour les abonnements en http que j&#8217;ai trouvé une solution à mon problème. En effet, dans le cas d&#8217;un message envoyé sur un consommateur HTTP, si la requête retourne un code d&#8217;erreur (type 5xx) alors le message n&#8217;est pas considéré comme lu et va être représenté au même consomateur suivant une politique de retry configurable (toutes les infos [sur la doc](http://docs.aws.amazon.com/sns/latest/dg/DeliveryPolicies.html)).

![SNS](/images/uploads/2014/02/sns-delivery-policy-defaults.png)

Et là on voit bien se profiler une tâche périodique 

C&#8217;est, je vous l&#8217;accorde, assez border line. Mais ça a le mérite d&#8217;être simple et de fonctionner. Le seul inconvénient c&#8217;est que le nombre de retry est limité à 99. Donc dans mon cas mon cron s&#8217;arrêtait après 50 minutes. Il n&#8217;y a pas d&#8217;information dans le message envoyé par SNS du nombre de retry, par contre il y a sa date d&#8217;émission. Dans mon consommateur, j&#8217;ai donc codé qu&#8217;après 2 minutes  j&#8217;envoyais un nouveau message et retournais un code HTTP 200 pour consommer le message et arrêter les retry sur celui-ci. Au début j&#8217;avais mis 10 minutes, mais je ne sais pas pourquoi, même avec un code 200 les retry continuaient toujours sur le message. Avec 2 minutes (et donc moins de retry) aucun problème.

Cela donne cette architecture :

![SNS](/images/uploads/2014/02/SNS.png)

Et un diagramme de séquence pour bien comprendre le déroulement  :

![SNS](/images/uploads/2014/02/Untitled-4.png)

<p style="text-align: left;">
  Dans ce cas je configure la politique de retry avec les options suivantes :
</p>

<pre class="php:nogutter">"minDelayTarget" =&gt; 30,
"maxDelayTarget" =&gt; 30,
"numRetries" =&gt; 10,
"numMaxDelayRetries" =&gt; 0,
"numNoDelayRetries" =&gt; 0,
"numMinDelayRetries" =&gt; 0,
"backoffFunction"=&gt; "linear"</pre>

Oui retourner une erreur 500 alors que le traitement s&#8217;est bien passé n&#8217;est pas très orthodoxe, Mais le système fonctionne bien, je peux voir sur la console SNS le nombre de Topic ouverts et donc le nombre de cron en cours d&#8217;exécution. C&#8217;est assez pratique. Si vous avez d&#8217;autres solutions je suis preneur ! (des services comme [setcronjob](http://www.setcronjob.com) ou même [easycron](http://www.easycron.com/?r=15708) sont trop limités au niveau requête par jour)