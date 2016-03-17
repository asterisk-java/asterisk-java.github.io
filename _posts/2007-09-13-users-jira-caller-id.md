---
author: srt
comments: true
date: 2007-09-13 21:51:52+00:00
layout: post
permalink: users-jira-caller-id-746
slug: users-jira-caller-id
title: 'Users: JIRA Caller ID'
wordpress_id: 746
tags:
- asterisk-java
- users
---


![]({{ site.url }}/assets/2011/12/Caller+ID+icon+screenshot.gif)
The cool aussi guys at [Atlassian](http://www.atlassian.com/) had another 
[FedEx day](http://blogs.atlassian.com/rebelutionary/archives/000495.html). One of the plugins for their issue tracker [JIRA](http://www.atlassian.com/software/jira/) they implemented is [JIRA Caller ID](http://blogs.atlassian.com/developer/2007/09/fedex_vi_winner_jira_caller_id.html).






Though JIRA is mainly used to track issues in software development projects this is by far not the only way to use the tool. JIRA is used to track support requests, project issues and Atlassian even uses it to track candidates in their recruitment process. Issues can be entered directly through their web UI, they can result from incoming emails and of course phone calls. So they had the following idea:





<blockquote>
Why not improve JIRA's abilities as a tool for capturing and responding to telephone enquiries? Most calls include Caller ID, showing the called party the caller's telephone number. Why not use this information to automatically retrieve the caller's information in JIRA, saving time and frustration for both parties?
</blockquote>





The solution they came up with extracts the Caller ID from the current call and finds the corresponding JIRA user so you can easily access the the caller's profile from which you can search for his open issues. In addition to that the new plugin saves a call history complete with recordings of answered calls:





![]({{ site.url }}/assets/2011/12/Call+History+Screenshot.gif)





The plugin will soon be publicly available from Atlassian's plugin library. For now you can get the details from Adrian Hempel's blog entry: [JIRA Caller ID](http://blogs.atlassian.com/developer/2007/09/fedex_vi_winner_jira_caller_id.html).

