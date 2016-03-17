---
author: srt
comments: true
date: 2009-09-26 10:16:00+00:00
layout: post
permalink: asterisk-java-goes-osgi-636
slug: asterisk-java-goes-osgi
title: Asterisk-Java goes OSGi
wordpress_id: 636
tags:
- asterisk-java
- osgi
---

We are currently working on making Asterisk-Java [OSGi](http://www.osgi.org/) compliant to make it easier for those users who want to use Asterisk-Java in an OSGi container like [Equinox](http://eclipse.org/equinox/). This means Asterisk-Java will contain the proper bundle headers in its MANIFEST.MF and will follow the OSGi rules for version names. The new version names for Asterisk-Java are similar to those used by Spring Framework:



1.0.0.CI-SNAPSHOT
    Continuous integration snapshot releases
1.0.0.M3
    Milestone releases
1.0.0.RC1
    Release candidates
1.0.0.RELEASE
    Final release
1.0.0.SR01
    Service release with emergency bug fixes
The first OSGi compliant snapshots of Asterisk-Java are now available for download: [Asterisk-Java 1.0.0.CI-SNAPSHOT](http://www.asterisk-java.org/download/1.0.0.CI-SNAPSHOT). The old 1.0.0-SNAPSHOT releases will no longer be updated.

For those developers that are not interested in OSGi nothing will change. The OSGi manifest headers added to Asterisk-Java are simply ignored when run in a non-OSGi environment.

The new MANIFEST.MF looks like this:

    
    Manifest-Version: 1.0
    Bundle-Description: The free Java library for Asterisk PBX integration.
    Bundle-DocURL: http://asterisk-java.org/
    Bundle-ManifestVersion: 2
    Bundle-Name: Asterisk-Java
    Bundle-SymbolicName: org.asteriskjava
    Bundle-Vendor: reucon
    Bundle-Version: 1.0.0.CI-SNAPSHOT
    Export-Package: org.asteriskjava;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.config;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.config.dialplan;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.fastagi;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.fastagi.command;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.fastagi.reply;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.manager;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.manager.action;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.manager.event;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.manager.response;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.manager.util;version="1.0.0.CI-SNAPSHOT",
     org.asteriskjava.live;version="1.0.0.CI-SNAPSHOT"


If you are looking for a ready to use OSGi based framework to develop AGI scripts for Asterisk on SpringSource dm Server you may also want to check [ajdmserver](http://code.google.com/p/ajdmserver/).
