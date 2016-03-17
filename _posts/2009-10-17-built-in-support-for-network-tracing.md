---
author: srt
comments: true
date: 2009-10-17 04:53:00+00:00
layout: post
permalink: built-in-support-for-network-tracing-656
slug: built-in-support-for-network-tracing
title: Built-in Support For Network Tracing
wordpress_id: 656
tags:
- agi
- ami
- asterisk-java
- debugging
---

Up to now the preferred way to obtain traces of the communication between Asterisk-Java and Asterisk was using tcpdump, wireshark or ngrep as described in [Debugging Manager API](http://blogs.reucon.com/asterisk-java/debugging-manager-api-776/). Having a full log of the direct network communication is often the only way to resolve issues related to problems in the Manager API or Fast AGI.

To make it easier for our users to obtain these traces we have now included a tracing feature directly into Asterisk-Java. You can enable it at runtime by setting the system property `org.asteriskjava.trace` to `true`. On the command line:

    
    java -Dorg.asteriskjava.trace=true ...


Trace files are written to the temp dir by default ("java.io.temp"). You can specify an alternate location by using the `org.asteriskjava.trace.directory` system property:

    
    java -Dorg.asteriskjava.trace=true \
         -Dorg.asteriskjava.trace.directory=/opt/traces ...


Log files contain a timestamp and the IP addresses and ports of the involved servers in their file name. A typical file looks like this:

    
    2009-10-20T21:51:18.414CEST <<< Asterisk Call Manager/1.1
    2009-10-20T21:51:18.536CEST >>> action: Challenge
                                >>> actionid: 888911819_0#
                                >>> authtype: MD5
                                >>>
    2009-10-20T21:51:18.601CEST <<< Response: Success
    2009-10-20T21:51:18.663CEST <<< ActionID: 888911819_0#
    2009-10-20T21:51:18.664CEST <<< Challenge: 336054137
    2009-10-20T21:51:18.665CEST <<<
    2009-10-20T21:51:18.705CEST >>> action: Login
                                >>> actionid: 888911819_1#
                                >>> authtype: MD5
                                >>> username: manager
                                >>> key: ed0481d08ae7832fb
                                >>>
    2009-10-20T21:51:18.768CEST <<< Response: Success
    2009-10-20T21:51:18.831CEST <<< ActionID: 888911819_1#
    2009-10-20T21:51:18.832CEST <<< Message: Authentication accepted
    2009-10-20T21:51:18.833CEST <<<


This new feature is already part of the latest Asterisk-Java [1.0.0-CI-SNAPSHOT](http://www.asterisk-java.org/download/1.0.0.CI-SNAPSHOT) and will be shipped with milestone 3.

Please consider attaching a trace file to your bug reports in the future. It speeds up bug fixing considerably.
