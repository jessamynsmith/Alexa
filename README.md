# Alexa in Amazon Echo

<a target="_blank" href="https://cloud.githubusercontent.com/assets/300046/8626603/bb0aed78-2702-11e5-97f9-f6c974223b80.png">
<img align="right" src="https://cloud.githubusercontent.com/assets/300046/8626603/bb0aed78-2702-11e5-97f9-f6c974223b80.png" /></a>

Amazon Echo is the hardware. Alexa is the software that processes text and natural speech.
This system is pre-programmed for English speech-to-text and text-to-speech.

The paper that comes with Echo says to use a mobile app to set it up.
After you setup the wi-fi, you would go though what is at http://echo.amazon.com.
<a target="_blank" href="http://www.amazon.com/gp/help/customer/display.html?nodeId=201601770">
All about setup on this page</a>.

To right sound volume, twist the top ring clockwise, the direction mechanical watches move.

<a target="_blank" href="https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/getting-started-guide"
title="Amazon Echo User Flow from Getting Started Guide" ><img src="https://cloud.githubusercontent.com/assets/300046/8625357/72960afc-26fb-11e5-8a3b-f1320a09df13.png"
/></a>

1) When a user asks Alexa a question or tells Alexa to do something,

2) Echo converts user speech to text and sends that text
   thru wi-fi then over the public internet to your own web service somewhere or 
   <a href="#Lambda">Amazon's Lamda web service</a> 
   running in the Amazon Web Service (AWS) cloud infrastructure.

3) The web service returns a text response to Alexa software
    which converts text to speech the user hears.

4) Responses can also be displayed on the companion Amazon Echo mobile app
    as a <a href="#CardResponse"> card</a>.

## <a name="Press"> Press about the Echo</a>
* http://www.geekwire.com/2014/amazon-echo-house-superior-streaming-speaker-smarts/
  mentiones that Echo was first announced November 6, 2014.
  Initially, it was offered by invitation only for $99 to Prime members.

## <a name="Lambda"> Lambda Amazon Web Service</a>
http://aws.amazon.com/lambda/
is a back-end processing service that's more general than just processing Amazon Echo requests.

To develop a new Skill as a Lambda function, see
https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/docs/developing-an-alexa-skill-as-a-lambda-function

0. In the AWS Management Console, select the Lambda eventing service.
1. Select the <strong>US East (N. Virginia)</strong> region.

    Initially the only region supported by the Alexa Skills Kit was "US East (N. Virginia)".

    <a target="_blank" href="http://aws.amazon.com/about-aws/whats-new/2015/06/aws-lambda-available-in-asia-pacific-tokyo/">
    On Jun 29, 2015, availability of AWS Lambda was announced</a>
    forUS East (N. Virginia), US West (Oregon), EU (Ireland), and Asia Pacific (Tokyo) regions.
    
    Look for #awslambda in Twitter.

1. Click <strong>Get Started Now</strong>. Otherwise, click Create a Lambda Function.
0. Enter a Blueprint Name and Description for the function: <strong>Roku</strong>
0. Click <strong>alexa-skills-kit-color-expert</strong>
    to populate the inline code editor with code that implements a simple Alexa skill.
0. Click Next to accept the default Alexa Skills Kit as the Event source type.
0. Specify Function Name: Roku.
0. For Runtime Node.js, sample code is provided. You'll have to provide Java 8 code if you have that.
1. For Handler, leave as <strong>index.handler</strong>
0. Set the Role to <strong>basic execution role</strong> (as suggested) to define the AWS resources the function can access.
1. In the new IAM window, click Allow creating a new IAM role. The role becomes "lambda_basic_execution".
2. Click Next to accept defaul Memory of 128 and Timeout of 3.
2. Click Create Function to save your new function.
0. Click Test.
1. In another browser window, read through template JSON coding for various types at  https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interface-reference.
1. Edit the sample Event Template "Hello World".

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

Follow https://twitter.com/@lambdatips.

VIDEO: https://s3.amazonaws.com/awscomputeblogmedia/Lambda+Plus+Echo+Plus+Slack+Demo.mp4
shows the voice commands and code: 

```
Alexa, tell Slack to send it's time for lunch
```

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

## <a name="DeveloperConsole"> Developer Console</a>
https://developer.amazon.com/home.html


In this sample spoken by a user:

    “Alexa, ask Greeter to say hello world.”

    * "Alexa" is the wake word.
    * "ask" verb requests an "ability" aka <strong>skill</strong>.
    * "Greeter" is the intent (custom web service) to invoke.
    * "Say"
    * "hello world"

## <a name="Intents"> Intents</a>
Borrowing a term from Android, <strong>intents</strong> is what a cloud-based service can handle,
using case-insensitive alphabetical characters.

An <strong>intent schema</strong> maps what services are processed based on users' spoken utterance text.


The <strong>slots</strong> associated intents have a name and a type
https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interaction-model-reference

Slack receives the request in its endpoint at `https://hooks.slack.com/services/'.

https://github.com/MrEggsalad/Echo-Roku-Voice-Control
Use Amazon Echo to control Roku 
utilizing Roku's External Control Guide API http://sdkdocs.roku.com/display/sdkdoc/External+Control+Guide .


and to confirm: 

```
Alexa, what was my message
```



## <a name="PortForwarding"> Port Forwarding</a>
0. Since Amazon Echo cannot access devices on your local area network, 
    set up port forwarding on your router for port 8060 to your Roku's IP.

0. In an internet browser, go to http://whatismyip.com to get your public IP address, such as 72.21.61.71.
1. Click "Check for Proxy".


## <a name="AppID"> Application ID</a>
0. Copy the function ID such as "ARN - arn:aws:lambda:us-east-1:495111183449:function:Roku"
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


