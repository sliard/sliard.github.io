---
author: Samuel
categories:
  - iPhone
date: 2012-07-07 17:28:56+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
guid: http://www.apptom.fr/?p=1297
id: 1297
permalink: /2012/07/jenkins-pour-xcode/
tags:
  - ios
  - iPhone
  - jenkins
  - ota
  - XCode
title: Jenkins pour xCode
url: /2012/07/07/jenkins-pour-xcode/
---

Il n&#8217;est pas concevable pour moi de développer sans avoir une plateforme d&#8217;intégration continue. Il existe pas mal de solutions pour le faire en mode SAAS (sur <a title="Cloudbees" href="http://www.cloudbees.com/" target="_blank">cloudbees</a> pas exemple). Par contre pour le faire sur des projets iOS c&#8217;est plus dur à trouver car il faut le faire sur un MAC. J&#8217;ai donc installé un jenkins sur un Mac mini et ce n&#8217;est pas si évident que ça à faire.

## Installation

Jenkins c&#8217;est un simple war à installer sur un serveur. Pour nous simplifier la vie une version installable est disponible <a title="Jenkins installation" href="http://jenkins-ci.org/content/thank-you-downloading-os-x-installer" target="_blank">ici</a>. Mais les premiers problèmes arrivent vite à cause des droits utilisateur. Par défaut Jenkins utilise l&#8217;utilisateur deamon et ça pose pas mal de problèmes.

J&#8217;ai trouvé la solution sur ce blog (lien cassé :( ).

Pour résumer, il faut changer la configuration par défaut et installer Jenkins pour qu&#8217;il démarre avec l&#8217;utilisateur jenkins &#8220;Start at boot as jenkins&#8221;. Ensuite il faut créer l&#8217;utilisateur :

> sudo dscl . create /Users/jenkins
  
> sudo dscl . create /Users/jenkins PrimaryGroupID 1
  
> sudo dscl . create /Users/jenkins UniqueID 300
  
> sudo dscl . create /Users/jenkins UserShell /bin/bash
  
> sudo dscl . create /Users/jenkins home /Users/Shared/Jenkins/Home/
  
> sudo dscl . create /Users/jenkins NFSHomeDirectory /Users/Shared/Jenkins/Home/
  
> sudo dscl . passwd /Users/jenkins

Grâce à ça vous allez pouvoir créer les clés SSH pour utiliser jenkins avec github. Pour cela il faut suivre <a href="https://help.github.com/articles/generating-ssh-keys" target="_blank">la doc github</a> en utilisant l&#8217;utilisateur jenkins.

## XCode

Maintenant que nous pouvons récupérer les sources, il faut construire un IPA. Commencez par ajouter <a href="https://wiki.jenkins-ci.org/display/JENKINS/Xcode+Plugin" target="_blank">le plugin xcode</a> dans jenkins.

A partir d&#8217;XCode 4.3, il faut commencer par changer le répertoire de base avec la commande :

> sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer

J&#8217;ai eu aussi des problèmes avec les certificats développeurs. Par défaut ils sont installés dans le trousseau au niveau session donc inaccessibles d&#8217;un autre utilisateur. Là j&#8217;ai utilisé la méthode un peu &#8220;bourine&#8221; et j&#8217;ai ajouté mes certificats au niveau système.

Ensuite le build était bloqué car il ne trouvait pas le fichier de provisioning. Il suffit de les ajouter dans le répertoire :

> /Users/jenkins/Library/MobileDevice/Provisioning

Et voilà ! On a enfin généré un fichier IPA avec Jenkins.

## Over The Air

Pour aller un cran plus loin, j&#8217;ai eu envie de mettre en place un site pour faciliter l&#8217;installation de l&#8217;application. C&#8217;est possible depuis iOS 4. Il faut générer le plist associé à l&#8217;IPA et faire une page web avec un lien vers le plist. Mais j&#8217;ai arrété mes recherches de script pour faire ça lorsque j&#8217;ai découvert le service testFlight. Il suffit d&#8217;uploader l&#8217;IPA et testflight s&#8217;occupe de la diffusion sur les terminaux de tests (et bien plus en fait). Comme il y a un plugin jenkins pour testflight l&#8217;intégration est transparente.

&nbsp;

En espérant que cette note vous gagne du temps ! :)

Liens :

  * Blog DeadMeta4
  * <a title="Cloudbees" href="http://www.cloudbees.com/" target="_blank">Cloudbees</a>
  * testFlight

&nbsp;