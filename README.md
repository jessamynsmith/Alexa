# Alexa in Amazon Echo

This page provides to experienced programmers a deep technical introduction to 
Amazon's Echo hardware and associated
Alexa software.


<a target="_blank" href="https://cloud.githubusercontent.com/assets/300046/8626603/bb0aed78-2702-11e5-97f9-f6c974223b80.png">
<img align="right" src="https://cloud.githubusercontent.com/assets/300046/8626603/bb0aed78-2702-11e5-97f9-f6c974223b80.png" /></a>
## <a name="Unboxing"> Unboxing and Setup</a>

Amazon Echo is the 9.25-inch-tall (23.5 cm) canister hardware with 2 speakers and 7 microphones. 

Alexa is the "Voice Assistant" software that is pre-programmed for English speech-to-text and text-to-speech.

The paper that comes with Echo says to use a mobile app to set it up.
But there is also  http://echo.amazon.com for the desktop browsers, according to 
<a target="_blank" href="http://www.amazon.com/gp/help/customer/display.html?nodeId=201601770">
All about setup on this page</a>.

To right sound volume, twist the top ring clockwise, the direction mechanical watches move.

<a target="_blank" href="https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/getting-started-guide"
title="Amazon Echo User Flow from Getting Started Guide" ><img src="https://cloud.githubusercontent.com/assets/300046/8625357/72960afc-26fb-11e5-8a3b-f1320a09df13.png"
/></a>

1) Connect Alexa to an Amazon account that has Prime membership because
   that is needed to play music.
  
2) Alexa knows where you live from you Amazon.com account address.
   Change the ZIP code in the Echo app.

3) Connect Alexa to your Google Calendar and ToDo list.
   
4) Ask Alexa a natural-language question such as:

      "Alexa, how old are you?"

   Echo converts user speech to text and sends that text
   thru wi-fi then over the public internet to a web service.
   
   The web service returns a text response to Alexa software
    which converts text to speech the user hears.

      "I was released November 6, 2014"

   Responses can also be displayed on the companion Amazon Echo mobile app
    as a <strong>card</strong>. 

   QUESTION: Do requests to Bing track back to the user making the request such that the subject follows the user
   in ads?
   
5) Tell Alexa to invoke a specific <strong> intent</strong> such as:

      "Alexa, tell ... to ..."
   
   You can create your own web service somewhere or as a "push event source" to
   <a href="#Lambda">Amazon's Lamda web service</a> 
   running in the Amazon Web Service (AWS) cloud infrastructure.
   
   “Developing an Alexa Skill as a Web Service”       (https://developer.amazon.com/public/solutions/alexa/alexa-skillskit/docs/developing-an-alexa-skill-as-a-web-service)
      notes that the web service must use HTTPS which requires an Amazon trusted certificate
      and validate the requests are coming from Amazon. 

QUESTION: Can Alexa "push" announcement of appointments in my Google calendar?

6) Tell Alexa to invoke a specific <strong> intent</strong> such as:

      "Alexa, tell ... to ..."
   
   The response to launch commands like this is a <strong>welcome message</strong>.


Even though Alexa is able to recognize much, it is rather primative compared to what Google is working on:
http://www.aiyellowpage.com/content/google-you-can-talk-about-life-with-robots/


## <a name="Press"> Blogs about This</a>
* http://www.geekwire.com/2014/amazon-echo-house-superior-streaming-speaker-smarts/
  mentiones that Echo was "announced" November 6, 2014,
  but did not begin shipments until December to beta customers offered an invitation to pay $99 as Prime members.

  The author reports that <strong>Alexa stores a recording of your actual voice</strong>.

* http://www.cnet.com/products/amazon-echo-review/ June 23, 2015
   says Alexa does a better job understanding what you're saying than today's iOS (Siri), Android (Google Now) and Windows (Cortana) mobile devices.

* http://www.wsj.com/articles/amazon-echo-review-talking-helper-alexa-is-no-match-for-siri-1422997829


## <a name="Social"> Social</a>
* <a target="_blank" href="https://forums.developer.amazon.com/forums/category.jspa?categoryID=48">
  The Alexa section of Amazon's Developer Forum</a>


## <a name="ExternalIntents"> External Intents</a>
Amazon provides some interfaces:

   * Phillips
   * Wink
 
