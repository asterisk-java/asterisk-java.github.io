---
author: srt
comments: true
date: 2007-07-23 19:16:15+00:00
layout: post
permalink: users-biocluster-406
slug: users-biocluster
title: 'Users: BioCluster'
wordpress_id: 406
tags:
- asterisk-java
- cluster
- users
---


![](/asterisk-java/wp-content/files/2011/12/voipcluster.jpg)
"[BioCluster](http://voip-cluster.org/) is a clustering platform for Asterisk. It is installed alongside 
Asterisk on several machines and can turn them into a VoIP cluster.   

BioCluster doesn't require changes to the Asterisk code, but communicates 
with it as needed by using Asterisk-Java. Although the peer-to-peer protocol 
used by BioCluster was originally designed to make Asterisk clusterable, it 
is separate from any Asterisk-dependent parts and can be adapted to make 
other platforms clusterable.



All data is shared across nodes in the cluster. This includes extensions, 
trunks, dialplan data, AGI scripts, configuration and many other types of 
data. Thus there's no single point of failure. Expanding a cluster with 
another machine is just a matter of connecting it to the network and giving 
it the right shared network secret. When a new node connects to the network, 
it discovers other nodes in the cluster and retrieves all relevant data.



[BioCluster](http://voip-cluster.org/) uses Asterisk-Java for several uses. It is used to monitor events, 
for example for keeping track of active channels on a local machine and 
sending updates about these channels to other nodes in the cluster. We also 
use it for sending events to Asterisk, e.g. hanging up a channel. Another 
feature used is the FastAGI server functionality provided in Asterisk-Java to 
support AGI scripts.



Using the Asterisk Management Interface would have normally been inconvenient 
and prone to trouble, but Asterisk-Java turned it into a simple task. Its API 
is extensively documented, which helped easily find the right classes for the 
task."





Meni Livne, BioCluster Maintainer, Atelis PLC
