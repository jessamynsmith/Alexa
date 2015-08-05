This is my intepretation and extension of the excellent
https://github.com/jjaquinta/EchoProofOfConcepts/tree/master/jo.echo.lambda
applied to my Mac OS Yosemite.

## <a name="Eclipse"> Eclipse</a>
0. Download <strong>Eclipse IDE for Java Developers</strong> from https://eclipse.org/downloads,
   file eclipse-java-mars-R-macosx-cocoa-x86_64.tar.gz (162 MB).
0. In a Terminal, `tar xyz eclipse-java-mars-R-macosx-cocoa-x86_64.tar.gz` to untar to a new folder.
1. Open a new finder window to copy the folder in the Application folder.

1. In Help | Install New Software, work with (add) http://aws.amazon.com/eclipse --
   the AWS Toolkit (plug-in) for Eclipse described at:
   http://docs.aws.amazon.com/AWSToolkitEclipse/latest/GettingStartedGuide/tke_setup.html

## <a name="AlexaSkillsKit">Java Sample AlexaSkillsKit.zip</a>
0. While signed into the Developer Console, download
   https://developer.amazon.com/edw/res/download/AlexaSkillsKit.zip

   In the <strong>samples</strong> folder, 
   helloworld and session folders each contain a
   <strong>slu</strong> folder containing the 
   IntentSchema.json and SampleUtterances.baf file:

      ```
MyColorIsIntent  my color is {dark brown|Color}
MyColorIsIntent  my color is {green|Color}
MyColorIsIntent  my favorite color is {red|Color}
MyColorIsIntent  my favorite color is {navy blue|Color}
WhatsMyColorIntent whats my color
WhatsMyColorIntent what is my color
WhatsMyColorIntent say my color
WhatsMyColorIntent tell me my color
WhatsMyColorIntent whats my favorite color
WhatsMyColorIntent what is my favorite color
WhatsMyColorIntent say my favorite color
WhatsMyColorIntent tell me my favorite color
WhatsMyColorIntent tell me what my favorite color is
      ```

      The intents specified (MyColorIntents and WhatsMyColorIntent) are defined in file
      <strong>IntentSchema.json</strong>

   These are the same as for the Node.js example.

   However, this set of sample assets was written to run on a Java, or more specifically, a J2EE server.

   So each folder in samples contains a Speechlet.java file.

   Also in the <strong>samples</strong> folder 
   is a <strong>build.xml</strong> file for the ant build tool to use:

      ```
<!-- Ant build script for compiling and running the Echo SDK samples. -->
<project name="Amazon Echo SDK Samples" default="run" basedir=".">
    <path id="java.sdk.classpath">
        <fileset dir="../lib" includes="**/*.jar"/>
        <fileset dir="../third-party" includes="**/*.jar"/>
        <pathelement location="."/>
    </path>

    <property name="disableRequestSignatureCheck" value="false"/>
    <property name="supportedApplicationIds" value=""/>
    <property name="timestampTolerance" value="150"/>

    <target name="run">
        <javac srcdir="." destdir="." classpathref="java.sdk.classpath"/>
        <java classname="Launcher" classpathref="java.sdk.classpath" fork="true">
            <sysproperty key="javax.net.ssl.keyStore" value=""/>
            <sysproperty key="javax.net.ssl.keyStorePassword" value=""/>
            <sysproperty key="com.amazon.speech.speechlet.servlet.disableRequestSignatureCheck"
                value="${disableRequestSignatureCheck}"/>
            <sysproperty key="com.amazon.speech.speechlet.servlet.supportedApplicationIds"
                value="${supportedApplicationIds}"/>
            <sysproperty key="com.amazon.speech.speechlet.servlet.timestampTolerance"
                value="${timestampTolerance}"/>
        </java>
    </target>
</project>
      ```

The <strong>Launcher.java</strong> file in turn references libraries in the
top-level "third-party" folder containing jar files in folder j2ee_servlet, Jetty.

The <a target="_blank" href="http://jakarta.apache.org/">Jakarta</a> folders were retired since 2011 by Apache
in favor of http://jmeter.apache.org/), and Jackson (for JSON processing) are used for testing.

<a target="_blank" href="http://www.slf4j.org/">Slf4j</a> 
is the Simple Logging Facade for Java, which serves as a facade to the Slf4j_log4j and log4j library.

The <a target="_blank" href="http://www.joda.org/joda-time/">Joda-time</strong> library 
provides a quality replacement for the poor Java date and time classes in standard Java.
From Java SE 8 onwards, users are asked to migrate to java.time (JSR-310).

In the lib folder is the <strong>alexa-skills-kit-1.0.120.0.jar</strong>
file which compresses a MANIFEST file describing code in folder com.amazon.speech.
