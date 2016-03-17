---
author: srt
comments: true
date: 2007-04-17 22:31:00+00:00
layout: post
permalink: originate-using-asterisk-local-channels-566
slug: originate-using-asterisk-local-channels
title: Originate Using Asterisk Local Channels
wordpress_id: 566
tags:
- asterisk
---


[![](http://asterisk-java.org/static/trace/trace.png)](http://asterisk-java.org/static/trace/originate_local.html)
Whenever you want to place a call between two extensions in the dialplan you have to use Local channels.
  

The [OriginateAction](http://asterisk-java.org/development/apidocs/org/asteriskjava/manager/action/OriginateAction.html) that you use when placing calls through the Manager API requires a channel name for the first leg. Usually your application has no knowledge of the dialplan details, i.e. it does not know which channel is triggered by an extension (maybe it's a SIP hardphone, an IAX device or a link to another Asterisk server). What you want to do is "place a call between number a and number b" and leave the rest to Asterisk.






Local channels act as a proxy to the real channels mapped to an extension. So to place a call from 1310 to 1299 your Originate looks like:




    
    
    Channel: Local/1310@from-local
    Context: from-local
    Exten: 1310
    Priority: 1
    




instead of



    
    
    Channel: SIP/1310
    Context: from-local
    Exten: 1399
    Priority: 1
    





There is an article about [Local Channels](http://www.voip-info.org/wiki/view/Asterisk+local+channels) at [voip-info.org](http://www.voip-info.org/) that covers the basics.






So that's all very nice and looks straight forward. It becomes more interesting if you have a look at what happens under the hood:






A Local channel actually consists of two channels in Asterisk: Local/XXX,1 and Local/XXX,2. The Local/XXX,2 channel traverses the dialplan starting at the context and extension you provided. In our example this is the extension 1310 in from-local. If you watch the CLI or the events triggered you will see:




    
    
    Set(_ALERT_INFO=<Bellcore-dr1>)
    Macro(localexten|1310|SIP/1310)
    Dial(SIP/1310|30|t)
    





This corresponds to the defintion of 1310 in my dialplan:




    
    
    [from-local]
    exten => 1310,1,Set(_ALERT_INFO=<Bellcore-dr1>)
    exten => 1310,n,Macro(localexten,${EXTEN},SIP/${EXTEN})
    
    [macro-localexten]
    exten => s,1,Dial(${ARG2},30,t)
    exten => s,n,Goto(s-${DIALSTATUS},1)
    exten => s-NOANSWER,1,Voicemail(u${ARG1})
    exten => s-NOANSWER,n,Hangup
    exten => s-BUSY,1,Busy
    exten => _s-.,1,Goto(s-NOANSWER,1)
    





The Dial command triggers an additional channel (SIP/1310). This is the actual channel that is proxied by the Local channel.






The other side of the Local channel, Local/XXX,1, is used for the desination. In our example this is the extension 1299 in from-local. You see similar events for this channel. The actual channel that is triggered for 1299 is an IAX channel to another Asterisk server: IAX2/iax_reucon_net-3.






Now we reach the point where we have four channels set up: The two sides of the Local channel and the two "real" channels SIP/1310 and IAX2/iax_reucon_net. Two channels are now longer needed and will vanish. Before this happens all data of the proxied channel is copied (masqueraded) to Local/XXX,1 so that Local/XXX,1 is renamed to SIP/1310. The "old" SIP/1310 channel is renamed to SIP/1310-0820f718<MASQ> and finally to Local/1310@from-local-1e71,1<ZOMBIE> before it is hung up. Local/XXX,2 is hung up without any renaming.
  

So in the end you have exactly what you would have expected: Two channels, SIP/1310 and IAX2/iax_reucon_net up and connected.






I have prepared a nice diagram that shows all these steps in detail and helps you understand what happens:




  * [Diagram: Originate with Local channel






