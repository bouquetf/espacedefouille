---
layout: post
title: "Où commencer son processus"
date: "2014-01-23 13:55"
author:
categories: []
comments: true
published: false
---

Très souvent, on en vient à se demander où commencer son processus, par quel bout prendre notre projet pour avoir une modélisation aisée et rapide. Cet article tente de répertorier plusieurs idées qui peuvent permettre de débuter sans trop de heurts pour aboutir rapidement à un prototype fonctionnel.

Qu’est-ce que l’on manipule ?

Un processus a pour objet la manipulation d’une notion métier. Plus loin, un processus sert à traiter une action sur un objet métier. Par exemple, dans le cadre de l’organisation d’une formation, nous pourrions avoir les processus suivants :

enregistrer une nouvelle formation,
enregistrer un nouveau participant à une session donnée,
suivre le payement d’un participant,
…
Chaque cas, chaque instance de processus représente une session de formation, un stagiaire, une facture, … qui interagissent ensembles pour former un projet global : la gestion des formations.

On commence où ? On obtient quoi ?

A partir de l’idée qu’un processus représente une action sur une notion métier, il convient de se demander où l’on commence le design.

L’idée principale là derrière, c’est que le cas est créé par un évènement métier bien défini. Par exemple, le cas (l’instance de processus) d’enregistrement du stagiaire M. Dupont est créé par son enregistrement sur le site web.

Et qu’est-ce qui termine le processus ? Un processus a un objectif métier, un état de l’objet métier manipulé. Pour notre enregistrement par exemple, ce sera une fin de processus « stagiaire enregistré », « stagiaire refusé », …  Les fins de notre processus correspondent donc à ces états vers lesquels nous arrivons. Ainsi, il n’est pas rare qu’un processus puisse avoir plusieurs fins, suivant l’état obtenu.

Et la gestion des risques dans tout ça ?

Un processus peut être vu comme la standardisation d’un projet récurrent. En gestion de projet, nous avons plusieurs façons de gérer les risques :

Tout se passe bien dans le meilleur des mondes, on ignore tout bonnement le risque : rien n’apparaît
On se débrouille pour ne jamais tomber dans le risque que l’on a identifié, auquel cas, la gestion de ce risque apparaîtra dans notre modèle
On identifie le risque et on le traite de façon exceptionnelle.
Ce dernier cas est ce que l’on pourrait qualifier d’erreur métier, notion qui est disponible dans la norme BPMN2 par exemple. Une erreur métier correspond à un risque identifié qui, s’il se produit, place mon cas dans un état d’erreur. Auquel cas, cette erreur est identifiée et il convient de définir un traitement particulier.

Mais une erreur métier, ça représente quoi exactement ? De base, il y en a de deux types :

une erreur qui survient au niveau technique et que l’on remonte au niveau métier. C’est le cas par exemple du cas où l’on doit récupérer l’information à traiter d’une base de donnée, mais que cette base de donnée est inaccessible, auquel cas, il faut définir une autre stratégie alternative de récupération de données, si elle est possible…
une erreur qui survient par le métier et impacte le métier. Par exemple, lors de la session de formation où le stagiaire ne se présente pas le premier jour.
Et comment prévoir l’imprévisible ?

Avant tout, rester pragmatique. Un processus est là pour automatiser la gestion de plusieurs cas. Si l’on traite 70% des cas, c’est déjà bien. La question, que fait on des cas restants ?
 Est-ce pertinent de traiter ces cas d’exception alors qu’ils n’interviennent qu’une fois tous les 10 ans ? Le retour sur investissement d’un tel développement est loin d’être évident. Auquel cas, autant ne pas le modéliser et agir le moment venu.

Oui, mais… J’ai un processus qui automatise tout mon système. Comment est-ce que je peux agir manuellement là où tout est automatisé ? Comment faites vous avec vos systèmes existants ? En général, vous décrochez votre téléphone pour le service informatique pour qu’il traite l’information exceptionnelle. Là c’est pareil, mais cela nécessite de concevoir vos processus de telle façon qu’il vous sera toujours possible de traiter ces cas d’exception.

Voici quelques idées qui pourraient vous aider :

Utiliser une base de donnée métier : ne pas stocker l’information dans le processus mais dans une base métier. Cela a aussi l’avantage de rendre ces données accessibles de l’extérieur
Utiliser des processus simples : c’est exactement ce que l’on disait en première partie, un processus par action sur un objet métier
Rester sur des processus le plus linéaires possibles. Après tout, la logistique nous apprend qu’un processus est une série d’actions qui débouchent sur un objectif métier précis, que si l’on traite les chemins alternatifs, on passe dans une gestion de projet, discipline beaucoup plus complexe
Ces quelques principes de base pourront, je l’espère, vous permettre de concevoir rapidement des processus utilisables, simples à maintenir, mais surtout, qui n’aboutissent pas à des plat de spaghetti. Revenir sur ces principes de base lorsque l’on commence à perdre pied, c’est souvent une façon de redevenir pragmatique et trouver une issue simple et rapide à la trop forte complexité dans laquelle nous nous égarons trop souvent.

