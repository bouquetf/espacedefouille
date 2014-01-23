---
layout: post
title: "Premier sentiment à  l'approche du test driven development"
date: "2014-01-23 13:57"
author:
categories: []
comments: true
published: false
---

Le « test driven development » est une pratique assez ancienne, repopularisée récemment par l’extreme programming. Il s’agit d’une approche qui permet d’améliorer la qualité des développements en écrivant les tests avant la réalisation de la fonctionnalité correspondante. Ces quelques lignes ont été motivées par ma propre expérience au sein d’un projet professionnel où nous avons adopté une méthodologie similaire suite à de nombreux tâtonnements qui nous ont au final permis un gain énorme en temps et en qualité de code. Cet article ne s’attardera que sur quelques sentiments, quelques principes et enseignements que ce projet a permis de mettre à jour.

Dans les grandes lignes, la méthode consiste à écrire au préalable les tests, conformément aux spécifications de la tâche à réaliser, puis d’implanter cette fonctionnalité en gardant à l’esprit que ce que l’on cherche, c’est passer les tests avec succès, rien d’autres. Le code réalisé doit être le plus simple possible et dédié seulement à ce que le test correspondant soit exécuté avec succès. L’exécution de la totalité des jeux de tests de la tâche validera alors la conformité des développements.

Chacun des tests ne doit s’attacher qu’à un aspect unique de la spécification. Par exemple, si la fonctionnalité d’ajout d’utilisateur de notre application est spécifiée ainsi :

L’ajout d’un utilisateur se fait à l’aide d’un nom d’utilisateur et d’un mot de passe
Le nom d’utilisateur ne doit pas déjà être présent dans le système auquel cas, l’exception UsernameAlreadyUsedException est levée.
Le nom d’utilisateur ou le mot de passe ne doivent pas être nuls et de 8 caractères minimum auxquels cas l’exception UserPreconditionException est levée
Les tests seront alors au minimum un cas nominal (1), un cas pour vérifier si l’exception UsernameAlreadyUsedException est bien levée lorsque le nom d’utilisateur est déjà utilisé (2) et quatre autres cas pour vérifier que l’exception UserPreconditionException est levée lorsque le nom de l’utilisateur ou le mot de passe est nul, ou lorsque l’un des deux est inférieur à 8 caractères (3).

Nous voyons sur ce petit exemple apparaître quelques utilités des tests qui permettent, en plus de simplement détecter des défauts dans les développements :

de proposer un premier exemple d’utilisation du code, conformément aux spécifications. Quelque part, les tests agissent comme une documentation non négligeable du code.
d’apporter ensuite la certitude que la conformité aux spécifications sera vérifiée à chaque fois qu’ils seront exécutés (détection des régression). Donc valident les développements effectués et détectent les régressions,
Dans la suite des développement, les tests doivent être maintenus aux dernières version du code. Ainsi, chaque modification à apporter, que ce soit une mise à jour des spécifications, une correction de bug ou l’ajout d’une fonctionnalité doit être précédée par l’écriture et la refonte des tests correspondants.

Les tests faisant partie intégrante du projet, il convient de bien les structurer en réfléchissant au préalable à leur évolution. Ainsi, on évitera par exemple de coder « en dur » les comparaisons de chaînes de caractères et l’on préfèrera une approche plus modulaire. Dans un sens, l’ensemble des tests peuvent être vu comme un programme qui utilisera le projet de l’extérieur, comme de l’intérieur.

En conclusion, les tests pour le code et les spécifications m’apparaissent un peu comme l’expérimentation pour la théorie dans d’autres sciences telles que la physique. Le physicien a une idée (la spécification), propose des expérimentations pour illustrer sa théorie (les tests) puis, une fois l’idée vérifiée proposera un article détaillé et explicatif (le code). Ainsi, les tests apparaissent aujourd’hui inévitables pour tous les projets car comme la théorie et la vérification expérimentale, l’un ne peut exister sans l’autre.