3rd-party interfaces:

      * Roku
      * Tweet to send

            * Alexa, ask Twitter to say "whatever".

      * Facebook blog to create

            * Alexa, ask Facebook to say "whatever".

      * Wordpress blog entry to create

## <a name="Lambda"> Lambda Amazon Web Service</a>
http://aws.amazon.com/lambda/
is a back-end processing service that's more general than just processing Amazon Echo requests.
Kinda like http://ifttt.com and http://zapier.com.

http://aws.amazon.com/api-gateway/ provides HTTPS secure access.

A <strong>Lambda function</strong> consists of your code, associated dependencies, and configuration.

## <a name="NewLambda"> New Lambda Amazon Web Service</a>
To develop a new Skill as a Lambda function, see
https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/docs/developing-an-alexa-skill-as-a-lambda-function

0. In the <a target="_blank" href="http://console.amazon.com/">
   AWS Management Console</a>, select the Lambda eventing service.
1. Select the <strong>US East (N. Virginia)</strong> region.

    Initially the only region supported by the Alexa Skills Kit was "US East (N. Virginia)".

    <a target="_blank" href="http://aws.amazon.com/about-aws/whats-new/2015/06/aws-lambda-available-in-asia-pacific-tokyo/">
    On Jun 29, 2015, availability of AWS Lambda was announced</a>
    forUS East (N. Virginia), US West (Oregon), EU (Ireland), and Asia Pacific (Tokyo) regions.
    
    Look for #awslambda in Twitter.

1. Click <strong>Get Started Now</strong>. Otherwise, click Create a <strong>Lambda Function</strong>.
0. Enter a <strong>Blueprint</strong> Name and Description for the function: <strong>Roku</strong>
0. Click <strong>alexa-skills-kit-color-expert</strong>
    to populate the inline code editor with code that implements a simple Alexa skill.
0. Click Next to accept the default Alexa Skills Kit as the Event source type.
0. Specify Function Name: Roku.
0. For Runtime Node.js, sample code is provided. You'll have to provide Java 8 code if you have that.
1. For Handler, leave as <strong>index.handler</strong>
0. Set the Role to <strong>basic execution role</strong> (as suggested) to define the AWS resources the function can access.
1. In the new IAM window, click Allow creating a new IAM role. The role becomes "lambda_basic_execution".
2. Click Next to accept defaul Memory of 128 and Timeout of 3.
2. Click <strong>Create Function</strong> to save your new Lambda function.
0. Click Test.
1. In another browser window, read through template JSON coding for various types at  https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interface-reference.
1. Edit the sample <strong>Event Template</strong> "Hello World".

```
{
  "key1": "value1",
  "key2": "value2",
  "key3": "value3"
}
```


