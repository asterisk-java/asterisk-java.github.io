---
author: srt
comments: true
date: 2007-07-01 21:45:00+00:00
layout: post
permalink: asterisk-java-0-3-726/
slug: asterisk-java-0-3
title: Asterisk-Java 0.3
wordpress_id: 726
tags:
- asterisk-java
- release
---

Asterisk-Java 0.3 has been released and is available from [http://asterisk-java.org/download/0.3](http://asterisk-java.org/download/0.3).




Asterisk-Java 0.3 is the new stable release with full support for
Asterisk 1.4 and the new Live API (org.asteriskjava.live).
The Live API takes care of the lowlevel action and event handling
of the Manager API and offers an intuitive API for Java developers.
Asterisk-Java takes advantage of the features of Java 5.0 and therfore
requires a Java Virtual Machine of at least version 1.5.0.






Here is the Changelog:





## Bug






  * [[AJ-30](http://jira.reucon.org/browse/AJ-30)] - Version detection does not work when restarting Asterisk


  * [[AJ-59](http://jira.reucon.org/browse/AJ-59)] - Incorrect class and method names when using JavaLoggingLog


  * [[AJ-60](http://jira.reucon.org/browse/AJ-60)] - DefaultManagerConnection.sendEventGeneratingAction() doesn't work with Asterisk 1.4.1


    


## Improvement






  * [[AJ-50](http://jira.reucon.org/browse/AJ-50)] - Support for Asterisk 1.4


  * [[AJ-54](http://jira.reucon.org/browse/AJ-54)] - AsteriskQueue observer and Park events fixes


  * [[AJ-55](http://jira.reucon.org/browse/AJ-55)] - Add "videoSupport" and "realtimeDevice" to PeerEntryEvent


  * [[AJ-56](http://jira.reucon.org/browse/AJ-56)] - Add "callerIdNum" to AbstractChannelEvent


  * [[AJ-57](http://jira.reucon.org/browse/AJ-57)] - Add "memberName" to AbstractQueueMemberEvent


  * [[AJ-58](http://jira.reucon.org/browse/AJ-58)] - Support for OpenPBX


    


## New Feature






  * [[AJ-43](http://jira.reucon.org/browse/AJ-43)] - Support GetConfig and UpdateConfig actions


  * [[AJ-62](http://jira.reucon.org/browse/AJ-62)] - Add executeCliCommand() method to AsteriskServer


    


## Task






  * [[AJ-2](http://jira.reucon.org/browse/AJ-2)] - Update design doc and tutorial according to AGI changes





Thanks to Martin B. Smith for working on Asterisk 1.4 support and fixing the remaining issues





Documentation for 0.3 is available at [http://asterisk-java.org/0.3/](http://asterisk-java.org/0.3/).
