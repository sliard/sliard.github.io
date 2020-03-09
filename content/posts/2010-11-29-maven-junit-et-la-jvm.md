---
author: Samuel
categories:
  - Java
date: 2010-11-29 09:56:23+00:00
guid: http://www.net-liard.com/blog/?p=751
id: 751
permalink: /2010/11/maven-junit-et-la-jvm/
tags:
  - Java
  - JUnit
  - Maven
title: Maven, JUnit et la JVM
url: /2010/11/29/maven-junit-et-la-jvm/
---

Ca fait longtemps que je n&#8217;ai pas fait de petit post technique où je decris la solution d&#8217;un problème simple. Et bien justement j&#8217;ai eu à en résoudre quelques uns ces derniers temps. Je vais donc les partager.

En ce moment je travaille sur un projet qui charge beaucoup d&#8217;objets en mémoire. Il faut donc redéfinir la taille de mémoire max à allouer pour le faire tourner. Une simple option &#8220;-Xmx512m&#8221; au niveau de la JVM et les tests unitaires fonctionnent sans pb. Mais comment faire lorsqu&#8217;on lance les tests avec Maven ?

La première solution est de redéfinir une variable d&#8217;environnement :  
  
**MAVEN_OPTS=-Xmx512m**

Mais dans ce cas chaque personne reprenant mon projet va devoir redéfinir cette variable. Pour moi ce n&#8217;est pas viable. En cherchant encore j&#8217;ai trouvé comment définir cela dans le pom :

<pre name="code" class="xml:nogutter:nocontrols">&lt;plugin>
    &lt;groupId>org.apache.maven.plugins&lt;/groupId>
    &lt;artifactId>maven-surefire-plugin&lt;/artifactId>
    &lt;configuration>
        &lt;argLine>-Xmx512m&lt;/argLine>
    &lt;/configuration>
&lt;/plugin></pre>

Et la ça fonctionne très bien.

Malheureusement j&#8217;avais un second problème. Je fais des tests avec des comparaisons de chaînes de caractères qui contiennent des accents. Et là encore sous Eclipse pas de problème mais en ligne de commande ça ne fonctionnait pas. En plus j&#8217;avais un Warning :
  
`[WARNING] Using platform encoding (MacRoman actually) to copy filtered resources, i.e. build is platform dependent!`

Pour corriger le Warning j&#8217;ai ajouter dans le pom :

<pre name="code" class="xml:nogutter:nocontrols">&lt;properties>

    &lt;project.build.sourceEncoding>ISO-8859-1&lt;/project.build.sourceEncoding>
&lt;/properties></pre>

Et pour que mes JUnit fonctionnent j&#8217;ai encore ajouté deux paramètres :

<pre name="code" class="xml:nogutter:nocontrols">&lt;build>
  &lt;plugins>
    &lt;plugin>
      &lt;groupId>org.apache.maven.plugins&lt;/groupId>
      &lt;artifactId>maven-surefire-plugin&lt;/artifactId>
      &lt;configuration>
        &lt;argLine>-Xmx512m -Dfile.encoding=ISO-8859-1&lt;/argLine>
      &lt;/configuration>
    &lt;/plugin>
    &lt;plugin>
      &lt;groupId>org.apache.maven.plugins&lt;/groupId>
      &lt;artifactId>maven-compiler-plugin&lt;/artifactId>
      &lt;configuration>
        &lt;target>1.5&lt;/target>
        &lt;source>1.5&lt;/source>
        &lt;encoding>ISO-8859-1&lt;/encoding>
      &lt;/configuration>
    &lt;/plugin>
  &lt;/plugins>
&lt;/build></pre>