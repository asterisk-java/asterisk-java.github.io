---
author: srt
comments: true
date: 2007-12-06 16:26:19+00:00
layout: post
permalink: integrating-agi-and-apache-tomcat-536/
slug: integrating-agi-and-apache-tomcat
title: Integrating AGI and Apache Tomcat
wordpress_id: 536
tags:
- agi
- asterisk-java
- spring
- tomcat
---


![]({{ site.url }}/assets/2011/12/tomcat.gif)
I've already described how the [Spring Framework](http://www.springframework.org) can be used to [externalize your AGI configuration](/asterisk-java/2007/03/22/externalize_your_agi_configuration.html). That blog entry asumed you are running your AGI server as a stand alone application. What is the best way to run it within an app server or a servlet container like [Tomcat](http://tomcat.apache.org) however?



When you just place the snippet from [here](/asterisk-java/2007/03/22/externalize_your_agi_configuration.html) into your applicationContext.xml you will notice that Tomcat will hang on start up and that you won't be able to shut it down properly.  

The reason for this is that the AGI server is blocking Tomcat and waits for incoming AGI requests. To solve this you have to wrap your [AgiServer](http://asterisk-java.org/latest/apidocs/org/asteriskjava/fastagi/AgiServer.html) in a thread so that it runs in the background. Asterisk-Java comes with a utility class called [AgiServerThread](http://asterisk-java.org/latest/apidocs/org/asteriskjava/fastagi/AgiServerThread.html) that just does this.



So the following snippet will work as expected:




    
    
    <bean class="org.asteriskjava.fastagi.AgiServerThread"
          init-method="startup" destroy-method="shutdown">
        <property name="agiServer" ref="agiServer"/>
    </bean>
    
    <bean id="agiServer" class="org.asteriskjava.fastagi.DefaultAgiServer">
        <property name="bindPort" value="4573"/>
        <property name="mappingStrategy">
            <bean class="xxx">
    ...
            </bean>
        </property>
    </bean>
    




References:






  * [Externalize your AGI Configuration](/asterisk-java/2007/03/22/externalize_your_agi_configuration.html)


