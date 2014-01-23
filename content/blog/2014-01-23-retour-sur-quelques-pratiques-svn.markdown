---
layout: post
title: "Retour sur quelques pratiques SVN"
date: "2014-01-23 13:57"
author:
categories: []
comments: true
published: false
---

Cet article fait suite à celui qui offrait un retour sur l’organisation d’un dépôt SVN. Il s’agit ici de présenter quelques pratiques comme comment fusionner (merge) une branche avec le trunk, comment revenir à une ancienne révision, comment corriger proprement un bug ou encore comment sortir une release d’un projet.

Il arrive souvent, lorsque l’on désire tester une nouvelle technologie de vouloir faire des expérimentations dans un répertoire à part et ensuite intégrer les changements s’il s’avère qu’ils conviennent à la suite du développement. Une branche paraît ici appropriée. Pour SVN, une branche n’est autre qu’une copie du trunk dans le dossier branches qui suit un développement parallèle. Pour ce faire, il convient d’utiliser la commande suivante :
 svn copy -m "Branche experimentale GWT" https://<depotsvn>/trunk https://<depotsvn>/branches/TEST-GWT

Afin de basculer (switch) le répertoire de travail du trunk vers la branche, la commande switch s’utilise de la façon suivante :
 svn switch https://<depotsvn>/branches/TEST-GWT
 Une alternative est de faire un checkout des sources à partir de la branche dans un autre répertoire.

Une fois que les expérimentations conviennent, il peut être intéressant de fusionner la branche au trunk ainsi :
 svn switch https://<depotsvn>/trunk
 svn merge https://<depotsvn>/trunk https://<depotsvn>/branches/TEST-GWT
 Après que les possibles conflits soient résolus, il est nécessaire de commiter les changements.

A force de modifications sur une branche ou dans le trunk, il arrive qu’à un moment, on s’aperçoive qu’un certain nombre de commits n’auraient pas du être effectués. A ce moment, nous aimerions revenir à une révision antérieure pour continuer le code à partir de celle-ci. Ceci peut être effectué dans le répertoire de travail ainsi :
 svn merge -rHEAD:rxxx .
 Où xxx doit biensûr être remplacé par le numéro de révision auquel revenir. Ici aussi, un commit est nécessaire pour informer SVN de repartir de cette version des sources.

Une fois le projet arrivé à une version stable, il est courant d’en sortir une release qui sera distribué. En langage subversion, cela consiste en :

La création d’un tag pour marquer l’état des sources à la sortie de la release
La création d’une branche pour les corrections de bugs
Voyons comment procéder.
 Tout d’abord, il convient de créer la branche pour héberger la release. Celle-ci n’est qu’une copie du trunk :

svn copy -m "Release branch xxx" https://<depotsvn>/trunk https://<depotsvn>/branches/RB-xxx

Cette branche servira à préparer la release en mettant à jour le code (fixer les noms de version, les paramètres, …). Une fois que tout est correctement modifié, que la release est prête à être livrée, un tag peut y être assigné. Encore une fois, il s’agit d’une copie :
 svn copy -m "Release xxx" https://<depotsvn>/branches/RB-xxx https://<depotsvn>/tags/REL-xxx

L’extraction des sources sans les informations svn, le code livrable en somme, se fait ensuite à l’aide de la commande export :
 svn export https://<depotsvn>/tags/REL-xxx projet-vxxx

La vie d’un projet ne s’arrête cependant pas à la sortie de la release. Des bugs interviennent régulièrement et nécessitent d’être corrigés. Lorsqu’un bug est reporté, un numéro y est associé, généralement par l’outil de suivi de bug. Admettons que notre branche 1.0 s’est vue attribuée le bug 3234. La première étape est de récupérer le code associé à cette branche.
 Dans le cas général, la correction d’un bug ne nécessite qu’un minimum de travail. Ainsi, ils peuvent être directement corrigés dans la branche courante. Une fois la correction effectuée et commitée, le tour est joué. Il est souvent intéressant de reporter la correction dans le trunk. Admettons que le bug a été découvert à la release 123 et corrigé à la release 124 de la branche RB-1.0, il convient d’aller dans le répertoire de travail associé aux sources du trunk et d’y taper la commande suivante pour mettre à jour les sources :

svn merge -r123:124 https://<depotsvn>/branches/RB-1.0 .

Si tout se passe bien, il ne reste plus qu’à commiter les changements.

Certains bugs peuvent parfois nécessiter plus d’efforts. La procédure classique dans ce cas est de créer une branche dédiée à leur correction et de répercuter ensuite les changements sur la release branch et sur le trunk.
 Ainsi, la première étape consiste à créer la branche pour corriger le bug :
 svn copy -m "bugfix branch 3234" https://<depotsvn>/branches/RB-1.0 https://<depotsvn>/branches/BUG-3234
 Une bonne pratique est de tagger le début de la correction :
 svn copy -m "Tag start of bug fix 3234" https://<depotsvn>/branches/BUG-3234 https://<depotsvn>/tags/PRE-3234
 A ce moment, le travail de correction peut commencer dans la branche. Une fois terminé, le bugfix peut être taggé :
 svn copy -m "Tag end of bug fix 3234" https://<depotsvn>/branches/BUG-3234 https://<depotsvn>/tags/POST-3234
 La dernière étape consiste simplement à répercuter les changements dans les répertoires de travail de la release branch et dans celui du trunk, puis de commiter après avoir vérifié que les tests passent :
 svn update
 svn merge https://<depotsvn>/tags/PRE-3234 https://<depotsvn>/tags/POST-3234
 svn commit -m "Merged bug fix for bug 3234"

Ces deux articles sur SVN ont été grandement inspirés par les articles de 2006 et 2007 du blog de Ariejan de Vroom et du svnbook.