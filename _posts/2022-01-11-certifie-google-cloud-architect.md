---
author: Samuel
categories:
  - Cloud
date: 2022-01-11 15:25:05+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
id: 1572
permalink: /2022/01/certifie-google-cloud-architect/
tags:
  - GCP
title: Certifié Google Cloud Architect
url: /2022/01/certifie-google-cloud-architect/
---

C'est fait ! Cette semaine j'ai passé l'examen de la certification "Google Professional Cloud 
Architect" avec succès ! Je vous propose de partager ici comment se sont déroulées la formation
et la préparation du test.


>TL;DR
>* La formation Coursera + Qwiklabs n'est pas suffisante (20% du travail de mon point de vue)
>* Faites plus de Qwiklabs et sortez des scripts pour tester les services
>* Lisez le livre Official Google Cloud Certified Professional Cloud Architect Study Guide
>* Les tests sur le site whizlabs sont très bien faits
>* Le site Examtopics est indispensable mais nécessite beaucoup de réflexion car les solutions proposées sont souvent fausses.

<div style="text-align:center"><img src="/images/uploads/certificationGCP.png"/></div>

Le 13 mars 2021, Orange signe un partenariat avec Google. Avec ce contrat Orange va pouvoir utiliser Google Cloud Platform : GCP. Il faut donc nous former.

## Les certifications

Il y a 8 certifications proposées :
* Cloud Architect
* Cloud Engineer
* Data Engineer
* Network Engineer
* Security Engineer
* Data Scientist ML Engineer
* Cloud Devops Engineer
* Cloud Developer


Dans mon cas, j’hésite entre la "Professional Cloud Architect" et la "Professional Cloud Developer" qui 
sont assez proches même si l'Architect a un scope plus important. Comme nous avons accès à l'ensemble des 
formations sur coursera, au lieu de choisir je fais les 2 parcours. Après plusieurs dizaines d'heures de vidéos,
je valide le parcours coursera. Cela donne accès à Qwiklabs. Qwiklabs est un outil pour faire des TP sur GCP.
C'est extrêmement bien fait. Le service vous donne accès à un compte google de test avec lequel vous pouvez
utiliser GCP pendant une durée limitée pour faire le TP. A la fin du temps, Google coupe le compte et détruit
ce qui a été fait pendant le TP. Vous pouvez donc jouer avec GCP sans avoir besoin d'utiliser votre CB.

## Qwiklabs

Pour pouvoir aller passer la certification, Google vous demande d'avoir des badges [Qwiklabs](https://www.qwiklabs.com/). Pour avoir un
badge il faut suivre une "Quest" (une série de lab). C'est intéressant car on peut manipuler vraiment l'interface
GCP. Le point négatif c'est que la plupart des labs sont un peu linéaires. Vous pouvez les faire en 5 minutes
en copiant collant les commandes sans vraiment réfléchir. Evidemment je ne vous le conseille pas, ça perd
complètement l’intérêt du lab. Bien au contraire, essayez d'utiliser le temps qui n'est pas consommé à la
fin du lab pour essayer des choses. Souvent les comptes utilisés par les labs ont des quotas très faibles
pour ne pas qu'on en abuse. Par exemple si un TP vous demande de créer 2 VM, il est souvent impossible d'en
créer plus de 2. De même pour l'activation des API. Pour un TP sur Pub/Sub, les API des services de Machine
Learning sont désactivées. Mais j'ai remarqué que les TP kubernetes avait souvent plus d'API et de quota.
J'ai pu tester des créations de base SQL par exemple. Attention de ne pas consommer trop quand même, 
il y a un gros risque que le TP se coupe brutalement. 

Souvent le dernier lab d'une quest est un "Challenge Lab".
Ces derniers sont beaucoup plus compliqué pour 2 raisons. Déjà ils ne sont pas guidés. On vous donne un 
objectif, mais pas les commandes pour le faire. Il faut se souvenir des autres labs de la quest. Mais le point
le moins drôle, c'est que parfois on pense avoir bien fait mais Qwiklabs ne valide pas certaines étapes et
souvent il n'y a pas d'explication. Parfois c'est juste une erreur bête dans le nom d'une ressource et le
script de validation est perdu. Mais il y a aussi des Qwiklabs de buggés. Par exemple ceux sur Apigee sont
pratiquement infaisables. J'ai signalé début septembre le problème sur le lab "Apigee API Security" mais il
est toujours buggé. Cela empêche d'avoir le badge "Apigee API Management" nécessaire pour la certification
"Professional Cloud Developer". C'est aussi pour cela que j'ai décidé de passer la certification Architect.
Attention, vous ne pouvez pas faire un lab plus de 3 fois (succès ou échec).

## Toujours plus de QCM

