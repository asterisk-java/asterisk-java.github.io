---
author: srt
comments: true
date: 2008-04-05 03:02:44+00:00
layout: post
permalink: preview-support-for-asyncagi-866/
slug: preview-support-for-asyncagi
title: 'Preview: Support for AsyncAGI'
wordpress_id: 866
tags:
- agi
- asterisk-java
---


I've just finished adding support for [Asynchronous AGI](http://www.moythreads.com/wordpress/2007/12/24/asterisk-asynchronous-agi/) to Asterisk-Java. AsyncAGI allows you to run AGI scripts through a Manager API connection.



The way AsyncAGI is supported by Asterisk-Java hides the differences in the underlying communication from the users of our library. Your AGI scripts developed for FastAGI will run with AsyncAGI without a change.



To make use of AsyncAGI add the following extension to you dialplan:




    
    
    exten => 1234,1,Agi(agi:async)
    





Create a simple AGI script, pass it to AsyncAgiServer and register the AsyncAgiServer as a listener to a ManagerConnection:




    
    
    public class SampleScript extends BaseAgiScript
    {
        public void service(AgiRequest request, AgiChannel channel) throws AgiException
        {
            channel.streamFile("tt-monkeys");
        }
    
        public static void main(String[] args) throws Exception
        {
            ManagerConnection connection;
            AsyncAgiServer agiServer;
    
            connection = new DefaultManagerConnection("localhost", "manager", "pa55w0rd");
            agiServer = new AsyncAgiServer(new SampleScript());
            connection.addEventListener(agiServer);
            connection.login();
    
            while (true)
            {
                Thread.sleep(1000L);
            }
        }
    }
    





To run the sample you need the [latest snapshot](http://asterisk-java.org/download/1.0.0-SNAPSHOT) of Asterisk-Java 1.0.0 (at least 20080404.222056-117) and Asterisk 1.6.0.





**References**






  * [Moy: Asterisk Asynchronous AGI](http://www.moythreads.com/wordpress/2007/12/24/asterisk-asynchronous-agi/)


