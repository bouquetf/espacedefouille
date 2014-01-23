---
layout: post
title: "Administration web de dépôts mercurial avec rhodecode"
date: "2014-01-23 13:56"
author:
categories: []
comments: true
published: false
---

Mercurial (hg pour les intimes) est un outil de gestion de sources distribué à l’instar de git, développé en python. L’avantage que l’on peut lui trouver est sa simplicité d’utilisation, son port sur les systèmes d’exploitation les plus répandus et son extensibilité aisée.

Cet article a pour objet l’installation et la configuration de rhodecode, une application web permettant d’administrer de multiples dépôts mercurial.

Mise en place de rhodecode

Les manipulations ont été effectuées sur un serveur archlinux. Pour d’autres distributions/OS, la procédure reste équivalente.

Versions utilisées

mercurial mercurial 1.9.1
pip 1.0.2
Procédure

Installer rhodecode
pip install rhodecode
Créer l’utilisateur rhodecode et se logger en tant que tel et créer le répertoire pour les dépôts
useradd -m rhodecode
su - rhodecode
mkdir repos
Créer le fichier de configuration
paster make-config RhodeCode production.ini
Configuration de base
paster setup-app production.ini
Il ne reste alors plus qu’à lancer le serveur :

paster serve production.ini
Note importante : le serveur écoute en local sur le port 5000. Pour écouter à l’extérieur ou sur un autre port, deux solutions :

Editer le fichier production.ini afin de changer l’IP et le port d’écoute
Mettre en place un proxy http pour rediriger les requêtes
Liens utiles

Mercurial
RhodeCode
