---
author: srt
comments: true
date: 2009-04-03 21:38:00+00:00
layout: post
permalink: speech-recognition-with-asterisk-java-666
slug: speech-recognition-with-asterisk-java
title: Speech Recognition with Asterisk-Java
wordpress_id: 666
tags:
- asterisk-java
- lumenvox
- speech
---

![](/asterisk-java/wp-content/files/2011/12/lumenvox.gif)
The latest [snapshot](http://maven.reucon.com/public-snapshot/org/asteriskjava/asterisk-java/1.0.0-SNAPSHOT/asterisk-java-1.0.0-20090403.210610-444.jar) of Asterisk-Java contains support for the Asterisk Speech API. This makes writing AGI script that recognize speech as easy as writing AGI scripts for DTMF input.

All you need to get started is a recent version of Asterisk 1.6 and the [Lumenvox](http://www.lumenvox.com) Speech Engine. For development you can buy a [starter kit](http://store.digium.com/productview.php?product_code=8ASTLUMSTART) from Digium for 50 USD.

In your AGI script you initialize the speech engine, load and activate a grammer and are ready to recognize speech. The speechRecognize() method takes a voice prompt as its first parameter. The prompt is played to the user and the users response is recognized. The user doesn't have to wait for the prompt to finish, he can start talking right away ("barge in"). The corresponding Java code looks like this:

    
    speechCreate();
    speechLoadGrammar("digits", grammarPath);
    speechActivateGrammar("digits");
    SpeechRecognitionResult result =
      speechRecognize("speech-demo/prompt", 10);
    speechDeactivateGrammar("digits");


The [SpeechRecognitionResult](http://www.asterisk-java.org/development/apidocs/org/asteriskjava/fastagi/SpeechRecognitionResult.html) provided by Asterisk-Java contains the result and the confidence score – a value between 0 and 1000 that indicates how sure the speech engine is that the result is correct. The Java code to evaluate the result looks like this:

    
    if (result.isSpeech())
    {
        if (result.getScore() > 990)
        {
            streamFile("speech-demo/absolutely-sure");
        }
        else if (result.getScore() > 800)
        {
            streamFile("speech-demo/pretty-sure");
        }
        else
        {
            streamFile("speech-demo/not-sure");
        }
    
        // say what we have recognized
        sayDigits(result.getText());
    }


Finally call speechDestory to end the speech recognition session (for a real application you probably want to do this in a finally block):

    
    speechDestroy();


Pretty easy, isn't it?

You can have a look at the [SpeechDemo](http://svn.reucon.net/repos/asterisk-java/trunk/src/integrationtest/org/asteriskjava/fastagi/SpeechDemo.java) AGI script or download the [full demo](http://asterisk-java.org/static/speech-demo.zip) that includes the latest snapshot of Asterisk-Java, the voice prompts and the AGI script.
