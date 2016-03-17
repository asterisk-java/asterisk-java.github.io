---
author: srt
comments: true
date: 2007-10-01 23:32:00+00:00
layout: post
permalink: using-asterisk-java-with-astmanproxy-876/
slug: using-asterisk-java-with-astmanproxy
title: Using Asterisk-Java with AstManProxy
wordpress_id: 876
tags:
- asterisk-java
- astmanproxy
---


[AstManProxy](http://www.voip-info.org/wiki/view/AstManProxy)
is a proxy application for the Asterisk Manager API that allows connecting multiple servers and clients through a central point of contact.






From a client perspective AstManProxy is almost transparent. Modified behavior includes a different protocol identifier and a changed logout message. Additionally AstManProxy does not correctly handle ActionIDs during the authentication phase.






Support for the protocol identifier of AstManProxy is available in Asterisk-Java since 0.3.1. The fix for the ActionID requires a modification of AstManProxy. Gaetan Minet has now done the work and provides a [patch](http://dev.mcit.be/various/astmanproxy-asterisk-java.html) to fix it.






Additionally you will find support for the server property in the latest [1.0.0-SNAPSHOT](http://asterisk-java.org/download/1.0.0-SNAPSHOT/)s of Asterisk-Java. This property is now available in [ManagerEvent](http://asterisk-java.org/development/apidocs/org/asteriskjava/manager/event/ManagerEvent.html) - the base class of all events in Asterisk-Java - and contains the name of the Asterisk server that sent the event.






Reference: [Gaetan Minet's patch to make AstManProxy work with Asterisk-Java](http://dev.mcit.be/various/astmanproxy-asterisk-java.html)

