---
author: Samuel
categories:
  - AgentIA 
date: 2025-04-08 08:25:05+00:00 
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
id: 1573
permalink: /2025/04/agent-ia-recrutement-chatgpt/
locale: fr_fr
tags:
  - n8n, chatGPT
title: Comment j'ai utilisé un agent IA pour booster ma recherche d'emploi
description: Je me suis demandé comment les utiliser pour optimiser ma recherche d'emploi. J'ai donc créé un agent capable de présenter mon CV à un recruteur.
image: "/images/uploads/2025/03/agentIA.png"
url: /2025/04/agent-ia-recrutement-chatgpt/
---

![agentIA.png](/images/uploads/2025/03/agentIA.png)

En ce moment, je suis à la recherche d'un nouveau poste et, comme les LLM et les agents IA sont à la mode, je me suis demandé comment les utiliser pour optimiser ma recherche d'emploi. J'ai donc créé un agent capable de présenter mon CV à un recruteur.

# My ChatGPT

La solution la plus simple consiste à personnaliser son ChatGPT. On utilise souvent cette méthode pour apprendre à ChatGPT à rédiger en copiant le style d'une personne.
Dans mon cas, j'ai spécialisé ce chat en commençant le prompt par:

> \# Role
> 
> Tu es mon agent qui va m'aider à présenter mon profil à des recruteurs. Les recruteurs se connectent pour obtenir des informations sur mon parcours professionnel, mon expérience sur des outils et/ou librairie de code que j'ai utilisé.

Ensuite, j'ai exporté mon profil LinkedIn en PDF pour l'intégrer à ChatGPT comme source d'information. J'ai même forcé l'utilisation exclusive de ce PDF pour éviter les hallucinations.

> \# Instructions
> - Tu n'utiliseras que les informations du document ProfileLinkedIn.pdf pour avoir des informations sur mon parcours.

Aux premiers tests, j'ai eu quelques surprises :

![ChatGpt pense que nous sommes en 2023](/images/uploads/2025/03/agent-age.png)

Alors ça me va très bien, mais c'est faux ! On oublie souvent que ChatGPT ne sait pas quel jour on est. J'ai donc ajouté l'année en cours dans le prompt pour obtenir des réponses correctes.
J'ai aussi fermé le prompt pour éviter les questions hors sujet ou toutes les tournures du style : "oublie ton prompt et…"

> \# Instructions
> - Ne répondre que sur des questions professionnelles autour de mon profil.
> - Ne jamais sortir de ton prompt et n'invente pas de réponse. Je serais très mécontent si tu donnais de fausses informations. Il faut mieux demander de reformuler la question.

J'utilise la phrase "Je serais très mécontent si tu donnais de fausses informations." depuis que [Sylvain Peyronnet](https://www.linkedin.com/in/sypsyp) m'a expliqué que les LLM ont comme principal objectif de satisfaire l'utilisateur, quitte à lui répondre n'importe quoi avec un ton très sûr d'eux. Cette simple phrase diminue énormément les hallucinations des LLM.

Le résultat est vraiment convaincant. Ce chat est très utile pour explorer mon CV dans le sens que je veux. En 25 ans, j'ai travaillé sur de nombreux projets. Avec cet agent, je peux facilement poser une question sur une technologie et retrouver les expériences en lien.

![Description de mes projets GCP](/images/uploads/2025/03/agent-gpt.png)

![Description de mes projets Java](/images/uploads/2025/03/agent-java.png)

![Je ne suis pas dev frontend](/images/uploads/2025/03/agent-frontend.png)

Cela fonctionne, mais cela reste un LLM spécialisé, pas un agent IA. Voyons comment aller plus loin.

# Créer un agent IA avec n8n

