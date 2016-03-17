---
author: srt
comments: true
date: 2010-12-12 12:37:00+00:00
layout: post
permalink: support-for-skype-for-asterisk-786/
slug: support-for-skype-for-asterisk
title: Support for Skype for Asterisk
wordpress_id: 786
tags:
- ami
- asterisk-java
- skype
---


![]({{ site.url }}/assets/2011/12/skype-for-asterisk.png)
The latest [nightly snapshot](https://secure.reucon.net/nexus/content/repositories/opensource-snapshots/org/asteriskjava/asterisk-java/1.0.0.CI-SNAPSHOT/) of Asterisk-Java now supports [Skype for Asterisk](http://www.digium.com/en/products/software/skypeforasterisk.php) manager events and actions after we've implemented [AJ-262](https://secure.reucon.net/issues/browse/AJ-262). Skype for Asterisk support will also be part of the upcoming 1.0.0.M4 release of Asterisk-Java.





**What can I do with it?**





You can now use Asterisk-Java to




  * Retrieve information about your buddies


  * Add buddies to your buddy list


  * Remove buddies from your buddy list


  * Send and receive Skype Chat messages


And of course you can originate calls to or receive calls from Skype users and use Asterisk-Java based AGI scripts to implement IVR features for Skype.





**What are the prerequisites?**





First you must have a Skype for Asterisk license installed on your Asterisk server. They are available from [Digium's online store](http://store.digium.com/productview.php?product_code=1SFA0001) for $66.00 per channel.  

Then you should apply [this patch](https://secure.reucon.net/issues/secure/attachment/11404/chan_skype.patch) to chan_skype.c to fix a few minor bugs in their Manager API implementation.





**Any questions?**





Feel free to join our [mailing list](https://lists.sourceforge.net/lists/listinfo/asterisk-java-users). 






