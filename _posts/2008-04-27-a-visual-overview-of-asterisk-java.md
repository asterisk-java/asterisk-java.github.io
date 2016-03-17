---
author: srt
comments: true
date: 2008-04-27 12:05:39+00:00
layout: post
permalink: a-visual-overview-of-asterisk-java-706
slug: a-visual-overview-of-asterisk-java
title: A Visual Overview Of Asterisk-Java
wordpress_id: 706
tags:
- asterisk-java
- statistics
---


Atlassian has improved the charting features in their latest release of [Fisheye](http://www.atlassian.com/software/fisheye/). So I had a look at the Asterisk-Java code base to see how it's major packages compare in size. This is what i got:



![](/asterisk-java/wp-content/files/2011/12/aj-stats-2008.png)


Let's have a look at the individual packages:




**The Manager API**





Support for the Manager API (manager) is by far the biggest package in Asterisk-Java. It provides access to a variety of Asterisk features from call control to monitoring and call center management. The size of this package and its steady groth ressemble the groth of features exposed by Asterisk.





**The Asterisk Gateway Interface**





FastAGI is an easy way to implement IVR applications in Java. The feature set is quite stable over time so we don't see significant changes in the code base. You'll even notice that support for [AsyncAGI](/asterisk-java/2008/04/05/preview_support_for_asyncagi.html) (i.e. running AGI scripts over the Manager API) was a quick win as it didn't have a significant impact on the overall size of the package.





**Parsing Configuration Files**





The config package is quite new and supports parsing Asterisk's configuration files. All config files use the same syntax and group up configuration items into contexts. It supports inheritance of contexts, includes and forms the basis for further development like configuration editors or dialplan visualization (stay tuned for more information from Martin on this topic).  

Originally developed to parse voicemail meta files the config package is certainly a candidate for future growth.





**The Live API**





The live API is our own invention and takes integration a step further. Instead of only providing access to the basic features exposed by Asterisk the live API offers real objects with state and behavior that model core concepts found in Asterisk. There are channel objects with state like the current caller id, the progress or hangup reason and methods to redirect channels, start and stop monitoring and much more.
The live API speeds up developers by hiding the sometimes tedious details of the low level Asterisk APIs and has reached a significant size. Next to the config package the live API is under active development and will certainly grow in the future.




