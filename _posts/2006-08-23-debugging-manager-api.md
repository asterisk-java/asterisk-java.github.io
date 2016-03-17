---
author: srt
comments: true
date: 2006-08-23 01:43:00+00:00
layout: post
permalink: debugging-manager-api-776
slug: debugging-manager-api
title: Debugging Manager API
wordpress_id: 776
tags:
- asterisk
---

Start ngrep either on the Asterisk server or on the client:




    
    
    ngrep -s 1500 port 5038 -T
    





A successful login results in output like this:




    
    
    interface: eth1 (10.13.0.0/255.255.255.0)
    filter: (ip or ip6) and ( port 5038 )
    ####
    T +7.653003 10.13.0.102:5038 -> 10.13.0.55:46779 [AP]
      Asterisk Call Manager/1.2..
    ##
    T +0.113468 10.13.0.55:46779 -> 10.13.0.102:5038 [AP]
      action: Challenge..actionid: 29181730_0#..authtype: MD5....
    ##
    T +0.000391 10.13.0.102:5038 -> 10.13.0.55:46779 [AP]
      Response: Success..ActionID: 29181730_0#..Challenge: 171465739....
    ##
    T +0.036776 10.13.0.55:46779 -> 10.13.0.102:5038 [AP]
      action: Login..actionid: 29181730_1#..key: fdc46063e81c6c5ab84188698e0cb55b..authtype: MD5..username: manager....
    #
    T +0.001271 10.13.0.102:5038 -> 10.13.0.55:46779 [AP]
      Response: Success..
    #
    
