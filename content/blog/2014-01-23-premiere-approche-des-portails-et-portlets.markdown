---
layout: post
title: "Première approche des portails et portlets"
date: "2014-01-23 13:55"
author:
categories: []
comments: true
published: false
---

Cet article fait suite à la conférence de Christophe Laprun sur JBoss Gatein et Portlets 2.0 qui a eu lieu le 27/09/2010 à l’alpesjug et dresse une vision d’ensemble de ce qu’est un portail et de quelques spécificités des portlets.

Un portail est une technologie qui permet de rassembler au sein d’une même interface web, un ensemble d’applications : les portlets. A l’instar des applications web, un portlet se construit comme une archive WAR dont un fichier de configuration (portlet.xml) précise la façon dont il doit être utilisée et est déployé au sein d’un serveur de portlets : le portail.
 Pour déployer cette archive, il suffit alors de la déposer dans le dossier prévu par le portail. Dans le cas de GateIn par exemple, lorsque déployé sous JBoss AS, l’archive doit être déposée dans le dépôt de déploiement de JBoss AS.

La spécification Portlet est pour l’instant divisée en deux textes :

Portlet 1.0 -- JSR-168 : la spécification initiale. Elle définit le modèle à composants de base. Cependant, elle souffre d’un certain nombre de problèmes (pas de dialogue entre les portlets, pas de solution élégante pour la gestion des resources, …), pour la plupart corrigés avec Portlet 2.0.
Portlet 2.0 -- JSR-286 : spécification plus récente destinée à corriger les problèmes soulevés par la JSR-168. Elle apporte le partage des paramètres (PRP), les évènements, les filtres et une gestion des ressources plus élégante.
Ces deux spécifications prévoient d’héberger les portlets localement au portail. L’OASIS a spécifié WSRP (WebService for Remote Portlet) qui propose d’invoquer un portlet distant au dessus de SOAP. Il n’existe pas, à l’heure actuelle, de standard concernant REST ou d’autres méthodes d’invocation distante, bien que certaines propositions puissent être implantées dans les différents portails du marché.

Revenons rapidement sur quelques fonctionnalités des portlets 2.0.

Nous parlions plus tôt de PRP, le partage de paramètres. Un paramètre est défini par un type primitif, et une valeur. Lorsque plusieurs portlets acceptent un paramètre dont le type et l’identifiant correspondent, si l’on modifie la valeur de ce paramètre sur l’une des portlets, alors cette valeur est diffusée de la même façon aux autres portlets. Par exemple, un portlet qui affiche la météo et une autre qui affiche la photo satellite de la zone à partir du code postal seront mis à jour en même temps selon si le code postal est entré sur l’une ou l’autre des portlets.

Les évènements sont une notion voisine qui permet d’aller un peu plus loin que les portlets, en manipulant par exemple un type plus complexe, défini comme une classe java. Par exemple, avoir plusieurs portlets qui manipulent une entité correspondant au client d’un site de e-commerce.

La dernière fonctionnalité dont nous n’avons pas parlé jusqu’alors mais qui est l’une des plus intéressante est l’identification de l’utilisateur. Un portail permet d’identifier le visiteur une seule fois (à l’aide de SSO) et propage l’identité aux différentes applications hébergées.

Avant de cloturer cet article, notons que portlet est un nom masculain d’après le grand dictionnaire terminologique.

Maintenant que nous avons dressé une rapide vue d’ensemble, il ne reste plus qu’à mettre les mains dans le cambouis, mais ce sera pour une autre fois…

