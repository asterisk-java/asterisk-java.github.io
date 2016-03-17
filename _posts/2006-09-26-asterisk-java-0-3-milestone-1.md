---
author: srt
comments: true
date: 2006-09-26 01:35:00+00:00
layout: post
permalink: asterisk-java-0-3-milestone-1-676/
slug: asterisk-java-0-3-milestone-1
title: Asterisk-Java 0.3 Milestone 1
wordpress_id: 676
tags:
- asterisk-java
---

Asterisk-Java 0.3 Milestone 1 has been released and is available from [http://asterisk-java.org/download/0.3-m1](http://asterisk-java.org/download/0.3-m1). The package name has been changed from net.sf.asterisk to org.asteriskjava and it makes use of Java 5 features so you need at least a JDK 1.5.





A whole bunch of new features has been added including support for SSL secured connections to the Manager API and the new org.asteriskjava.live package that handles call tracking and allows you to build applications like click2call very easily and without all the hassles involved in directly using the Manager API.





Here is the Changelog:





## Bug






  * [[AJ-17](http://jira.reucon.org/browse/AJ-17)] - call.getChannel() is null when using AsteriskManager.originateCall()


  * [[AJ-25](http://jira.reucon.org/browse/AJ-25)] - Timing issue with ResourceBundleMappingStrategy


  * [[AJ-27](http://jira.reucon.org/browse/AJ-27)] - ManagerReader Interrupt


  * [[AJ-31](http://jira.reucon.org/browse/AJ-31)] - getParameter() Bug


  * [[AJ-32](http://jira.reucon.org/browse/AJ-32)] - Incorrect usage of ConnectEvent


  * [[AJ-33](http://jira.reucon.org/browse/AJ-33)] - no setter for the dnd field


  * [[AJ-34](http://jira.reucon.org/browse/AJ-34)] - redirect action for 2 channels not works


  * [[AJ-36](http://jira.reucon.org/browse/AJ-36)] - Bug with CommandAction: result is overwritten each time


  * [[AJ-37](http://jira.reucon.org/browse/AJ-37)] - Default CompositeMappingStrategy doesn't honor fastagi-mapping.properties


  * [[AJ-39](http://jira.reucon.org/browse/AJ-39)] - Missing property "callerId" on ExtensionStatusEvent


        


## New Feature






  * [[AJ-28](http://jira.reucon.org/browse/AJ-28)] - Add support for login with eventMask


  * [[AJ-29](http://jira.reucon.org/browse/AJ-29)] - Add support for non-shared instances to ResourceBundleMappingStrategy and ClassNameMappingStrategy





## Task






  * [[AJ-18](http://jira.reucon.org/browse/AJ-18)] - Change to maven2


  * [[AJ-19](http://jira.reucon.org/browse/AJ-19)] - Change package name to org.asteriskjava


  * [[AJ-26](http://jira.reucon.org/browse/AJ-26)] - Fix @version javadoc tags which are broken since moving to svn





Documentation for 0.3-m1 is available at [http://asterisk-java.org/0.3-m1/](http://asterisk-java.org/0.3-m1/).





Asterisk-Java 0.3 will be released with the release of Asterisk 1.4.



