---
author: Samuel
categories:
  - AgentIA 
date: 2026-03-08 09:15:05+00:00 
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
id: 1574
permalink: /2026/03/copilot-cli-online/
locale: fr_fr
tags:
  - claude code, copilot
title: GitHub Copilot CLI vs Online
description: J'ai eu envie de faire un test simple, demander a GitHub Copilot de generer le meme site via deux approches differentes, une en mode CLI et une en mode online.
image: "/images/uploads/2026/03/cli/home.png"
url: /2026/03/copilot-cli-online/
---

# GitHub Copilot : CLI vs Online

J'ai eu envie de faire un test simple: demander a GitHub Copilot de generer le meme site via deux approches differentes, une en mode CLI et une en mode online.

L'idee ici c'est  d'observer les differences de rendu ecran par ecran. Les deux generations couvrent globalement le meme besoin, avec des variations sur la presentation, la hierarchie visuelle et quelques details d'ergonomie.

Vous pouvez regarder la branche [construite avec la CLI](https://github.com/sliard/TestChessCopilot2/tree/feature-cli) pour voir les fichiers modifies.
Et la branche [construite en ligne](https://github.com/sliard/TestChessCopilot2/tree/copilot/implement-all-features) pour voir les fichiers generes. 

Les fichiers dans le répertoires docs sont les mêmes et pourtant on constate des différences.

## Home

| CLI | Online |
| --- | --- |
| ![Home version CLI](/images/uploads/2026/03/cli/home.png) | ![Home version Online](/images/uploads/2026/03/online/home.png) |

## Create Account

J'ai laissé l'erreur CSS alors qu'a mon avis ça pouvais ce corriger rapidement.

| CLI | Online |
| --- | --- |
| ![Create Account version CLI](/images/uploads/2026/03/cli/CreateAccount.png) | ![Create Account version Online](/images/uploads/2026/03/online/CreateAccount.png) |

## Opening

| CLI | Online |
| --- | --- |
| ![Opening version CLI](/images/uploads/2026/03/cli/Opening.png) | ![Opening version Online](/images/uploads/2026/03/online/Opening.png) |

## Opening Edit

| CLI | Online |
| --- | --- |
| ![Opening Edit version CLI](/images/uploads/2026/03/cli/OpeningEdit.png) | ![Opening Edit version Online](/images/uploads/2026/03/online/OpeningEdit.png) |

## Opening View

| CLI | Online |
| --- | --- |
| ![Opening View version CLI](/images/uploads/2026/03/cli/OpeningView.png) | ![Opening View version Online](/images/uploads/2026/03/online/OpeningView.png) |

## Public / Private

| CLI | Online |
| --- | --- |
| ![Public Private version CLI](/images/uploads/2026/03/cli/PublicPrivate.png) | ![Public Private version Online](/images/uploads/2026/03/online/PublicPrivate.png) |

## Conclusion

Ce comparatif confirme que **la qualité du résultat dépend autant du contexte et des instructions que de l'outil lui-même**. Les différences observées s'expliquent en partie par le fait que j'ai focalisé mes descriptions sur les besoins fonctionnels de l'utilisateur, sans jamais mentionner d'aspects ergonomiques ou de design.

Point intéressant : aucune des deux générations ne propose d'éditer une ouverture en déplaçant directement les pièces sur l'échiquier, fonctionnalité que j'avais pourtant obtenue lors d'une [première génération](https://github.com/sliard/TestChessCopilot). Cela montre l'importance de la formulation des prompts et du contexte dans lequel l'IA travaille.
