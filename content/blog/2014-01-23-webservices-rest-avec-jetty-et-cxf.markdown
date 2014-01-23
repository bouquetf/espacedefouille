---
layout: post
title: "Webservices REST avec Jetty et cxf"
date: "2014-01-23 13:56"
author:
categories: []
comments: true
published: false
---

Ce document explique sommairement comment établir un serveur pour partager des ressources REST.

Un webservice simple

Voici le code d’un service simple qui permet d’afficher « coucou » via un GET en se basant sur JAX-RS.

import javax.ws.rs.GET;
import javax.ws.rs.Path;

public class Resource {
 @GET
 @Path("/test")
 public  test() {
  return "coucou";
 }
}
Exposer une resource

Il convient maintenant d’exposer cette ressource à l’aide de cxf. Pour cela, les étapes les plus simples sont les suivantes :

Tout débute par la création d’un JAXRSServerFactoryBean : une fabrique de serveur REST
Il faut ensuite exposer la resource à l’aide de la resource à l’aide de  la méthode setResourceClasses
Il ne reste qu’à demander au serveur d’écouter avant de le créer.
Cela donne le code suivant :

public class startJetty {
 public static void main( args[]) {
  JAXRSServerFactoryBean sf = new JAXRSServerFactoryBean();

  sf.setResourceClasses(Resource.class);
  sf.setAddress("http://localhost:9080/");
  sf.create();

 }
}
Compiler et lancer

La seule chose à faire maintenant est de construire un pom.xml maven avec les dépendances nécessaires :

  <dependencies>
    <dependency>
    <groupId>org.apache.cxf</groupId>
    <artifactId>cxf-rt-frontend-jaxrs</artifactId>
    <version>2.5.0</version>
  </dependency>
  <dependency>
    <groupId>org.apache.cxf</groupId>
    <artifactId>cxf-rt-transports-http-jetty</artifactId>
    <version>2.5.0</version>
  </dependency>
</dependencies>
Le projet se lance maintenant avec la commande :

mvn exec:java -Dexec.mainClass="org.jaalon.simpleJettyServer.startJetty"
