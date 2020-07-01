---
author: Samuel
categories:
  - Modelisation
date: 2009-07-20 08:00:22+00:00
guid: http://www.net-liard.com/blog/?p=434
id: 434
permalink: /2009/07/retour-sur-lacceleo-day/
tags:
  - Acceleo
  - MDA
  - Scrum
title: Retour sur l'acceleo day
url: /2009/07/20/retour-sur-lacceleo-day/
---

Vendredi 10 juillet avait lieu à Nantes les Rencontres Mondiales du Logiciel Libre. C&#8217;est dans ce cadre qu&#8217;Acceleo a choisi d&#8217;organiser une journée dédiée à leur outil de transformation M2T.

Etienne Juliot commence cette journée par une présentation de l&#8217;outil. Il a reussi à faire une présentation à la fois pour les débutants et pour les plus aguerris en y ajoutant quelques petites astuces bien pratiques. Le reste de la matinée était consacrée aux retours clients. Il y en aura quatre de Capgemini, Atos, Bull et OrangeLabs.  C&#8217;est celui d&#8217; Atos qui m&#8217;a vraiment marqué et pas forcément dans le bon sens du terme. J&#8217;ai été frappé par le fossé qu&#8217;ils creusent entre les développeurs et les architectes. Attention je ne stigmatise pas Atos, beaucoup de grands groupes (le mien en premier) partage cette approche et voient l&#8217;Architecte comme un dieu dans sa tour d&#8217;argent dictant sa loi aux gueux développeurs.

Pour ma part je ne l&#8217;approuve absolument pas et la distribution des rôles en scrum me donne raison. En effet en scrum les rôles architecte et développeur n&#8217;existent pas. Seul le rôle **team** compte. L&#8217;équipe doit bien sûr être composée d&#8217;experts en architecture et en développement mais ils doivent travailler ensemble. Pour moi un bon architecte doit mettre les mains dans le code et un bon développeur doit maîtriser l&#8217;architecture et même y contribuer.

Pour revenir à acceleo day, j&#8217;ai donc présenté très rapidement comment notre chaîne de génération a évolué avec le temps.

<div id="__ss_1704821" style="width: 425px; text-align: center;">
</div>

Je me suis bien amusé à le faire et ça a été partagé si j&#8217;en crois le premier retour que j&#8217;ai pu lire. Retour fait par Cedric Vidal qui avait le créneau le plus dur, celui d&#8217;après le repas. Il a fait une très bonne présentation sur le Scaffolding. Technique intéressante qui propose d&#8217;enrichir le modèle par une ou plusieurs transformations M2M (Model to Model) avant la génération de code. Ca permet de garder la main sur certains éléments pour les enrichir. L&#8217;exemple type est le service CRUD (Create, Read, Update, Delete) d&#8217;un entité, c&#8217;est intéressant de le générer et de garder le lien avec l&#8217;entité tout en l&#8217;ayant modélisé pour le compléter et le documenter.

Je n&#8217;ai malheureusement pas pu assister à la dernière présentation de Goulwen Le Fur car je devais reprendre la route. Vous pouvez lire ses slides sur [leur site](http://www.acceleo.org/wiki/index.php/EclipseAcceleoDay:Program).

Journée qui a donc été très enrichissante. C&#8217;est toujours intéressant de partager avec d&#8217;autres industriels pour comparer nos façons de faire.