---
layout: post
title: UML reverse engineering using maven and UMLGraph
---

During the Design Phase of a Sofware Application you may use UML sketches, using a CASE tool but when the times goes you code more than sketch and likely those diagrams are outdate and don't fit the code. How didn't start to work in a new company and asked about arquitecture diagrams, or class diagrams and the answers was: the UML diagrams are outdated have a look on the code.

This a likely scenario that could be avoid, by using reverse engineering tool. One may disagree and suggest a round-trip engineering tool, and he's likely right but most of those tools are comercial and not suitable for all projects. 
An open source and easy to apply approach is [UMLGraph][umlgraph]. This a Javadoc doclet which reads javadoc annotations and draws UML Diagrams, ClassDiagram or even Sequence Diagram. The doclet also, can predict or infers the relationships from the code or by adding custom tags the diagrams can be refined.

One negative issue is that the project is not quite active the latest official release was in [May 2013](http://search.maven.org/#search|ga|1|umlgraph), the positive side is that the [snapshots](https://github.com/dspinellis/UMLGraph) are not that old, and Java 8 is seemed supported. One pretty straight forward solution is to build the doclet from sources or take the latest snapshot from [Download page](http://www.umlgraph.org/download.html) and copy and references it using docletPath tag for a maven integration.

> Note about UmlGraph: You must have the Graphviz binary in your PATH, or the images will not be generated. For more information about Graphviz, please refer to http://www.graphviz.org/

Ant Syntax

{% gist antoniomaria/61cb521dc85743068556 %}

Maven Syntax

{% gist antoniomaria/885558704946e51885b6 %}


References:

* [Official UMLGraph Site](http://www.umlgraph.org/)
* [Code examples UMLGraph Maven](https://github.com/antoniomaria/umlgraph-test)
* [Be a better developer](http://www.beabetterdeveloper.com/2013/03/automated-class-diagrams-using-maven.html)
* [Java dZone](http://java.dzone.com/articles/reverse-engineer-source-code-u)

[umlgraph]: http://www.umlgraph.org/