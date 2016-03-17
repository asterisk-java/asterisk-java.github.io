---
author: srt
comments: true
date: 2008-01-12 18:32:00+00:00
layout: post
permalink: md5-authentication-bug-in-asterisk-576
slug: md5-authentication-bug-in-asterisk
title: MD5 Authentication Bug in Asterisk
wordpress_id: 576
tags:
- asterisk
---


The good news is: Asterisk-Java seems to work quite well with the latest development version of [Asterisk](http://www.asterisk.org).






One issue came up with a [discussion](http://www.igniterealtime.org/community/message/163479) on [igniterealtime.org](http://www.igniterealtime.org) concerning [Asterisk-IM](http://www.igniterealtime.org/community/community/support/asterisk-im_support) though. Asterisk-IM had problems authenticating to the latest development version of Asterisk. As it turned out the reason for this was a
[bug](http://bugs.digium.com/view.php?id=11749) in Asterisk introduced a few months ago:





<blockquote>

> 
> When using challenge/reponse authentication with AMI the "Login" action uses the secret supplied with the "Login" action instead of the one from manager.conf to calculate the MD5 hash.
> 
> 

> 
> This has two effects:
> 
> 

> 
> 

>   1. Login with "AuthType: MD5" and "Key:" but without a "Secret:" always fails
> 

>   2. Anybody who knows a valid username can login without knowing the secret configured in manager.conf
> 

</blockquote>




As Asterisk-Java uses MD5 based challenge/response authentication by default there are probably other users out there that are affected by the problem.




The solution is easy: Just upgrade to the latest revision from trunk. Tilghman just commited a fix with [r98536](http://svn.digium.com/view/asterisk?view=rev&revision=98536).
