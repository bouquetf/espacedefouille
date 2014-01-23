---
layout: post
title: "Méthode pour concevoir son processus"
date: "2014-01-23 13:55"
author:
categories: []
comments: true
published: false
---

Bien des fois, le design de processus est une tâche si ardue qu’elle finit souvent par un vrai sac de noeuds bon à jeter. Cet article tente d’adresser cette problématique en viennant compléter le post du 29 novembre 2011 : « où commencer son processus ?«  et propose une méthode de conception qui, je l’espère, vous permettra de concevoir un processus avec Bonita Open Solution aisément et rapidement.

1. Formalisation du métier

Un processus fait souvent intervenir différents acteurs et il peut être difficile d’extirper qui fait quoi et quand.

La première étape consiste donc à identifier clairement quels sont les différents profils qui interviendront dans le workflow. Une fois cette liste établie, l’étape suivante s’attaque aux processus vus par chaque acteur.Ainsi, on commence par établir le chemin le plus long de façon informelle : le « happy path ».

Ici, différentes tâches vont apparaître. Pour chaque tâche, il va falloir établir de façon claire et précise :

Les évènements déclencheurs de l’action. Le plus souvent, ce sera la fin de l’étape précédente, mais cela peut être des évènements basés sur le temps, ou même une information envoyée par un autre processus, …
Le produit résultat de l’étape : quel est le livrable de l’action effectuée à cette étape ? Qu’est-ce que l’on cherche à obtenir, pourquoi est-ce que cette étape est nécessaire : en quoi est-ce qu’elle résulte ?
Les ressources requises en plus que le profil acteur de cette tâche : quels sont les outils dont il va avoir besoin, est-ce qu’il va devoir travailler avec quelqu’un d’autre, … En bref, tout ce qui existe avant la tâche, ce qui sera utilisé pendant la tâche, mais se retrouvera intact après son exécution.
Les informations et produits nécessaires à l’établissement de l’activité. Ces produits seront consommés et éventuellement modifiés en le produit résultat.
Identifier l’activité en tant que tel et quel est l’évènement provoqué : quel est l’objectif de la tâche et la décision qui en résulte. Une bonne convention de nommage est ici de nommer une activité par un verbe d’action à l’infinitif et un produit résultat. « Saisir les informations », « Ouvrir un ticket », « Acheter bouteille de lait », …
Une fois que toutes les tâches de ce happy path ont été spécifiées, il convient de traiter tous les chemins alternatifs en partant de la fin du processus. Soit, pour chaque étape depuis en partant de l’évenement de terminaison, est-ce que j’ai une décision alternative possible ? Un chemin d’exception, … Si la réponse est oui, ce chemin alternatif devient le nouveau chemin le plus long à clarifier comme défini précédemment.

A ce point, nous aurons pour chaque profil d’acteur une liste de micro processus qu’il va falloir agréger et dans un sens cartographier pour obtenir un design clair, précis et configurable…

2. Configuration du ou des processus

Plus haut, nous avons établi l’ensemble des connaissances, des informations qui étaient nécessaires à l’exécution des tâches, et les décisions en résultant.

Toutes ces informations ne sont pas nécessaires à l’avancée de notre processus. Il s’agit pour la plupart de données métier dont le processus et sa logique n’ont que faire. L’étape suivante consiste donc à identifier clairement les informations nécessaires au processus pour les modéliser et donner au processus cette connaissance.

Ainsi, il convient de créer les conteneurs pour ces données (les variables) et les éventuels connecteurs nécessaires à leur manipulation. Le processus peut, dans certains cas, nécessiter des actions sur des services externes. Il est maintenant nécessaire d’établir ces connexions et donner au processus la connaissance nécessaire à ce que ses activités automatiques soient réalisées correctement.

A ce moment, notre processus est prêt à être exécuté. Le problème : il n’a aucune interaction avec le métier et les utilisateurs ne peuvent pas effectivement travailler : c’est l’application métier au dessus du processus.

3. Développement de l’application métier

Pour chaque étape où un utilisateur doit interagir, il faut modéliser les écrans qu’il utilisera pour effectuer le travail qui lui est demandé. Il s’agit d’interfaces (web) qui serviront à saisir de l’information. Une saisie d’information doit répondre à des règles d’ergonomie et d’utilisabilité qu’il va falloir modéliser à partir des informations identifiées dans au premier point de notre méthode. Il s’agit du développement de la vue de notre application métier.

En parallèle, il est nécessaire de spécifier le modèle de données métier, les sources de données, et l’interaction qu’elles vont avoir entre elles. Une fois le modèle de données établi et les sources identifiées/créées, il ne reste plus qu’à connecter nos modèles de formulaires avec les données qui lui seront utiles.

A cette étape, notre processus est prêt à être utilisé, mais potentiellement moche et avec des temps de chargement non négligeables qui le rendent peu « user friendly ».

L’étape finale consiste donc à optimiser les performances là où nécessaire et à établir le look’n'feel final de notre application.

Le mot de la fin

Le développement d’un processus comprend trois grandes étapes consécutives : la spécification de la façon de travailler (1), la configuration du processus pour qu’il puisse s’exécuter (2) et le développement des interfaces utilisateur (3).

L’expérience montre que l’étape 1 semble souvent assez rapide à mettre en place mais nécessite hélas un travail de spécification non négligeable et très souvent mal évalué. L’étape 2 est souvent la plus rapide car elle est presque automatique. L’étape 3 est souvent le plus gros développement d’un projet où l’on fait face à des détails souvent négligeables et pourtant si problématiques… Comme on le dit souvent : le client est roi, alors soignons ce que nos utilisateurs voient tous les jours.

