---
author: Samuel
categories:
  - Java
date: 2009-06-24 20:38:00+00:00
guid: http://www.net-liard.com/blog/?p=403
id: 403
permalink: /2009/06/conflit-de-lib-apache-cxf-et-hibernate/
tags:
  - cglig
  - CXF
  - hibernate
  - Maven
  - NoClassDefFoundError
title: Conflit de lib Apache CXF et hibernate
url: /2009/06/24/conflit-de-lib-apache-cxf-et-hibernate/
---

Je viens de perdre pas mal de temps à faire fonctionner mon projet qui utilise hibernate et apache CXF pour exposer des WebServices.

Au moment de compiler j&#8217;avais l&#8217;erreur suivante :
  
`WARN: Nested in org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'sessionFactory' defined in class path resource [applicationContext.xml]: Invocation of init method failed; nested exception is java.lang.NoClassDefFoundError: org/objectweb/asm/CodeVisitor:<br />
at net.sf.cglib.core.KeyFactory$Generator.generateClass`

Au début ça me paraissait être un simple NoClassDefFound, mais la classe recherchée était bien dans mon CLASSPATH.

A force de chercher j&#8217;ai fini par comprendre que c&#8217;etait un problème d&#8217;incompatibilité de version de lib cglib. Il faut donc exclure la librairie cglib récupérée avec hibernate pour en prendre une nommée : cglib-nodep.

Voici comment faire dans votre fichier maven 2 :

<pre name="code" class="xml:nogutter:nocontrols">&lt;dependency>
    &lt;groupId>org.hibernate&lt;/groupId>
    &lt;artifactId>hibernate&lt;/artifactId>
    &lt;version>3.2.1.ga&lt;/version>
    &lt;exclusions>
        &lt;exclusion>
            &lt;groupId>cglib&lt;/groupId>
            &lt;artifactId>cglib&lt;/artifactId>
        &lt;/exclusion>
    &lt;/exclusions>
&lt;/dependency>
&lt;dependency>
    &lt;groupId>cglib&lt;/groupId>
    &lt;artifactId>cglib-nodep&lt;/artifactId>
    &lt;version>2.1_3&lt;/version>
&lt;/dependency>
</pre>