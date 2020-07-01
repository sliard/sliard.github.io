---
author: Samuel
categories:
  - Java
date: 2008-09-11 08:05:44+00:00
guid: http://www.net-liard.com/blog/?p=36
id: 111
permalink: /2008/09/fuite-de-threads-dans-jonas/
tags:
  - Fuite de threads
  - JMS
  - Jonas
  - Joram
  - thread
title: Fuite de threads dans Jonas
url: /2008/09/11/fuite-de-threads-dans-jonas/
---

Depuis plusieurs mois nous avions détecté que le nombre de thread de notre serveur jonas augmentait sans arrêt. Un de mes collègues a donc pris le taureau par les cornes pour trouver l&#8217;origine du problème. Après 4 jours à fouiller dans le code source de Jonas, il a trouvé le problème au niveau du connecteur Joram (notre application utilise des JMS).

Dans la classe
  
org.objectweb.joram.client.connector.ManagedConnectionFactoryImpl, on peut lire :

<pre name="code" class="java:nogutter:nocontrols">public Set getInvalidConnections(Set connectionSet) throws ResourceException {
  if (AdapterTracing.dbgAdapter.isLoggable(BasicLevel.DEBUG))
    AdapterTracing.dbgAdapter.log(BasicLevel.DEBUG,
       this+" getInvalidConnections("+connectionSet+")");
    Iterator it = connectionSet.iterator();
    ManagedConnectionImpl managedCx;
    while (it.hasNext()) {
      try {
        managedCx = (ManagedConnectionImpl) it.next();
        if (managedCx.isValid())
          connectionSet.remove(managedCx);
        }
      catch (ClassCastException exc) {}
  }
  return connectionSet;
}</pre>

Ca met en évidence deux règles de codage Java importantes qui ne sont pas respectées :

  1. Ne pas retourner la référence d&#8217;un paramètre en valeur de retour
  2. Eviter de modifier un paramètre d&#8217;une méthode

<div>
  La méthode getInvalidConnections permet de chercher dans la liste de connexions passées en paramètre celles qu&#8217;il faut libérer. Mais au lieu de mettre les connexions invalides dans une nouvelle collection, ils suppriment les connexions valides de la collection passée en paramètre. Du coup ces connexions ne sont plus dans la liste des connexions actives, elles ne seront donc jamais libérées.
</div>

Depuis que nous avons patché le connecteur Joram, nous n&#8217;avons plus de fuite de thread :)

Le patch :

<pre name="code" class="java:collapse:nogutter">public Set getInvalidConnections(Set connectionSet) throws ResourceException {
  if (AdapterTracing.dbgAdapter.isLoggable(BasicLevel.DEBUG))
    AdapterTracing.dbgAdapter.log(BasicLevel.DEBUG,
      this+" getInvalidConnections("+connectionSet+")");
  Iterator it = connectionSet.iterator();
  ManagedConnectionImpl managedCx;
  java.util.HashSet invalidConnections = new java.util.HashSet();
  while (it.hasNext()) {
    try {
      managedCx = (ManagedConnectionImpl) it.next();
      if (!managedCx.isValid())
        invalidConnections.add(managedCx);
    }
    catch (ClassCastException exc) {}
  }
  return invalidConnections;
}</pre>