## <a name="Slack"> Slots in 3rd Party API (Slack)</a>
https://aws.amazon.com/blogs/compute/slack-dictation-an-amazon-echo-and-aws-lambda-demo/
by Tim Wagner (https://twitter.com/timallenwagner)
presents an example using AWS Lambda to post text Alexa converts to text in a Slack chat room.

Also follow tweets at https://twitter.com/@lambdatips.

VIDEO: https://s3.amazonaws.com/awscomputeblogmedia/Lambda+Plus+Echo+Plus+Slack+Demo.mp4
shows the voice commands and code: 

```
Alexa, tell Slack to send it's time for lunch
```

   * "Alexa" or "Amazon" are the <strong>wake word</strong> 
   * "tell" or "ask" verb requests an "ability" aka <strong>skill</strong>.
   * "Greeter" is the <strong>intent</strong> (custom web service) to invoke.
   * "send" or "Say" 
   * "it's time for lunch" is the <strong>message text</strong>.

If we capture the unencrypted request body, the relevant part is: 

```
  "slots": {
    "Message": {
      "name": "Message",
      "value": "it's time for lunch"
```

<strong>"slots"</strong> is keyword that must be specified.
"Message" appears twice: once as the identifier and another as ???.

There is a "outputSpeech" 

```
{
  "version": "1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "PlainText",
      "text": "Welcome to the Alexa Skills Kit sample, Please tell me your favorite color by saying, my favorite color is red"
    },
```

## <a name="CardResponse"> Card Response</a>
What is displayed in the Amazon Echo mobile app is defined in a "card":

```
"card": {
      "type": "Simple",
      "title": "SessionSpeechlet - Welcome",
      "content": "SessionSpeechlet - Welcome to the Alexa Skills Kit sample, Please tell me your favorite color by saying, my favorite color is red"
    },
```

A <strong>reprompt</strong> should be defined for when the user does not respond as expected.

```
    "reprompt": {
      "outputSpeech": {
        "type": "PlainText",
        "text": "Please tell me your favorite color by saying, my favorite color is red"
      }
    },
    "shouldEndSession": false
  }
}
```

https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-voice-design-best-practices
describes Alexa Skills Kit Voice Design Best Practices:

* Give users options
* Avoid Overwhelming Users with Too Many Choices
* Obtain One Piece of Information at a Time

These options are defined ???

## <a name="RokuFiles"> Roku Github Files</a>
https://github.com/MrEggsalad/Echo-Roku-Voice-Control
presents a sample set of files to setup Amazon Echo to control Roku
utilizing Roku's External Control Guide API http://sdkdocs.roku.com/display/sdkdoc/External+Control+Guide .

The files:

* AlexaSkill.js
* index.js
* intentSchema.json
* SampleUtterances.txt
* .gitattributes
* .gitignore
* README.md
* LICENSE.txt

Let's use the contents of these files to setup our own Roku voice controller.

### <a name="PortForwarding"> Port Forwarding</a>
0. Since Amazon Echo cannot access devices on your local area network, 
    set up port forwarding on your router for port 8060 to your Roku's IP.

0. In an internet browser, go to http://whatismyip.com to get your 
      <strong>public IP address</strong>, such as 72.21.61.71.

1. Click "Check for Proxy".

0. Find the Roku IP address on the TV at Roku menu: Settings | Network, Enter.
 
      VIDEO: https://www.youtube.com/watch?v=757nLvUvIgM
      
      On your computer go to network and sharing center. You will see your computer, your network, and the internet. 
      Click on your network. Once inside your router, your computer will see the roku player. 
      Click on it and you'll see the ip address and mac address.
 
      Or see http://photobridge.roku.com/downloads/pb_support_downloads/StaticIPAddress_HD1000.pdf

      NOTE: The Roku OS is only able to get an IP via DHCP 
      
### <a name="DeveloperConsole"> Developer Console</a>
1) Sign directly into the Alexa Developer Console at <a target="_blank" href=""https://developer.amazon.com/home.html">
   https://developer.amazon.com/home.html</a> rather than the 
   <a target="_blank" href="https://developer.amazon.com/edw/home.html#/"> Dashboard to all services</a>.

2) Flip back to the <a href="#NewLambda"> AWS Console</a>.
   Use your mouse to highlight the ARN string (without the "ARN - ", such as:

      arn:aws:lambda:us-east-1:123456789101:function:Roku

3) Press Ctrl+C to copy into the clipboard.

4) In the Developer Console, click the ApplicationID box and press Ctrl_V to paste.

5) Specify the skill name (Roku) and invocation name, and version 

    See Invocation Name Guidelines at
    https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/choosing-the-invocation-name-for-an-alexa-skill
    
6) Click in the <strong>Endpoint*</strong> box and press Ctrl_V to paste the Lambda ARN, such as:

      amzn1.echo-sdk-ams.app.b1bf9000-1111-2222-3333-30b6bacc90fd

      amzn1.echo-sdk-ams.app.[unique-value-here]

7) Click Next.

8) Copy the contents of the Roku Github repo file <strong>intentSchema.json</strong> and paste into the 
   <strong>Intent Schema*</strong> box.
   The schema of user intents in JSON format
   is described at 
   https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/docs/defining-the-voice-interface

```
{
  "intents": [
    {
      "intent": "RokuIntent",
      "slots": [
        {
          "name": "Control",
          "type": "LITERAL"
        }
      ]
    }
  ]
}
```

      There is only one slot - a LITERAL named Control to handle a finite set of known values.

9) Copy the contents of the Roku Github repo file <strong>SampleUtterances.txt</strong> and paste into the 
 Sample Utterances box.
 These are phrases end users say to interact with this skill. 
 For better results, provide as many samples as you can.
 For more information, see Defining the Voice Interface for an Alexa skill at
  https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/docs/defining-the-voice-interface

   The Developer's Console only allows up to 200,000 characters in the utterance field.

