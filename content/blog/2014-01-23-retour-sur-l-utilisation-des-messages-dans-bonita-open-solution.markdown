---
layout: post
title: "Retour sur l?'utilisation des messages dans Bonita Open Solution"
date: "2014-01-23 13:56"
author:
categories: []
comments: true
published: false
---

L’utilisation et la configuration des messages est souvent quelque chose de mal
 compris par les utilisateurs de BOS. Le but de cet article est de
 reprendre ces notions pour tenter d’éclaircir les choses.

Quelques rappels sur les messages

Les messages permettent à deux processus de communiquer entre eux, et
 éventuellement faire transiter de l’information. Les propriétés des messages
 sont les suivantes :

Un message est unique : une fois traité, le message est détruit
Un message doit avoir une cible unique : un message ne peut être envoyé qu’à
 un processus donné
Un message ne peut relier deux évènements du même processus
L’envoi et la réception de message se fait par l’intermédiaire d’évènements
 d’envoi ou de réception de messages. L’envoi de messages peut se faire en
 cours de processus ou en fin de processus. La réception peut intervenir en
 cours d’exécution ou pour débuter un processus.

Evènements relatifs aux messages







Des tâches d’envoi et de réception de messages existent et agissent de la même façon que les évènements correspondants.

Tâches d'envoi et de réception de messages







L’évènement d’envoi de messages peut envoyer un ou plusieurs messages alors que
 la réception ne peut traiter qu’un message donné. L’évènement de réception peut
 éventuellement filtrer le message à traiter à l’aide d’une condition. cela
 permet de cibler précisément le cas ciblé.

Configuration de l’envoi et la réception de messages

La première étape est de modéliser deux processus qui vont communiquer entre eux en faisant apparaître les évènements d’envoi et de réception de messages.

Ajout des évènements dans le diagramme

Il ne reste plus qu’à ajouter un message :

sélectionner l’évènement d’envoi de processus et dans les détails Général->Message
Sélection de l'envoi de messages
Ajouter le message
configurer le message en définissant son nom, le processus cible ainsi que la tâche de réception
Configuration du message

Faire transiter les données

Pour faire transiter des données d’un processus l’un autre, il convient de
 créer des variables locales au message pour copier la valeur qui nous intéresse.

En pratique :

Tout d’abord, il faut ajouter une variable locale au message en éditant le
 message que l’on vient de créer :

Et de configurer la variable locale au message en l’initialisant avec la valeur
 de la variable du processus émetteur

Ajout des données

A ce stade, le message contient la donnée qui nous intéresse, mais à la

réception, il nous reste à transférer cette valeur au processus cible. Pour
 cela, il suffit d’utiliser un connecteur Bonita pour mettre à jour la ou les
 variables correspondantes (set variable(s)) dans le processus cible :

Sélectionner l’évènement de réception du message
Réception évènement réception message

Ajouter un connecteur en allant dans l’onglet général->Connecteurs->Ajouter…
Connecteur mise à jour de variables

Puis configurer le connecteur avec le nom de la variable cible et la valeur à lui donner
Mise à jour de variables

4. Corrélation cas/message



J’en parlais en introduction, un message doit avoir un cas cible. Or, lors de
 sa définition, il n’est précisé que le processus et la tâche cible. Le filtrage
 sur le cas doit se faire dans l’évènement de réception de message avec la
 condition de réception.
 Cette condition permet de comparer une valeur contenue dans le message avec une
 valeur du processus cible. Cela permet par exemple de s’assurer que le dossier
 dont l’information est contenue dans le message est bien envoyé au cas affecté
 à son traitement.

Pour effectuer la corrélation entre un cas et un message reçu :

sélectionner l’évènement de réception du message
paramétrer la condition de réception du message
Corrélation

