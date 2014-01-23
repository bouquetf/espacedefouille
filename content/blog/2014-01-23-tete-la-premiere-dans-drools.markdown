---
layout: post
title: "Tête la premiere dans drools"
date: "2014-01-23 13:56"
author:
categories: []
comments: true
published: false
---

Jboss Drools est un moteur de règles métier intéressant mais l’aborder semble une tâche ardue. Plutôt que de se laisser intimider, plongeons la tête la première dans l’outil, de son téléchargement à son utilisation, jusqu’à ce qui m’intéresse en dernier lieu : le piloter avec Bonita.

Où commencer ?

Sur http://www.jboss.org/drools. Ici, nous avons visiblement le choix entre 5 projets :

Drools Guvnor : pour la gestion des règles métier
Drools Expert : le moteur de règles
jBPM 5 : le BPMS de jboss
Dools Fusion : pour la gestion d’évènements métier. Cela semble s’apparenter à un bus d’évèments
Drools planner : un plannificateur automatique (recherche opérationnelle inside emoticon_smile)
Je pense que pour commencer, Drools guvnor est la bonne solution :

Guvnor is the web application and repository to govern Drools and jBPM assets

Téléchargement effectué, que nous réserve le manuel de référence ?
 Le quickstart tour part du principe que l’installation de drools a été effectuée donc …

Installation de Drools Guvnor

A l’heure où j’écris ces lignes, la dernière version stable est la 5.2.0, donc c’est sur l’installation de cette version que nous allons couvrir. RDV au chapitre 13 du manuel de référence.

Guvnor est fourni comme un fichier .war, déployons le sous un apache tomcat. Dans les grandes lignes :

Télécharger et extraire une archive de tomcat (disons la dernière version 6 stable)
Copier guvnot (binaries/guvnor-5.2.0.Final-tomcat-6.0.war) dans le dossier webapps de tomcat
Lancer le tomcat
Se connecter à http://localhost:8080/guvnor (j’ai renommé le fichier .war en guvnor.war pour me simplifier la vie)
Et installons un dépôt d’exemple en cliquant au prompt sur « Yes, please install samples »

L’exemple vient avec un modèle et un ensemble de règles pour nous aider à prendre en main l’outil. L’interface présente à gauche les grandes fonctionnalités, ici seule l’administration et la base de connaissance (knowledge base) nous intéressent pour l’instant.

Nous avons à l’heure actuelle une configuration de base sur le projet exemple, cependant, pour un cas réel, il nous faut une configuration de base et écrire des règles. Ainsi :

Configuration de base

Créer une catégorie pour le projet (administration->categories)
Créer un package pour le projet (knowledge base->create new->package)
Uploader le modèle de données (une librairie java .jar)
Nous sommes maintenant prêt à définir nos règles métier

Ecrire des règles

Dans knowledge base : create new->new rule
Définir un nom pour la règle
Définir une catégorie (un tag)
Etablir une règle métier à l’aide du DSL correspondant
Ces quelques lignes se sont concentrées sur les grands composants de Drools, ainsi que l’installation du moteur de règle métier et l’interface utilisateur par défaut.
 D’autres articles seront à venir sur le vocabulaire intrasèque à Drools et son utilité réelle, sur des exemples concrets d’utilisation et sur l’utilité d’un moteur de règle en relation avec un BPMS. Bien entendu, au fur et à mesure que l’on plongera dans l’exploration du domaine des règles métier, nous rentrerons plus en détail dans les choses techniques qui régissent l’outil.

