---
author: srt
comments: true
date: 2007-03-22 21:58:00+00:00
excerpt: "<p>Using a dependency injection framework like the <a href=\"http://www.springframework.org\"\
  >Spring Framework</a>\nto exernalize your configuration is often a great enhancement\
  \ for maintainance and deployment of your application.</p>\n\n<p>If you are building\
  \ an AGI application using Asterisk-Java the following code snippets will show you\n\
  how do it.</p>\n\n<pre class=\"brush: xml;\">\n&lt;beans xmlns=\"...\"&gt;\n\n\t\
  &lt;bean id=\"agiServer\" class=\"org.asteriskjava.fastagi.DefaultAgiServer\"\n\t\
  \tinit-method=\"startup\" destroy-method=\"shutdown\"&gt;\n\t\t&lt;property name=\"\
  mappingStrategy\" ref=\"mappingStrategy\" /&gt;\n\t&lt;/bean&gt;\n\n\t&lt;bean id=\"\
  mappingStrategy\" class=\"org.asteriskjava.fastagi.SimpleMappingStrategy\"&gt;\n\
  \t\t&lt;property name=\"mappings\"&gt;\n\t\t\t&lt;map&gt;\n\t\t\t\t&lt;entry key=\"\
  hello.agi\" value-ref=\"helloAgi\" /&gt;\n\t\t\t&lt;/map&gt;\n\t\t&lt;/property&gt;\n\
  \t&lt;/bean&gt;\n\t\n\t&lt;bean id=\"helloAgi\" class=\"HelloAgi\"&gt;\n\t\t&lt;property\
  \ name=\"voicePrompt\" value=\"tt-monkeys\" /&gt;\n\t&lt;/bean&gt;\n\n&lt;/beans&gt;\n\
  </pre>"
layout: post
permalink: externalize-your-agi-configuration-796/
slug: externalize-your-agi-configuration
title: Externalize your AGI Configuration
wordpress_id: 796
tags:
- agi
- asterisk-java
- spring
---

Using a dependency injection framework like the [Spring Framework](http://www.springframework.org)
to exernalize your configuration is often a great enhancement for maintainance and deployment of your application.





If you are building an AGI application using Asterisk-Java the following code snippets will show you
how do it:





Build your AGI script as before:




    
    
    public class HelloAgi extends BaseAgiScript
    {
        private String voicePrompt;
        
        public void setVoicePrompt(String voicePrompt)
        {
            this.voicePrompt = voicePrompt;
        }
        
        public void service(AgiRequest request, AgiChannel channel) throws AgiException
        {
            streamFile(voicePrompt);
        }
    }
    





This is really a very simple one but note the property voicePrompt that we added.
This property will be configured using Spring at deploy-time.





Next define an ApplicationContext (usually an XML file somewhere on the classpath):




    
    
    <beans xmlns="...">
    
    	<bean id="agiServer" class="org.asteriskjava.fastagi.DefaultAgiServer"
    		init-method="startup" destroy-method="shutdown">
    		<property name="mappingStrategy" ref="mappingStrategy" />
    	</bean>
    
    	<bean id="mappingStrategy" class="org.asteriskjava.fastagi.SimpleMappingStrategy">
    		<property name="mappings">
    			<map>
    				<entry key="hello.agi" value-ref="helloAgi" />
    			</map>
    		</property>
    	</bean>
    	
    	<bean id="helloAgi" class="HelloAgi">
    		<property name="voicePrompt" value="tt-monkeys" />
    	</bean>
    
    </beans>
    





This context configures your AGI script and defines the mapping of URL to script instance.





Finally provide a main() method somewhere to start the context:




    
    
    public class Main
    {
        public static void main(String[] args)
        {
            new ClassPathXmlApplicationContext("context.xml").start();
        }
    }
    





Now you are ready to run the application.




Follow Up:






  * [Integrating AGI and Apache Tomcat](/asterisk-java/2007/12/06/integrating_agi_and_apache_tomcat.html)