<img align="right" src="https://cloud.githubusercontent.com/assets/300046/8628873/b0840f36-2713-11e5-8a7e-8042fbe82275.png"
alt="roku-108x108.png" />
10) Copy from the Roku Github repo file <strong>roku-108x108.png</strong> and paste into the 
    Size 108x108 pixels, in PNG or JPG format. This is displayed in the Echo app. 

11) Click <strong>Image</strong> and select the path and file.

12) For Category, select Home Automation.

13) For Skill Description, type "Control Roku without a remote by talking to Alexa living in the Amazon Echo".

14) Some Sample Phrases:

      * Alexa, have Roku play
      * Alexa, have Roku pause
      * Alexa, have Roku forward

15) QUESTION: Is there a Privacy Policy URL and Terms of Use URL I can use without having my own website?

16) QUESTION: Is there a Privacy Policy URL I can use without having my own website?

17) Check the Export Compliance checkbox.

18) Click Save or, if you're ready, Submit for Certification.


## <a name="AlexaSkillsKit">Java Sample AlexaSkillsKit.zip</a>
While signed into the Developer Console, download
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


## <a name="AlexaLambdaSamleKit">AlexaLambdaExamples.zip</a>
While signed into the Developer Console, download
https://developer.amazon.com/edw/res/download/AlexaLambdaExamples.zip
Unzip it. There are several examples. In each sample folder are a src folder and speechAssets folder.

* helloWorld
* HistoryBuff : a skill that gives historical information that happened on a user provided day.
* MinecraftHelper : a simple skill that responds to the user's recipe queries with formulas.
* Savvy Consumer : a skill that looks up a category on Amazon and returns the best selling products.
* ScoreKeeper : a skill that can keep score of a game.
* SpaceGeek : a simple skill that responds to the user with a space fact.
* TidePooler : a skill that looks up tide information for various cities.
* WiseGuy : a skill that tells knock knock jokes, a multi-turn dialog using a JavaScript array in index.js,
      with these custom intents in file IntentSchema.json:

      * TellMeAJokeIntent
      * WhosThereIntent
      * SetupNameWhoIntent
      * HelpIntent

The <strong>AlexaSkill.js</strong> file contains prototype of requestHandlers:

      * LaunchRequest
      * IntentRequest
      * SessionEndedRequest
      
IntentHandlers:

      * onSessionStarted
      * onLaunch
      * onIntent
      
      

## <a name="Intents"> Intents</a>
Borrowing a term from Android, <strong>intents</strong> is what a cloud-based service can handle,
using case-insensitive alphabetical characters.

An <strong>intent schema</strong> maps what services are processed based on users' spoken utterance text.


The <strong>slots</strong> associated intents have a name and a type
https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interaction-model-reference

Slack receives the request in its endpoint at `https://hooks.slack.com/services/'.


## <a name="Intents"> Other</a>

and to confirm: 

```
Alexa, what was my message
```



## <a name="AppID"> Application ID</a>
0. Copy the function ID such as "ARN - arn:aws:lambda:us-east-1:495111183449:function:Roku"
   ??? ARN (Amazon Resource Name)
   Application ID amzn1.echo-sdk-ams.app.here

    ```
    /*
    if (event.session.application.applicationId !== "amzn1.echo-sdk-ams.app.[unique-value-here]") {
    */
    ```

0. Zip up
0. Upload the zip file to Amazon.

https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/handling-requests-sent-by-alexa

WARNING: Using 'todo' items for identifying tasks. It seems like 'todo' processing at amazon performs extra processing on the text to clean it up when it's a todo.


## <a name="JavaSample"> Java Sample</a>
https://github.com/dwdamon/echolib
is a Java library for using amazon echo
for configuration driven automation of tasks driven by the Amazon Echo Todo list. 

send tweets and start programs from Amazon echo.
with wakeup command "Alexa simon says"


## <a name="Laravel"> Laravel PHP compatibility</a>
https://github.com/develpr/alexa-app

Laravel is a PHP framework.


## <a name="Node"> Node.JS example</a>
http://docs.aws.amazon.com/lambda/latest/dg/getting-started.html


## <a name="SmartThings"> SmartThings</a>
https://community.smartthings.com/t/playing-around-with-amazon-echo-technical-interface-discussion/14887/314
