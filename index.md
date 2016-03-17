---
layout: default
---

The Asterisk-Java package consists of a set of Java classes that allow
you to easily build Java applications that interact with an [Asterisk
PBX Server](http://www.asterisk.org/).

Asterisk-Java supports most features of the following Asterisk
interfaces:

-   [Fast Asterisk Gateway
    Interface](http://www.voip-info.org/wiki-Asterisk+AGI) (FastAGI)
-   [Asterisk Manager
    interface](http://www.voip-info.org/wiki-Asterisk+manager+API) (AMI).

Please start with the [tutorial]({{ site.url }}/tutorial/), the [frequently
asked questions]({{ site.url }}/faq/), or the API
reference.

## License

Asterisk-Java is provided under the terms of the [Apache License,
Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

## Download

Official releases and release candidates are available via Maven central:

    <dependency>
        <groupId>org.asteriskjava</groupId>
        <artifactId>asterisk-java</artifactId>
        <version>1.0.0-final</version>
    </dependency>

Please feel free to provide any feedback or ask for support via the
[Asterisk-Java users mailing list](https://lists.sourceforge.net/lists/listinfo/asterisk-java-users).

You can find the source code at:
{% include icon-github.html username="asterisk-java" %} /
[asterisk-java](https://github.com/asterisk-java/asterisk-java)

## Requirements

Asterisk-Java is compatible with Asterisk 1.0, 1.2, 1.4 and 1.6.

At runtime Asterisk-Java requires a Java Runtime Environment (JRE) of at
least version 1.6 (Java SE 6).

Of course you also need a working Asterisk server. When using the
Manager API be sure that it has been enabled (see [Asterisk config
manager.conf](http://www.voip-info.org/tiki-index.php?page=Asterisk%20config%20manager.conf)).

For logging Asterisk-Java will use
[log4j](http://logging.apache.org/log4j/) when available.
If you do not include log4j in your Classpath Asterisk-Java will use
java.util.logging.

If you choose to compile Asterisk-Java on your own you need a Java
Developer Kit (JDK) of at least version 1.6 (Java SE 6). To run the unit
tests you need [JUnit](http://www.junit.org/) and
[EasyMock](http://www.easymock.org/) in addition.

## Related Projects

[AsterFax](http://asterfax.sourceforge.net/) provides an
SMTP Fax gateway for the transmission of faxes using Asterisk and is
based on Asterisk-Java.\
Available under a modified GNU General Public License (Organizations
with more than one fax lines must purchase a commercial licence).

[Asterisk-JTAPI](http://asterisk-jtapi.sourceforge.net/)
is a JTAPI implementation for the Asterisk software PBX system. JTAPI is
a provider independent programming interface for Java to build
applications for computer telephony or to add support for it. JTAPI
covers a wide range of usage scenarios starting from controlling a
single telephone to a whole PBX system for example in call-centers.\
Asterisk-JTAPI builds on top of two other projects: Asterisk-Java, which
provides a Java interface to the Asterisk Manager API, and GJTAPI, which
provides a general framework for JTAPI interfaces.\
Available under Apache License.

[Asterisk
.NET](http://www.voip-info.org/wiki/view/Asterisk+.NET)
is a full port of Asterisk-Java to .NET. It supports both the Manager
API and FastAGI. The latest version is available from
[SourceForge](http://asterisk-dotnet.sourceforge.net).\
Available under Apache License.

[Asterisk-Java for
Mono/.NET](http://www3.mb.sympatico.ca/~chadk/) is a port
of Asterisk-Java to C\# for Mono, Microsoft's .NET Framework and
anything else that implements the basic portions of the framework. It
currently only supports the Manager API and is based on a pre-0.1
snapshot of Asterisk-Java.\
Available under Apache License.

[Jast Agi](http://tanesha.net/Wiki/JastAgi.html) is
another toolkit for writing Java applications that connect to Asterisk
using the FastAGI protocol. The lastest version introduces a
statemachine approach to handle AGI requests and uses java.nio to
process all requests in one Thread.\
Available under Apache License.

[OrderlyCalls](http://orderlycalls.sourceforge.net/)
supports writing Java based AGI Scripts using FastAGI. Support for the
Manager API was recently added.\
Available under a modified Lesser GNU General Public License (It is
prohibited to use it for automating 'cold-calling' and you need prior
written permission to provide or augment call queuing).

[JAsterisk](http://sourceforge.net/projects/jasterisk/)
is a set of JNI classes providing direct access to Asterisk PBX
functionality from Java. It is not a socket-level interface to Asterisk
(like Asterisk-Java) but a true Java-Asterisk integration at the Thread
level.
Available under GNU General Public License.

## Sponsors

Thanks to our sponsors:

-   JetBrains for providing a free license of [IntelliJ
    Idea](http://www.jetbrains.com/idea/).
-   [Atlassian](http://www.atlassian.com/) for providing
    a free license of the excellent
    [JIRA](http://www.atlassian.com/software/jira/) Bug
    tracker.
-   YourKit [Java Profiler](http://www.yourkit.com/).
