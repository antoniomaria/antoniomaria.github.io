---
layout: post
title: UML reverse engineering using maven and UMLGraph
---

During the Design Phase of a Sofware Application you may use UML sketches, using a CASE tool but when the times goes you code more than sketch and likely those diagrams are outdate and don't fit the code. How didn't start to work in a new company and asked about arquitecture diagrams, or class diagrams and the answers was: the UML diagrams are outdated have a look on the code.

This a likely scenario that could be avoid, by using reverse engineering tool. One may disagree and suggest a round-trip engineering tool, and he's likely right but most of those tools are comercial and not suitable for all projects. 
An open source and easy to apply approach is [UMLGraph][umlgraph]. This a Javadoc doclet which reads javadoc annotations and draws UML Diagrams, ClassDiagram or even Sequence Diagram. The doclet also, can predict or infers the relationships from the code or by adding custom tags the diagrams can be refined.

One negative issue is that the project is not quite active the latest official release was in [May 2013](http://search.maven.org/#search|ga|1|umlgraph), the positive side is that the [snapshots](https://github.com/dspinellis/UMLGraph) are not that old, and Java 8 is seemed supported. One pretty straight forward solution is to build the doclet from sources or take the latest snapshot from [Download page](http://www.umlgraph.org/download.html) and copy and references it using docletPath tag for a maven integration.

> Note about UmlGraph: You must have the Graphviz binary in your PATH, or the images will not be generated. For more information about Graphviz, please refer to http://www.graphviz.org/

{% gist antoniomaria/61cb521dc85743068556 %}

```xml
  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-javadoc-plugin</artifactId>
    <version>2.9</version>
    <configuration>
      <tags>
        <tag>
          <name>depend</name>
          <placement>X</placement>
        </tag>
        <tag>
          <name>hidden</name>
          <placement>X</placement>
        </tag>
        <tag>
          <name>opt</name>
          <placement>X</placement>
        </tag>
      </tags>
      <doclet>org.umlgraph.doclet.UmlGraphDoc</doclet>
      <docletPath>C:/Users/antonio/git/UMLGraph/lib/UmlGraph.jar</docletPath>
      <additionalparam>-inferrel</additionalparam>
      <additionalparam>-inferdep</additionalparam>
      <additionalparam>-collapsible</additionalparam>
      <additionalparam>-hide java.*</additionalparam>
      <additionalparam>-collpackages</additionalparam>
      <additionalparam>-qualify</additionalparam>
      <additionalparam>-postfixpackage</additionalparam>
      <additionalparam>-nodefontsize 9</additionalparam>
      <additionalparam>-nodefontpackagesize 7</additionalparam>
      <additionalparam>-link http://docs.oracle.com/javase/7/docs/jdk/api/javadoc/doclet/</additionalparam>
      <additionalparam>-link http://download.oracle.com/javase/7/docs/api/</additionalparam>
      <useStandardDocletOptions>true</useStandardDocletOptions>          
    </configuration>
  </plugin>
```

To execute the plugin
    mvn javadoc:javadoc

References:

* [Official UMLGraph Site](http://www.umlgraph.org/)
* [Code examples UMLGraph Maven](https://github.com/antoniomaria/umlgraph-test)
* [Be a better developer](http://www.beabetterdeveloper.com/2013/03/automated-class-diagrams-using-maven.html)
* [Java dZone](http://java.dzone.com/articles/reverse-engineer-source-code-u)

[umlgraph]: http://www.umlgraph.org/