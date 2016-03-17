---
author: srt
comments: true
date: 2008-08-15 01:21:00+00:00
layout: post
permalink: aacc-an-asterisk-java-based-solution-for-call-centers-736/
slug: aacc-an-asterisk-java-based-solution-for-call-centers
title: 'AACC: An Asterisk-Java based solution for Call Centers'
wordpress_id: 736
tags:
- aacc
- asterisk-java
- call-center
- users
---


As far as I know, no one has yet succeeded to deliver a high quality open source package for the thousands of small and medium sized call centers around the globe that want to go _Asterisk_. But having to buy proprietary software for managing the call center, or having to build their own software, seemed up to now the only two available options.



AACC was conceived to fulfill the need of those call centers, and make an impact in call centers similar to the one Asterisk has made in telephony. Now, thatâ€™s setting a pretty high mark for ourselves, so, how will we do it? 



First of all, we have tried very hard to understand what those small and medium sized call centers need and want. So we are designing a system which is feature rich, yet easy to manage, agile, and extensible. We didnâ€™t set up to reinvent the wheel. So we try to take advantage of other open source projects out there that do what they do very well. One of those projects is Asterisk-Java, on which we rely to communicate back and forth with Asterisk.



Then we said to ourselves, "Letâ€™s go visual!" But letâ€™s not go exactly _mainstream_. So we ruled out resource-hungry web based solutions, AJAX, and other technologies, and chose to use _industry proven_ Java technology, both for our clients as well as for our servers.



Agents will have a toolbar â€“ a specialized CRM from which they will be able to see and update call information, see a script for the campaign, or have it do an automatic screen pop. Administrators will have a control panel from which they will manage all aspects of the call center with ease. And they can chose to go Linux, or to go Windows, orâ€¦ Mac? Doesnâ€™t matter, AACC is built with Java, so itâ€™s OS independent. 



The response from the developersâ€™ community was overwhelming, surpassing all of our expectations. We even had the luxury of turning down candidates! We are working right now on several fronts.



AACC will be suitable both for inbound as well as for outbound call centers. So weâ€™re designing a predictive dialer, which will be able to handle multiple campaigns for multiple customers, with customizable information such as products offered, and per-campaign custom data, sales scripts, and call disposition.



Reporting is key. We are creating additional reporting information to what Asterisk provides, both for realtime and historical statistics. We're also incorporating [JasperReports](http://www.jaspersoft.com/JasperSoft_JasperReports.html) for stunning on-screen reporting, as well as saving the reports in the most relevant file formats, like PDF, RTF, ODT, HTML, XLS, and others. Reporting will of course be extensible, meaning that you will be able to design your own reports â€“ with a [WYSIWYG tool](http://www.jaspersoft.com/JasperSoft_iReport.html), also open source â€“ in addition to the reports you will get out-of-the-box.



Last, but not least, AACC will be fully localizable. We hope that once initial development stage is over, we can be joined by translators who will help us localize the application to many languages.



When, you would ask, will this be production ready? We believe an alpha (i.e. not yet ready for production) version will be available before Christmas 2008. A beta version should be ready not long after that. Iâ€™ll keep you posted! Make sure you join our [users list](https://lists.sourceforge.net/lists/listinfo/hanashidialer-users) and visit our site at [http://hanashidialer.sourceforge.net](http://hanashidialer.sourceforge.net) for more information about this project.

