---
author: srt
comments: true
date: 2008-08-10 03:38:46+00:00
layout: post
permalink: outbound-message-delivery-using-agi-and-ami-in-scala-556
slug: outbound-message-delivery-using-agi-and-ami-in-scala
title: Outbound Message Delivery using AGI and AMI in Scala
wordpress_id: 556
tags:
- agi
- ami
- asterisk
- asterisk-java
- scala
---


![Scala](/asterisk-java/wp-content/files/2011/12/scala_logo.png)

From my participation in the [asterisk-users](http://lists.digium.com/mailman/listinfo/asterisk-users) and [asterisk-java-users](http://lists.sourceforge.net/mailman/listinfo/asterisk-java-users) mailing lists, and from the general questions I see, I think a common use case for the combination of the **Gateway** interface and the **Manager** interface is to **deliver outbound recorded messages**. I think that an example might help to show how the two interfaces (and the two parts of Asterisk-Java) can be leveraged to deliver outbound messages.






However, because **I've recently wanted to write more complex applications in [Scala](http://www.scala-lang.org/)** (a language interoperable with Java), I'm going to show you how to perform outbound message delivery with Scala and Asterisk-Java and without modification of the dialplan. **If you liked my example of Scala and want to see more, I'd recommend [this series if you have a Java background](http://www.codecommit.com/blog/scala/scala-for-java-refugees-part-1).**







**Here's the plan for our simple application**:




  1. Design an Agi script that plays back our message


  2. Create & start an AgiServer object to host our script


  3. Create a Manager connection to Asterisk


  4. Using the Manager connection, ask Asterisk to originate a call from some destination to our Agi script


  5. Create a callback handler to act if/when the originate fails, succeeds, or we get disconnected









**First, here's some definitions and imports we'll need** in order to use Console (the System.out analog) and the Asterisk-Java library:

    
    
    package org.asteriskjava.blog.scala
      
    import actors.Actor
    import Console.println
    import org.asteriskjava.fastagi._
    import org.asteriskjava.live._
    









**Next, here's the simple Agi script singleton class** that simply plays the hello-world sound file, and then counts to ten. This is what our users will hear as the message.

    
    
    object OutgoingMessageScript extends BaseAgiScript
    {
        def service(request: AgiRequest, channel: AgiChannel): Unit = {
          streamFile("hello-world")
          for(i <- 0.until(10))
            sayNumber((i+1)+"")
        } 
    }
    









Skipping ahead of a few steps (because it doesn't depend on anything else), **here's the class that implements the callback interface**, providing instructions on what to do if the originate dials, fails, succeeds, it's busy or not answered, or we get disconnected. This handler simply prints out what happened, though in your own code, this would be a good place to queue up something that failed, or mark it as a preliminary success (I say preliminary because this only means the originate succeeded, but not the playback... yet).

    
    
    object OutgoingMessageStatusReport extends OriginateCallback
    {
        def onDialing(channel: AsteriskChannel): Unit = println("Dialing-" + channel)
        def onSuccess(channel: AsteriskChannel): Unit = println("Success-" + channel)
        def onNoAnswer(channel: AsteriskChannel): Unit = println("No Answer-" + channel)
        def onBusy(channel: AsteriskChannel): Unit = println("Busy-" + channel)
        def onFailure(cause: LiveException): Unit = println("Failure-" + cause)
    }
    









**And finally, here's the start of the main class and method...**

    
    
    object OutgoingMessageDelivery {
      
      def main(args : Array[String]) : Unit = {
    



**We'll create an AGI server, and use _Actor_ to get the startup method executed in a separate thread.** We do this so that it will begin to accept connections without blocking our current thread.


    
    
        // start an AGI server with the given script
        val asteriskGatewayServer = new DefaultAgiServer(OutgoingMessageScript)
        new Actor { def act = asteriskGatewayServer.startup }.start
    



**Next, we'll connect to Asterisk through the Manager interface too** (via the nice Live API that wraps it).

    
    
        // start a connection to the manager interface
        val asteriskManagerInterface = new DefaultAsteriskServer(
          "192.168.1.15", 
          "root", 
          "secret")
    



**Finally, we will ask through the Manager interface that Asterisk originate** to _"SIP/xlite1"_ (if you were doing massive outbound delivery with T1/E1 circuits, you'd probably put something like _"Zap/r1/outbound number"_ here)

    
    
        // connect some channel to the script, with a callback 
        asteriskManagerInterface.originateToApplicationAsync(
          "SIP/xlite1", // **** could be "Zap/r1/1234567890"
          "Agi", "agi://"+java.net.InetAddress.getLocalHost.getHostAddress, 
          10*1000, 
          OutgoingMessageStatusReport)
      }
      
    }
    









**And that's it!** Asterisk will try to originate that call, and inform us (via the callback) of the outcome of the attempted originate.







**Here's what the log will look like**:

    
    
    2008-08-09 16:02:04,671 org.asteriskjava.fastagi.DefaultAgiServer INFO [Thread-1] - Listening on *:4573.
    2008-08-09 16:02:04,718 org.asteriskjava.manager.internal.ManagerConnectionImpl INFO [main] - Connecting to 192.168.1.15:5038
    2008-08-09 16:02:04,843 org.asteriskjava.manager.internal.ManagerConnectionImpl INFO [Asterisk-Java ManagerConnection-0-Reader-0] - Connected via Asterisk Call Manager/1.0
    2008-08-09 16:02:04,859 org.asteriskjava.manager.internal.ManagerConnectionImpl INFO [main] - Successfully logged in
    2008-08-09 16:02:04,875 org.asteriskjava.manager.internal.ManagerConnectionImpl INFO [main] - Determined Asterisk version: Asterisk 1.4
    2008-08-09 16:02:04,890 org.asteriskjava.live.internal.AsteriskServerImpl INFO [main] - Initializing done
    2008-08-09 16:02:04,937 org.asteriskjava.live.internal.ChannelManager INFO [Asterisk-Java DaemonPool-1-thread-1] - Adding channel SIP/xlite1-081da108(1218312125.13)
    Dialing-AsteriskChannel[id='1218312125.13',name='SIP/xlite1-081da108',callerId='',state='DOWN',account='null',dateOfCreation=Sat Aug 09 16:02:04 EDT 2008,dialedChannel=null,dialingChannel=null,linkedChannel=null]
    2008-08-09 16:02:06,218 org.asteriskjava.fastagi.DefaultAgiServer INFO [Thread-1] - Received connection from /192.168.1.15
    Success-AsteriskChannel[id='1218312125.13',name='SIP/xlite1-081da108',callerId='',state='UP',account='null',dateOfCreation=Sat Aug 09 16:02:04 EDT 2008,dialedChannel=null,dialingChannel=null,linkedChannel=null]
    2008-08-09 16:02:06,218 org.asteriskjava.fastagi.DefaultAgiServer INFO [Thread-1] - Thread pool started.
    2008-08-09 16:02:06,375 org.asteriskjava.fastagi.internal.FastAgiConnectionHandler INFO [Asterisk-Java DaemonPool-2-thread-1] - Begin AgiScript org.asteriskjava.blog.scala.OutgoingMessageScript$ on Asterisk-Java DaemonPool-2-thread-1
    









**Questions?** Post on our [mailing list](http://lists.sourceforge.net/mailman/listinfo/asterisk-java-users) or reply to the post!







It's worth nothing, too, that there are certainly [already ways of doing this](http://www.voip-info.org/wiki/view/Asterisk+auto-dial+out+deliver+message) that may only involve the dialplan. Also, this doesn't solve the problem of [detecting answering machines](http://www.voip-info.org/wiki/view/Asterisk+cmd+AMD).







**The complete source**:

    
    
    package org.asteriskjava.blog.scala
      
    import actors.Actor
    import Console.println
    import org.asteriskjava.fastagi._
    import org.asteriskjava.live._
    
    object OutgoingMessageDelivery {
      
      def main(args : Array[String]) : Unit = {
        // start an AGI server with the given script
        val asteriskGatewayServer = new DefaultAgiServer(OutgoingMessageScript)
        new Actor { def act = asteriskGatewayServer.startup }.start
        
        // start a connection to the manager interface
        val asteriskManagerInterface = new DefaultAsteriskServer(
          "192.168.1.15", 
          "root", 
          "secret")
        
        // connect some channel to the script, with a callback 
        asteriskManagerInterface.originateToApplicationAsync(
          "SIP/xlite1", // **** could be "Zap/r1/1234567890"
          "Agi", "agi://"+java.net.InetAddress.getLocalHost.getHostAddress, 
          10*1000, 
          OutgoingMessageStatusReport)
      }
      
    }
    
    object OutgoingMessageScript extends BaseAgiScript
    {
        def service(request: AgiRequest, channel: AgiChannel): Unit = {
          streamFile("hello-world")
          for(i <- 0.until(10))
            sayNumber((i+1)+"")
        } 
    }
    
    object OutgoingMessageStatusReport extends OriginateCallback
    {
        def onDialing(channel: AsteriskChannel): Unit = println("Dialing-" + channel)
        def onSuccess(channel: AsteriskChannel): Unit = println("Success-" + channel)
        def onNoAnswer(channel: AsteriskChannel): Unit = println("No Answer-" + channel)
        def onBusy(channel: AsteriskChannel): Unit = println("Busy-" + channel)
        def onFailure(cause: LiveException): Unit = println("Failure-" + cause)
    }
    



