---
author: srt
comments: true
date: 2009-01-20 03:02:00+00:00
layout: post
permalink: free-implementation-of-iax-in-java-436/
slug: free-implementation-of-iax-in-java
title: Free Implementation of IAX in Java
wordpress_id: 436
tags:
- asterisk
- iax
- java
---


Tim Panton [recently announced](http://lists.digium.com/pipermail/asterisk-users/2009-January/224730.html) that [Mexuar](http://www.mexuar.com/) has released their [Correlata SDK](http://www.mexuar.com/developers) under the terms of GPLv3. It is available for download at [http://www.mexuar.com/files/corraleta_sdk.rar](http://www.mexuar.com/files/corraleta_sdk.rar).



Correlata SDK is a pure Java implementation of the [IAX2](http://en.wikipedia.org/wiki/Inter-Asterisk_eXchange) protocol. It includes an applet that can be accessed via JavaScript which makes it useful as a softphone embedded into web pages. In contrast to SIP IAX2 is firewall and NAT friendly.



To use the code you have to compile the sources and create a jar file. Then you have to sign it to allow the applet to access the microphone. Finally you'll setup a web page with the applet and add some JavaScript. You can have a look at the source code of the [Mexuar homepage](http://www.mexuar.com/) to see an example.



Though Mexuar has published the source code under GPL the download only contains the plain Java sources. There is no documentation except for JavaDoc, no build script and no sample code. The link to the download is quite hidden on their website. While Mexuar offers paid support, licenses and manged hosting there doesn't seem to be an Open Source community around it yet. Tim suggested to set up a project on Sourceforge or Google Code to build one. However due to his former relationship with Mexuar he prefers not be the project lead.



I think the code is a great complement to Asterisk-Java and will be very useful for a lot of applications. If you are also interested in giving it a good home and add some polish feel free to comment on this posting or discuss it on our [mailing list](http://asterisk-java.org/development/mail-lists.html).





**References**






  * [Download Source Code](http://blogs.reucon.com/asterisk-java/files/corraleta_sdk.rar)


  * [Implementing IAX2 In Java](http://blogs.reucon.com/asterisk-java/files/Tim%20Panton%20AstriconDallas.ppt), presentation at Astricon Dallas by Tim Panton in 2006


