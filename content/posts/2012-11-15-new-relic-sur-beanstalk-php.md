---
author: Samuel
categories:
  - Cloud
date: 2012-11-15 21:34:41+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.apptom.fr/?p=1369
id: 1369
permalink: /2012/11/new-relic-sur-beanstalk-php/
tags:
  - AMI
  - Beanstalk
  - EC2
  - New Relic
title: New Relic sur du Beanstalk PHP
url: /2012/11/15/new-relic-sur-beanstalk-php/
---

Ces derniers temps j&#8217;ai beaucoup travaillé sur les produits Amazon Web Services. J&#8217;ai notamment utilisé Beanstalk pour mettre en production un site web important. Pour mesurer l&#8217;activité des serveurs et l&#8217;utilisation de l&#8217;application j&#8217;ai utilisé le service <a title="new relic" href="https://newrelic.com" target="_blank">New Relic</a>. En plus il existe un <a title="Newrelic aws" href="http://newrelic.com/aws" target="_blank">partenariat entre AWS et New Relic</a> pour utiliser un compte standard gratuitement (vous économisez $50 par mois).

Pour utiliser New Relic il faut l&#8217;installer sur une image et en faire une nouvelle AMI. Dans un premier temps j&#8217;ai fait l&#8217;erreur de faire une image depuis une instance EC2 lancée par Beanstalk. Ca ne peut pas fonctionner car vous intégrez votre application à l&#8217;image. La procédure est assez simple une fois qu&#8217;on a compris ça.

  1. Notez la référence de l&#8217;AMI utilisée en ce moment pas Beanstalk (dans mon cas ami-df9b9cab)
  2. Lancez une nouvelle instance EC2 basée sur l&#8217;AMI notée juste avant
  3. Loggez vous sur la VM pour y installer New Relic. Toute la doc est disponible <a title="newrelic php" href="https://newrelic.com/docs/php/the-newrelic-install-script" target="_blank">ici</a>, mais pour du PHP sous centos 64 bits ça donne ça :
> <pre>sudo rpm -Uvh http://yum.newrelic.com/pub/newrelic/el5/x86_64/newrelic-repo-5-3.noarch.rpm

sudo yum install newrelic-php5

sudo newrelic-install

sudo chown elasticbeanstalk:elasticbeanstalk /etc/php.d/newrelic.ini

sudo chmod 777 /etc/php.d/newrelic.ini</pre>

  4. Editez ensuite le fichier /etc/php.d/newrelic.ini pour indiquer votre clé API dans &#8220;newrelic.license&#8221; et changez le nom de l&#8217;application dans &#8220;newrelic.appname&#8221;. Par contre j&#8217;ai remarqué que sur ma VM le démon New Relic n&#8217;était pas lancé automatiquement au démarrage. Il faut donc exécuter la ligne de commande :
> <pre>sudo chkconfig newrelic-daemon on</pre>

  5. Ensuite on peut ajouter le monitoring du serveur
> <pre>sudo yum install newrelic-sysmond</pre>
> 
> <pre>sudo nrsysmond-config --set license_key=YOUR_LICENSE_KEY</pre>
> 
> <pre>sudo /etc/init.d/newrelic-sysmond start</pre>

Une fois que vous avez bien vérifié que les services sont bien lancés au démarrage, vous pouvez construire une AMI depuis la console. Ensuite il faut indiquer la référence de l&#8217;AMI au niveau de la configuration de l&#8217;environnement Beanstalk dans &#8220;Custom AMI ID&#8221;

C&#8217;est aussi simple que ça 😉