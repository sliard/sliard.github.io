---
author: Samuel
categories:
  - Java
date: 2021-03-28 15:25:05+00:00
general_page_bg_color:
  - '#FFFFFF'
general_page_bg_override:
  - false
general_page_bg_pattern:
  - none.png
general_title_show:
  - true
id: 1572
permalink: /2021/03/achete-un-chat-virtuel/
tags:
  - NFT
title: J'ai acheté un chat virtuel
url: /2021/03/achete-un-chat-virtuel/
---

Vous ne rêvez pas, nous sommes en 2021 et je découvre les cryptokitties 3 ans après sa sortie et alors que la "hype" est bien passée. Alors quel intérêt d'écrire un article sur ce sujet aujourd'hui ? Et bien simplement car début 2021,  il s'est passé des choses folles à propos de la vente de token NFT. Comme la vente du premier tweet de Jack Dorsey 2,5 millions ou comme l'oeuvre numérique de Beeple vendue 69,3 millions de dollars aux enchères.

Mon objectif n'est pas de vous expliquer comment vendre vous aussi votre plus beau JPG (il y a des tonnes de vidéos Youtube pour ça) mais plus de comprendre ce qu'est concrètement et techniquement un token NFT. Et quoi de mieux pour comprendre que d'essayer. N'ayant pas plusieurs millions en ETH pour acheter une oeuvre, je me suis rabattu sur un chat cryptokitties, mais j'aurais aussi pu acheter une image de joueur de foot sorare ou un bitburgersr.

## Blockchain et smart contract

L'élément de base, c'est que ces tokens s'intègrent dans une blockchain permettant l'exécution de smart contract. Un smart contract est juste un morceau de code. Ce code va définir la structure du token et la gestion de ce dernier (comment il est créé, les règles de transfert et celles de destruction). Ce code va aussi avoir besoin d'un espace de stockage pour sauvegarder ses données.

Cette question du stockage de données m'a intrigué. Où peut-on sauvegarder des données dans une blockchain ? Une blockchain, c'est avant tout une succession de block contenant une suite de transactions. Il n'y a pas de notion d'espace de stockage centralisé de variable… Ce que je n'avais pas compris, c'est qu'une blockchain comme ethereum est constituée de 2 parties :
* une partie block data
* une partie blockchain state

Dans le block data est sauvegardé l'ensemble des blocks de la blockchain et dans le blockchain state on retrouve par exemple la balance d'ETH d'un compte ou les variables d'un smart contract. Cet espace de stockage utilise un "Merkle Patricia Trie" pour référencer les données.

Savoir ou sont stockées les données c'est un bon début, mais il y a quoi dans un token ?

## Token ERC-721

Un token NFT c'est un "Non-Fungible Tokens". Un token non fongique est un token qui est unique et identifiable. Chaque token a sa propre valeur. Pas comme un billet de 10 euros que l'on peut changer par un autre billet de 10 sans aucune différence.

Pour que notre token soit utilisable par d'autres smart contract, l'idéal c'est qu'il implémente une interface. Et c'est pour cela qu'a été créé le modèle des token ERC721. 

Mais qu'est ce qu'il y a dans mon token exactement ? Et bien dans le cas de mon chat : juste un identifiant. Mon chat est identifié par l'adresse du contrat qui l'a créé et par son identifiant : 0x06012c8cf97bead5deae237070f9587f8e7a266d et 1222591

La norme ERC721 autorise aussi l'ajout de metadata avec un nom, un symbole et un "tokenURI" mais rien de plus. Et les développeurs essaient de mettre le minimum d'informations aussi car plus le token occupe de l'espace, plus il est cher à gérer (on reviendra plus tard sur les problèmes de coût). Si le token de mon chat n'est composé que d'un id, son smart contract stocke un peu plus d'informations :

{% highlight java %}
struct Kitty {
 uint256 genes;
 uint64 birthTime;
 uint64 cooldownEndBlock;
 uint32 matronId;
 uint32 sireId;
 uint32 siringWithId;
 uint16 cooldownIndex;
 uint16 generation;
}
{% endhighlight %}

Il y a donc dans le smart contract des cryptokitties une liste avec les caractéristiques de tous les chats. Mais pour sa photo, c'est une URL sur un serveur de Google. Et c'est là qu'on voit arriver un des plus gros paradoxes de ces tokens, on utilise une blockchain car elle est complètement décentralisée mais au final, souvent c'est une simple URL vers un serveur où est stocké "l'oeuvre". Heureusement des réseaux comme IPFS existent et proposent une alternative, mais c'est une autre histoire :)

C'est aussi grâce à cette interface que beaucoup de places de marchés comme OpenSea peuvent voir le jour. Elle peuvent effectuer des opérations avec leur propre smart contract sur l'ensemble des tokens respectant la norme ERC-721.

## La gestion du Gas

Un autre élément que j'ai eu du mal à appréhender en étudiant les smart contract c'est la notion de "Gas". Comme son nom l'indique c'est le "carburant" qui est utilisé pour effectuer des opérations sur la blockchain ethereum. Chaque transaction a un coût en Gas qui est ensuite reversé au noeud qui a validé le block de transaction dans la blockchain. Ce coût se transforme donc en ETH au moment de valider le block.

Mais combien va coûter l'exécution d'une méthode de smart contract ? Et bien c'est super simple à savoir car une fois votre code compilé dans le dialect EVM, chaque instruction à un coût. Le problème c'est qu'en fonction de l'exécution le coût va être différent (en fonction d'un if pas exemple). C'est pour cela qu'au moment de faire une transaction, il faut indiquer un "Gas Limit". Ca va éviter de mauvaises surprises en cappant le coût maximum de la transaction. Par contre c'est une arme à double tranchant. Car si par exemple vous limitez à 1000 Gas, mais qu'il en faudrait 1100 et bien la transaction va échouer mais vous serez quand même facturé des 1000 Gas (car le noeud a bien effectué ce travail).

Par exemple pour mon chat acheté 8$ j'ai eu 15$ de Transaction Fee car l'achat à consommé 64 344 Gas. C'est cher car il y a eu plusieurs opérations à faire. En effet j'ai acheté sur la place de marché du site. Il a donc fallu plusieurs étapes :
* le compte "CryptoKitties: Sales Auction" m'a envoyé le token
* mon compte a envoyé une grosse partie du prix au vendeur
* mon compte a envoyé une partie du prix au compte "Sales Auction"

C'est en étudiant le détail de la transaction que l'on découvre toutes ces étapes complètement transparentes au moment de l'achat.

## Pourquoi ?

Oui pourquoi prendre du temps pendant son weekend à comprendre le fonctionnement d'un chat virtuel ? Tout simplement car je pense que le développement d'applications décentralisées va devenir la norme dans le futur. Le champ des possibles est immense avec cette technologie.

Ma prochaine étape sera de développer un smart contract avec un token pour tester le principe. Affaire à suivre donc :)

## Références

[Tuto dev](https://www.youtube.com/watch?v=YPbgjPPC1d0)

[Vidéo info](https://www.youtube.com/watch?v=9yuHz6g_P50)

[Blog post smart contract](https://auth0.com/blog/an-introduction-to-ethereum-and-smart-contracts-part-2/)