Fin octobre, j'ai obtenu les badges nécessaires pour passer la certification. Pour sortir des formations en vidéo,
je m'inscris sur une formation de fin de parcours d'une journée "Preparing for the Professional Cloud Architect".
C'est en visio mais avec un formateur de chez Google. Pendant cette formation je me rends compte qu'il me manque
certaines bases. Pour se préparer à l'examen, Google propose un [Google Form avec 20 questions](https://docs.google.com/forms/d/e/1FAIpQLSdvf8Xq6m0kvyIoysdr8WZYCG32WHENStftiHTSdtW4ad2-0w/viewform). Je fais l'exercice
et j'ai juste un peu plus de 50% de bonnes réponses. Plus grave, j'ai des questions super pointues sur des points 
que je n'ai jamais regardés. Je pars donc à la recherche de plus de jeu de questions. Dans un premier temps, 
j'ai acheté le livre ["Official Google Cloud Certified Professional Cloud Architect Study Guide"](https://www.wiley.com/en-in/Official+Google+Cloud+Certified+Professional+Cloud+Architect+Study+Guide-p-9781119602446). Il est très 
bien fait même si les 3 derniers chapitres sont maintenant hors scope pour la certification. Il date de 2019, 
il y a donc des choses qui ne sont pas à jour. Par contre le gros point positif, c'est qu'à la fin de chaque 
chapitre il y a des QCM pour vous entraîner.

Mais il m'en fallait encore plus, j'ai donc trouvé une formation avec 4 examens blancs sur le site de [whizlabs](https://www.whizlabs.com/google-cloud-certified-professional-cloud-architect/).
C'est cette formation et surtout les tests qui m'ont aidé à trouver les points que je n'avais pas assez approfondis.
Enfin, le dernier lien que j'ai trouvé a été finalement le plus important : [Examtopic](https://www.examtopics.com/exams/google/professional-cloud-architect/). ***Mais attention !*** 
C'est aussi le plus dangereux. En effet, les solutions affichées sont souvent mauvaises (dans 1 tiers des cas).
Les réponses ont été sélectionnées par celui qui gère le site et il a fait beaucoup d'erreurs. Heureusement, 
pour chaque question il y a une partie "discussion" qui permet à chacun d'argumenter sur la bonne réponse. 
Mais ça reste un avis. Il n'y a aucune réponse validée par Google. Donc utiliser le avec intelligence.

## Le jour J

Avec ces éléments je pouvais planifier la date de passage pour la certification et un plan de révision.
Sur 3 semaines, j'ai travaillé cette certification
à 50% de mon temps de travail et à 100% le weekend. Alors je ne dis pas que ce rythme est obligatoire pour
l'avoir ni que c'est un modèle. C'est juste ma façon de faire. Je préfère bosser beaucoup sur un temps assez court.
Et il faut bien comprendre que Google recommande d'avoir un an d'utilisation de la plateforme avant de passer
la certification. Dans mon cas, je n'ai absolument pas ce recul. J'ai donc dû travailler plus.

Arrive le jour J. L'examen c'est une série de 50 QCM (enfin plus souvent des QCU) à faire en 2 heures. 
Pour rentrer dans la salle il faut présenter ***2 pièces d'identités*** (la seconde n'a pas forcement besoin de 
photo juste le nom, CB ou carte vitale passent). On donne aussi montre connectée et téléphone. Dans la salle
il y a juste un PC, pas de papier ni de crayon. Pas de pause technique pendant les 2h, interdiction de boire
ou de manger et toute sortie de la salle arrête le test. Il est aussi possible de le passer à distance mais 
les conditions sont encore plus strictes. Il faut le faire dans une pièce fermée, sur un poste Windows où il
faudra installer un logiciel nécessitant les droits admin. Pendant l'examen le casque est 
interdit, il ne faut pas tourner la tête, ni mettre sa main devant sa bouche. Et en cas de coupure internet, 
c'est perdu.

Pendant le test, les 50 questions s'enchaînent. Il n'y a pas de point négatif sur des erreurs, il faut donc
répondre à toutes les questions même si on a un doute. Il est possible de marquer les questions où vous avez
un doute. A la fin vous pouvez plus facilement les retrouver. Après 1h20 j'avais répondu aux 50 questions. 
Ensuite j'ai passé 20 minutes pour revoir les 15 questions que j'avais marquées.

A la fin, il faut valider et confirmer qu'on a terminé. Je m'attendais à avoir le résultat sur la page d'après, 
mais non ! Je tombe sur une page avec un champ texte pour rédiger mon avis sur le test. Je note n'importe quoi 
pour passer à la suite. Toujours pas de résultat ! Maintenant on me demande si je veux remplir un sondage. 
Heureusement on peut skip et enfin arrive une page où est noté "Exam : Pass" en petits caractères et sans couleur 
ni confettis.. Il faut lire l'encart plus bas pour comprendre que ça doit être noté "Pass" ou "Fail". 
Donc je respire, ça passe !

Aucun score n'est donné, en cas d'échec on ne peut pas savoir si on a raté de peu ou pas. Google ne communique 
pas sur le score cible. On ne sait pas s'il faut 70 ou 80% de bonnes réponses.

Si j'ai fini assez rapidement, c'est que j'avais déjà vu au moins la moitié des questions sur le site Examtopic. 
Je vous conseille donc fortement de travailler sur ce site même si encore une fois il faut faire très attention 
aux réponses proposées par le service.

En espérant que ce retour vous aide dans vos révisions !
