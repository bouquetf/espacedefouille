---
layout: post
title: "Les recorders dans bonita open solution"
date: "2014-01-23 13:56"
author:
categories: []
comments: true
published: false
---

Les recorders sont un service du moteur de Bonita qui permettent de d’enregistrer les différents évènements du moteur. Dans les grandes lignes, il s’agit simplement d’implémenter un service bonita pour écouter ce qui nous intéresse et y réagir en conséquence. L’implémentation par défaut fournie par Bonita est de stocker l’état Bonita dans la base de donnée journal. Une utilité étendue que l’on peut envisager à la première pensée est le log (savoir quand une tâche est démarrée, lorsque des acteurs sont assignés et qui ils sont, …). Ensuite, d’autres utilisations plus originales peut être envisagées comme envoyer un email aux candidats de chaque tâche créée.

Mettons donc les mains dans le cambouis.

La configuration

Les services du moteur se configurent dans le fichier bonita/server/default/conf/bonita-server.xml. Les recorders se chainent par leur déclaration dans la section chainer d’identifiant recorder.

<chainer name='recorder'>
    <!-- Implémentation des recorders à utiliser -->
    <ref object='journal' />
</chainer>
Et un recorder (disons org.jaalon.MyRecorder) se déclare ainsi :

<recorder class='org.jaalon.MyRecorder'>
    <arg><string value='un parametre' ></arg>
</recorder>
Et le code dans tout ça ?

Le code, c’est pas bien compliqué. La seule dépendance requise est le bonita-server-<version>.jar

Un recorder implémente la classe org.ow2.bonita.services.Recorder. Chaque méthode représente un évènement qui peut survenir dans le moteur ; son corps, le traitement correspondant.

public class MyRecorder implements Recorder {
  /* code du recorder */
}

Les paramètres de configuration fournis sont récupérés par le constructeur, par exemple, pour notre configuration plus haut

   message;
  public MyRecorder ( message) {
    this.message = message;
  }

Et réagir à un évènement ? Il s’agit simplement d’implémenter la méthode qui nous intéresse, par exemple, pour logger le fait qu’une instance est prête :

  public void recordTaskReady(ActivityInstanceUUID uuid,  candidates,
                               userId) {
    LOG.log(Level.INFO, "Activity "+uuid+" is ready");
  }

Et l’accès au moteur me direz vous ? Ici, il n’est plus rentable d’utiliser l’API publique du moteur, mais passer par l’environnement du moteur et manipuler les objets directement depuis l’intérieur. Tout se fait en passant par l’EnvTool. Pour certains cas, les méthodes accessibles à partir de l’API publique peuvent être pratiques, alors on utiliserait ici l’accesseur renvoyé par LocalAPIAccessorFactory.getStandardServerAPIAccessor()

Ainsi, pour récupérer la valeur d’une variable par exemple :

EnvTool.getAllQueriers().getProcessInstance(processUUID).getLastKnownVariableValues().get("myVariableName");
