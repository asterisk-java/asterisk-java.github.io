---
author: srt
comments: true
date: 2007-03-22 23:36:00+00:00
layout: post
permalink: adding-support-for-asterisk-1-4-606
slug: adding-support-for-asterisk-1-4
title: Adding Support for Asterisk 1.4
wordpress_id: 606
tags:
- asterisk
- asterisk-java
---

The most important issue we have to resolve before we can release Asterisk-Java 0.3 is 
full support for Asterisk 1.4




The challenge is to find all changes. Unfortunately the Changelogs do not record all of them so the only way to go is looking through the whole source tree and checking all
events and actions for the Manager API and the supported requests for FastAGI.




Many thanks to Martin B. Smith who continued that work and provided support for
the GetConfig and UpdateConfig actions and is currently working on
[AJ-50](http://jira.reucon.org/browse/AJ-50).




You can also help us by providing feedback on what's still missing. Just post a
short comment to [AJ-50](http://jira.reucon.org/browse/AJ-50) and
tell us which new properties, actions, events or FastAGI changes you encountered.



