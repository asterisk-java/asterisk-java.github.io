---
author: srt
comments: true
date: 2007-11-20 20:00:14+00:00
layout: post
permalink: agi-scripts-in-groovy-806/
slug: agi-scripts-in-groovy
title: AGI scripts in Groovy
wordpress_id: 806
tags:
- agi
- asterisk-java
- groovy
- scripting
---


![]({{ site.url }}/assets/2011/12/groovy.png)
With a little bit of glue code you can implement your AGI scripts in [Groovy](http://groovy.codehaus.org), an agile dynamic language for the Java Platform. Your scripts run still in the Java VM on top of Asterisk-Java.






A very simple Groovy AGI script might look like this:




    
    
    channel.streamFile('tt-monkeysintro')
    





Save it as hello.groovy, put it into your Groovy AGI directory and access it from Asterisk via




    
    
    exten => 1234,1,Agi(agi://your.agi.server.org/hello.groovy)
    





Using Groovy for AGI scripts is great for rapid prototyping as you only have to edit your Groovy script to modify the applications behavior. Recompilation happens automatically. You get the benefits of scripting languages and still run on the JVM.






Here is the glue code to make this work:




    
    
    public class GroovyAgiScript implements AgiScript
    {
        private GroovyScriptEngine gse;
    
        public GroovyAgiScript() throws IOException
        {
            this.gse = new GroovyScriptEngine("/my/groovy/scripts");
        }
    
        public void service(AgiRequest request, AgiChannel channel)
                throws AgiException
        {
            String script;
            Binding binding;
    
            script = request.getScript();
            binding = new Binding();
            binding.setVariable("request", request);
            binding.setVariable("channel", channel);
    
            try
            {
                gse.run(script, binding);
            }
            catch (ResourceException e)
            {
                throw new AgiException("Unable to load groovy script '" + script + "'", e);
            }
            catch (ScriptException e)
            {
                throw new AgiException("Exception while running groovy script '" +
                        script + "'", e);
            }
        }
    }
    





References:




  * [Groovy Homepage](http://groovy.codehaus.org)


  * [Embedding Groovy](http://groovy.codehaus.org/Embedding+Groovy) in the Advanced Usage Guide






