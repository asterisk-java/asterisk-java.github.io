---
author: srt
comments: true
date: 2009-05-13 08:34:00+00:00
layout: post
permalink: scripting-support-for-fastagi-466/
slug: scripting-support-for-fastagi
title: Scripting Support for FastAGI
wordpress_id: 466
tags:
- agi
- asterisk-java
- groovy
- javascript
- php
---


Asterisk-Java 1.0.0 includes support for implementing AGI scripts in the scripting language of your choice. You still have the benefit of running on the JVM but for the implementation of your script you can now choose your favorite language.



I've prepared a small demo script that counts down from ten to zero. Then it plays a beep and waits for DTMF input to read the digit you've pressed back to you. You can exit by pressing star (*) or pound (#). To show you how this script looks like in the different languages it is implemented three times: In Groovy, JavaScript and PHP.



To get started just download the [binary distribution of Asterisk-Java](http://maven.reucon.com/public-snapshot/org/asteriskjava/asterisk-java/1.0.0-SNAPSHOT/asterisk-java-1.0.0-20090513.085050-484-bin.zip). Unpack it and run the asterisk-java.jar file from the unpacked directory.




    
    
    $ cd asterisk-java-1.0.0-SNAPSHOT
    $ java -jar asterisk-java.jar
    May 13, 2009 1:26:16 AM org.asteriskjava.fastagi.DefaultAgiServer startup
    INFO: Listening on *:4573.
    





The AGI scripts are put into the agi directory. There you'll also find the [demo.groovy](http://svn.reucon.net/repos/asterisk-java/trunk/dist/agi/demo.groovy), [demo.js](http://svn.reucon.net/repos/asterisk-java/trunk/dist/agi/demo.js) and [demo.php](http://svn.reucon.net/repos/asterisk-java/trunk/dist/agi/demo.php) files. The lib directory contains additional libraries required to execute the scripts.



In addition to the functions provided by the scripting language Asterisk-Java adds two variables:






[request](http://asterisk-java.org/development/apidocs/org/asteriskjava/fastagi/AgiRequest.html)

    the request data including the dialed extension, the caller id, channel name, parameters and more

[channel](http://asterisk-java.org/development/apidocs/org/asteriskjava/fastagi/AgiChannel.html)

    for interacting with Asterisk, e.g. to stream files, receive DTMF digits or execute dialplan applications





Modify your dialplan and add extensions for the demo scripts:




    
    
    exten => 2000,1,Agi(agi://localhost/demo.groovy)
    exten => 2001,1,Agi(agi://localhost/demo.js)
    exten => 2002,1,Agi(agi://localhost/demo.php)
    





If you are not running Asterisk-Java on the same server as Asterisk replace localhost by the hostname of the machine running Asterisk-Java.



Note that you will need at least Java 6 to make use of the new scripting support.

