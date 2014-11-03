---
layout: post
title: Alternative to maven release plugin
---

After reading this articule [http://java.dzone.com/articles/why-i-never-use-maven-release](http://java.dzone.com/articles/why-i-never-use-maven-release) I changed my way how to release new versions using maven.

    mvn versions:set -DnewVersion=0.5.4.1-RELEASE -DgenerateBackupPoms=false
