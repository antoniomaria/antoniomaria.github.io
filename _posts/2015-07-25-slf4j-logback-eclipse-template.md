---
layout: post
title: Eclipse SLF4J (logback) template
---

Eclipse template are really useful, one application could be create the Logger declaration at the beginning of every class:

Java > Editor > Templates > New

    ${:import(org.slf4j.LoggerFactory,org.slf4j.Logger)}
    /**
      * Logger.
     */
    private static final Logger logger  = LoggerFactory.getLogger(${enclosing_type}.class);
    
