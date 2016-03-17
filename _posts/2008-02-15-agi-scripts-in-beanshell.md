---
author: srt
comments: true
date: 2008-02-15 02:18:17+00:00
layout: post
permalink: agi-scripts-in-beanshell-766/
slug: agi-scripts-in-beanshell
title: AGI scripts in BeanShell
wordpress_id: 766
tags:
- agi
- asterisk-java
- beanshell
- scripting
---


[beanizer.org](http://www.beanizer.org/) has published an interesting [article](http://www.beanizer.org/site/index.php/en/Articles/A-simple-AGI-scripting-engine-with-Asterisk-Java.html) on how to build an AGI server with Asterisk-Java to run AGI scripts written in [BeanShell](http://www.beanshell.org/).



They provide a dispatcher AgiScript that delegates to a BeanShell script and provides some additional convenience functions to make the custom scripts easy to implement.



The advantages of using scripting languages on the JVM along with Asterisk-Java are compelling:





<blockquote>
The approach is quite flexible, our script engine doesn't need to be on the same computer the pbx is on, and we can add/modify our scripts on the fly without need for compilation or engine restart.
</blockquote>





You might also be interested in our recent posting on writing [AGI scripts in Groovy](http://blogs.reucon.com/asterisk-java/2007/11/20/agi_scripts_in_groovy.html) that describes a similar approach with a focus on [Groovy](http://groovy.codehaus.org/).





**References**






  * [A simple AGI scripting engine with Asterisk-Java](http://www.beanizer.org/site/index.php/en/Articles/A-simple-AGI-scripting-engine-with-Asterisk-Java.html)


  * [BeanShell - Lightweight Scripting for Java](http://www.beanshell.org/)


  * [AGI scripts in Groovy](http://blogs.reucon.com/asterisk-java/2007/11/20/agi_scripts_in_groovy.html)