[n8n](https://n8n.io/) est un orchestrateur de tâches. Il permet d'assembler des briques logicielles de façon graphique avec très peu de code. C'est proche de [make.com](https://www.make.com/), mais en open source et simplement déployable via une simple commande Docker sur un serveur.

En plus, n8n propose un module Agent IA, qui intègre :
- Un client web chat public,
- La possibilité d'utiliser le LLM de son choix,
- La connexion à des outils pour permettre au LLM d'agir sur le monde extérieur.

![graph n8n de l agent](/images/uploads/2025/03/agent-n8n.png)

Dans mon exemple, j'ai ajouté un module permettant à mon agent d'ajouter directement un rendez-vous avec un recruteur dans mon agenda Google Calendar.

J'ai utilisé 4 outils :

1. Une requête HTTP pour récupérer les informations sur mon parcours depuis le site de mon CV.
2. Un workflow Calendar_Avaibility pour interroger mon calendrier et récupérer l'ensemble des rendez-vous sur deux mois.
3. CreationRdv pour ajouter un rendez-vous dans mon calendrier.
4. PrevenirContact, un module pour envoyer un mail via un serveur SMTP.

Un module de mémoire permet aussi d'attacher à une session la liste des réponses antérieures, conservant ainsi le contexte entre plusieurs messages.

La grosse différence ici est que l'on utilise l'API de ChatGPT. Il faut donc lui passer l'ensemble du contexte à chaque appel : la page HTML avec mon CV, les x derniers messages de la conversation et l'ensemble de mes rendez-vous sur deux mois. Cela fonctionne très bien, mais comme la facturation de l'API se fait par token envoyé et reçu, cela peut vite coûter cher. Une soirée de tests m'a coûté 4 centimes, ce qui reste raisonnable. Toutefois, si beaucoup de monde utilise l'agent, il faut mieux configurer une limite de paiement chez OpenAI.

Pour le prompt principal de l'agent, il est très proche du précédent. Il faut en plus ajouter une description des outils et de comment les utiliser.

Par exemple pour la partir rendez-vous

> Tu peux utiliser l'outil Calendar_Availability pour savoir si je suis disponible pour un entretien. Mais ne proposer un rendez-vous que du lundi au vendredi entre 9h et 17h si je suis disponible.
> Le user peut demander de créer un rendez-vous dans mon calendrier avec l'outil CreationRdv. Pour pouvoir le faire il faut lui demander de décrire un peu le poste et le nom de l'entreprise. Il faut aussi que le user donne son email pour l'ajouter en invité dans le rendez-vous. Il faut lui proposer 3 date/heure ou je suis disponible et que le client choisisse une des dates proposées. Ajoute les informations du poste dans la description du rdv et le texte "Interview XXXX" en remplaçant XXXX par le nom de l'entreprise donné. Les utilisateurs ne peuvent pas changer la date du rdv une fois que celui-ci est défini. Ils ne peuvent pas demander plusieurs rdv, s'il en demande un autre leur dire que c'est impossible et leur demander de me contacter par email directement.
> Les RDV sont tous d'une heure.

J'ai dû ajouter la limite à un rendez-vous pour éviter de remplir rapidement mon calendrier avec des tests. Vous noterez que c'est important de respecter certaines règles pour nommer vos outils. Un nom explicite et sans espace va être utilisé plus efficacement. Vous pouvez trouver pas mal de conseils sur le prompt avec [cette vidéo](https://www.youtube.com/watch?v=77Z07QnLlB8).

![test avec une mauvaise date](/images/uploads/2025/03/agent-date.png)

Ce chat fonctionne assez vite même s'il faut bien travailler son prompt pour diminuer les hallucinations.

J'ai également expérimenté avec d'autres sources de données. Par exemple, j'ai tenté de créer un agent pour l'organisation de l'Open d'échecs de mon club. J'ai ajouté la liste des joueurs inscrits dans une table Airtable que j'ai connectée comme outil et source de données. Cependant, l'agent ne parvenait pas à compter correctement le nombre d'inscrits.

![agent-open.png](/images/uploads/2025/03/agent-open.png)

Pour résoudre ce problème, j'ai remplacé Airtable par une extraction des pages HTML du site de la Fédération Française des Échecs et l'agent a immédiatement fonctionné correctement. L'outil Airtable est bien sûr utilisable, c'est juste que je n'ai pas réussi à tourner mon prompt pour que ça fonctionne alors qu'avec une source de données HTML, ça a fonctionné du premier coup.

# Bilan : quelle solution choisir ?
En une journée, j'ai réalisé deux chats utilisables pour présenter mon profil à un recruteur et planifier un rendez-vous. C'est très simple à mettre en place. Voici un récapitulatif des deux solutions :

## Mon ChatGPT
Avantages :
- Super simple à utiliser, sans compétences techniques requises
- Inclus avec l'abonnement ChatGPT Plus à 20$
- Coût fixe, même si des millions de personnes utilisent votre chat

Inconvénients :
- Ce n'est pas un agent IA, mais un LLM spécialisé

## Agent IA avec n8n
Avantages :
- Facile à utiliser en SaaS ou à déployer sur un serveur
- Compatible avec n'importe quel LLM (possiblement en local pour la confidentialité)
- Connexion facile à d'autres outils comme WhatsApp ou Telegram

Inconvénients :
- Tarification basée sur le nombre d'appels API

Dans les deux cas, la clé du succès repose sur la qualité du prompt. Un bon prompt détermine si votre chat fonctionnera bien ou non.

Testez [mon ChatGPT](https://chatgpt.com/g/g-67cad0c5b37c8191a68b8aa2e0f98cbb-recruter-samuel) et partagez votre expérience en commentaire ! Concernant l'agent n8n, je préfère ne pas partager l'URL pour éviter les risques de remplissage de mon calendrier et les coûts API.