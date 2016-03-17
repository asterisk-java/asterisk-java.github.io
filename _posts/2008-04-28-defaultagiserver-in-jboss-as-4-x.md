---
author: srt
comments: true
date: 2008-04-28 02:05:29+00:00
layout: post
permalink: defaultagiserver-in-jboss-as-4-x-906/
slug: defaultagiserver-in-jboss-as-4-x
title: DefaultAgiServer in JBoss AS 4.x
wordpress_id: 906
tags:
- agi
- asterisk-java
- jboss
- mbean
---


![JBoss Logo](http://blogs.reucon.com/asterisk-java/images/jboss_logo.gif)
A recent post to the mailing list asked about how to stop and start a FastAGI server and how folks host Fast AGI servers. I shared some code I wrote for a [small MBean that starts and stops a DefaultAgiServer](http://asterisk-java.org/development/faq.html) from Asterisk-Java -- see the last FAQ question _"Can I have an example of using an AGI server in a container like JBoss?"_. The MBean uses the JBoss-specific @Management annotation.






I work on a home-grown call center management application (EJBs, JSP webpages, and two standalone Java Swing applications, all talking through JBoss Application Server), and we've already been able to add a couple features with Asterisk-Java that add value and utility to our application. I didn't want to introduce another service to our infrastructure and I also didn't want to write an entirely new Agi server, as Stefan had done a great job on that part. Thus, the above MBean was born.






Comments and suggestions and other examples of how you run your Agi scripts are welcome and encouraged on [our mailing lists.](http://asterisk-java.org/development/mail-lists.html)

