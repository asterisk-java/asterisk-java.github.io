---
author: srt
comments: true
date: 2009-07-09 15:52:00+00:00
layout: post
permalink: asterisk-java-sync-to-maven-central-repo-386
slug: asterisk-java-sync-to-maven-central-repo
title: Asterisk-Java Sync to Maven Central Repo
wordpress_id: 386
tags:
- asterisk-java
- maven
---


The released Asterisk-Java artifacts are now automatically published to Maven's central repository. This includes our milestone releases 1.0.0-m1 and 1.0.0-m2. 



If you are already using Maven for development that means to you that you no longer have to download Asterisk-Java in order to use it. You can just declare a dependency and Maven automatically downloads it from central.



The Maven coordinates for Asterisk-Java are:




    
    
    <dependency>
      <groupId>org.asteriskjava</groupId>
      <artifactId>asterisk-java</artifactId>
      <version>1.0.0-m2</version>
    </dependency>
    
