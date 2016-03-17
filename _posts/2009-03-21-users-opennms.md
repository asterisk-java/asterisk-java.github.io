---
author: srt
comments: true
date: 2009-03-21 11:48:00+00:00
layout: post
permalink: users-opennms-546/
slug: users-opennms
title: 'Users: OpenNMS'
wordpress_id: 546
tags:
- users
---


![]({{ site.url }}/assets/2011/12/opennms_logo.png)[OpenNMS](http://www.opennms.org/) is an open source network management platform developed on the Java platform. It offers monitoring for a wide range of network devices and services.



As Asterisk becomes an important part of today's network infrastructure it becomes more important to be able to monitor it for outages and resource usage. Jeff Gehlbach of [The OpenNMS Group](http://www.opennms.com/) is the de facto maintainer of res_snmp and is working on improved monitoring for Asterisk with OpenNMS. His [slides](http://asterisk-java.org/static/OpenNMS%20and%20Asterisk.pdf) from a recent talk in Frankfurt provide a good overview of the effort.



In addition to monitoring Asterisk Jeff has also added support to send OpenNMS notifications through Asterisk. This allows staff to be notified by a phone call of any outages in the network. The notification module is based on Asterisk-Java and uses the originate feature of the Manager API along with a custom AGI script that reads the notice details.



Jeff has made a [screencast](http://asterisk-java.org/static/opennms-asterisk-notifications.swf) that shows it in action. If you are interested in the details have a look at his [strategy class](https://opennms.svn.sourceforge.net/svnroot/opennms/opennms/trunk/opennms-asterisk/src/main/java/org/opennms/netmgt/notifd/AsteriskOriginateNotificationStrategy.java) for originating calls and the [AGI script](https://opennms.svn.sourceforge.net/svnroot/opennms/opennms/trunk/opennms-asterisk/src/main/java/org/opennms/netmgt/asterisk/agi/scripts/ReadNoticeDetailsAgiScript.java) that reads some of the notice details. Along with a few [properties](https://opennms.svn.sourceforge.net/svnroot/opennms/opennms/trunk/opennms-base-assembly/src/main/filtered/etc/asterisk-configuration.properties) for configuration this makes a good example on how to integrate Asterisk into your applications with Asterisk-Java.





**References**






  * [OpenNMS homepage](http://www.opennms.org/)


  * Jeff's slides on [OpenNMS and Asterisk](http://asterisk-java.org/static/OpenNMS%20and%20Asterisk.pdf)


  * Jeff's screencast on [OpenNMS Asterisk Notifications](http://asterisk-java.org/static/opennms-asterisk-notifications.swf)







