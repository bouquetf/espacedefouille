---
layout: post
title: "Retour sur l'organisation d'un dépôt SVN"
date: "2014-01-23 13:57"
author:
categories: []
comments: true
published: false
---

Trop souvent, je me suis retrouvé dans des environnements de travail où les recommandations pour une utilisation de subversion sans trop de heurts n’étaient pas appliquées, car méconnues. Je vais donc tenter, dans cet article et au moins un autre à venir, de faire un tour d’ensemble de quelques bases et bonnes pratiques sur l’outil afin que tout le monde se comprenne et que les soucis les plus courants soient évités.
 La lecture de ces quelques lignes sous entend que les bases sur l’utilisation de SVN soient déjà connues (comme ce qu’est un commit, comment effectuer un checkout, …). De plus, afin de lever les ambiguïtés des traductions approximatives, je ne m’y hasarderai pas et utiliserai aussi souvent que nécessaire des anglicismes communément pratiqués.

Avant toute chose, revenons sur la façon dont nous contribuons à l’aide de subversion. Le schéma de base est le suivant : un repository SVN central et une série de committeurs qui soumettent régulièrement leurs changements au répertoire trunk. Autour de cela, il apparaît souvent, dans le cas de logiciels libres notamment, que la plupart des contributeurs occasionnels n’aient qu’un accès en lecture aux sources du projet. La seule solution qui leur est offerte est d’envoyer (via mail par exemple) des patchs aux committeurs pour que ces derniers intègrent les changements aux sources du projet.
 La question que l’on peut alors se poser, c’est comment soumettre un patch et comment l’appliquer. La toute première chose à faire est de travailler sur les dernières versions des sources (un checkout du trunk s’impose donc). Une fois les modifications apportées, la commande svn diff permet d’afficher à l’écran les différences entre la dernière révision et la version de l’espace de travail. Pour construire un patch, il convient de lancer cette commande à la racine du répertoire de travail et de rediriger la sortie dans un fichier. Exemple sous unix :
 $ svn diff > ../monpatch.patch
 Par la suite, l’application d’un patch se fait à la racine du projet à l’aide de la commande :
 $ patch -p0 -i ../monpatch.patch

Dans la peau du committeur maintenant, arrêtons nous sur la fréquence des commits. Cette question est récurrente dans les équipes de développeurs. Certains ne commitent qu’une fois en fin de journée, d’autres à chaque ligne ajoutée au projet. La bonne pratique est de commiter de façon logique et plusieurs fois par jour. Dans les grandes lignes, commiter logiquement se prépare dès que travail à faire est découpé en tâches et sous-tâches. Il convient de séparer les développements en petits blocs atomiques, qui, une fois conçus, testés et débuggés sont commités. En général, ces blocs ne devraient nécessiter que quelques minutes à deux heures de travail et correspondent à des sous-tâches du processus de développement.

Il arrive souvent que j’entende autour de moi des développeurs dire “je commit le travail que j’ai fait ce soir pour sauvegarder, c’est normal si ça compile pas, je continuerai demain”. C’est une pratique à bannir immédiatement ! Si vous n’avez pas le temps de terminer votre sous-tâche, ne la commitez pas. Une pratique qui peut être une bonne idée serait même de supprimer vos changements et de repartir le lendemain sur un espace de travail sein. Après tout, vous n’aviez sûrement pas travaillé plus d’une heure avant de commiter et le travail de réflexion a déjà été fait emoticon_smile Le code résultant n’en sera que plus rapide à produire et plus propre.

Jusqu’alors, nous n’avons discuté que du trunk. Cependant, un dépôt, c’est bien plus que ça. Subversion n’offre pas de distinction entre la notion de répertoire et des notions telles que les branches ou les tags. Certains y voient une flexibilité appréciable, d’autres un mélange des concepts. Il convient donc d’assoir des conventions d’utilisation pour que tout le monde s’y retrouve. Voyons tout de suite celles qui sont couramment appréciées. Tout d’abord, pour la gestion de plusieurs projets, il est possible de créer un dépôt par projet ce qui pour des raisons d’administration, peut être difficile et laborieux. Une autre solution consiste alors à créer un seul dépôt qui contiendra en sa racine un répertoire par projet.
 Ensuite, chaque projet devrait idéalement contenir 3 sous répertoires : trunk, branches et tags.

Le trunk est destiné à recevoir les dernières versions des sources. Une idée à garder constamment à l’esprit est que le trunk doit être dans un état stable, c’est à dire que le source doit compiler et ne pas avoir subi de régression depuis le dernier commit. Il peut arriver par exemple que les outils d’intégration continue soient configurés pour annuler un commit si suite à celui-ci, le projet ne compile plus, voir que certains jeux de tests ne passent plus.
Le répertoire branches est destiné à héberger les branches parallèles de développement du projet. On distingue classiquement trois types de branches :
les branches de release qui contiennent une version stable du projet. Les seuls changements apportés seront des corrections de bugs. Aucun ajout de fonctionnalité ne sera effectué ici.
les bug fix qui contiennent les corrections de bugs qui ne peuvent pas être effectuées rapidement (i.e. en un seul commit)
les branches expérimentales qui contiennent les tests de passage à une nouvelle version de librairie, d’une nouvelle technologie, …
Le répertoire tags destiné à héberger les versions identifiées, à un moment donné du projet. Aucune modification ne sera appliquée ici. On distingue deux type de tags :
les “release tag” qui identifient la première version de la release
les “bug fix PRE/POST” qui identifient respectivement la version du projet où le bug est apparu et la version du projet qui correspond à la correction du bug.
Cet article s’est contenté d’offrir une vision de base sur l’organisation d’un dépôt SVN, et de la façon de l’utiliser sommairement. Dans un prochain article, je m’arrêterai sur les détails de la réalisation de quelques tâches courantes comme la façon de releaser un projet, comment corriger un bug, ou encore comment revenir proprement à une ancienne révision (ou version) des sources.