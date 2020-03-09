---
author: Samuel
categories:
  - Cloud
date: 2013-01-07 09:39:50+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.apptom.fr/?p=1398
id: 1398
permalink: /2013/01/lancer-un-cron-sur-un-cluster/
tags:
  - Amazon
  - EC2
title: Lancer un cron sur un cluster
url: /2013/01/07/lancer-un-cron-sur-un-cluster/
---

Sur un de mes projets j&#8217;ai besoin d&#8217;exécuter une tâche tous les jours. Cet exercice pourtant trivial peut devenir plus complexe si mon service utilise plusieurs serveurs et que je ne veux exécuter la tâche qu&#8217;une seule fois. En Java j&#8217;utilisais le [scheduler Quartz](http://quartz-scheduler.org/) pour régler ce problème. Il est très efficace et en cas de cluster il utilise une base de données pour s&#8217;assurer que la tâche n&#8217;est lancée que sur un seul serveur. Mais si votre tâche doit être lancée en shell ? J&#8217;ai donc cherché une solution pour le faire simplement sur mon projet utilisant des instances EC2.

Après pas mal de recherches, j&#8217;ai trouvé une solution simple sur [stackoverflow](http://stackoverflow.com/a/12623737). L&#8217;idée est bonne mais le script ne fonctionne pas (rien que l&#8217;utilisation de la commande hostname est étrange&#8230;).
  
J&#8217;ai finalement fait fonctionner ce script :

<pre name="code" class="ruby:nogutter">#!/usr/bin/env ruby

AWS_AUTO_SCALING_HOME='/opt/aws/apitools/as'
JAVA_HOME='/usr/lib/jvm/jre'
MY_GROUP = '&lt;GroupName&gt;'

@cmd_out = `bash -c 'JAVA_HOME=#{ JAVA_HOME } AWS_AUTO_SCALING_HOME=#{ AWS_AUTO_SCALING_HOME } as-describe-auto-scaling-instances -region &lt;REGION&gt; -I &lt;KEY&gt; -S &lt;SECRET&gt;'`

raise "Output empty, should not happen!" if @cmd_out.empty?
@lines = @cmd_out.split(/\r?\n/)
@last = @lines.select {|l| l.match MY_GROUP }.reverse.
detect { |l| l =~ /^INSTANCE\s+\S+\s+\S+\s+\S+\s+InService\s+HEALTHY/ }
raise "No suitable host in autoscaling group!" unless @last
@last_host = @last.match(/^INSTANCE\s+(\S+)/)[1]
@hostname = `wget -q -O - http://169.254.169.254/latest/meta-data/instance-id`

if @hostname.index(@last_host)
  puts "It's me!"
  exit(0)
else
  puts "Someone else will do it!"
  exit(1)
end</pre>

Il est aussi possible de gérer différemment la gestion de l&#8217;authentification AWS en passant par un fichier comme expliqué [ici](http://alestic.com/2010/09/aws-iam).

Ce script doit être exécuté par root. Ensuite il suffit d&#8217;ajouter une ligne dans la crontab de vos instances du type :

> 02 01 \* \* * ~/lastonly.rb && wget -q -O &#8211; http://www.mysite.com/cron/crontasks

Cette solution n&#8217;est pas parfaite mais elle a le mérite d&#8217;être simple. Une autre solution plus &#8220;propre&#8221; serait sans doute d&#8217;utiliser [Amazon Simple Workflow Service](http://aws.amazon.com/fr/swf/)