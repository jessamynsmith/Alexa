This page aims to provide to experienced programmers a deep technical introduction to 
Amazon's Echo hardware and associated
Alexa software.

This repo contains a folder for each sample Alexa Skills:

* <a href="Echo-Call-Lost-Phone">Echo-Call-Lost-Phone</a> 
  makes use of a Lambda service which calls a 3rd-party web service that robot-calls a phone number.

* <a href="AlexaRoku.md">Roku</a> involves setting up a connection over the public internet to the Roku box.

* <a href="AmazonJavaSample.md"> AmazonJavaSample</a>
  is provided by Amazon to use a Java program.

* Slack channel update
* Sample provided by Amazon in Java

* Phillips
* Wink
* Tweet to send
* Facebook blog to create
* Wordpress blog entry to create

## <a name="Competitors"> Competitors</a>
Alexa responds to utterances from the many shows doing fake voice recognition:
* Computer, tea, earl gray. hot.
* https://www.luis.ai/?ref=1981319 Microsoft's 

## <a name="Lambda"> Lambda Amazon Web Service</a>
http://aws.amazon.com/lambda/
is a back-end processing service that's more general than just processing Amazon Echo requests.
Kinda like http://ifttt.com and http://zapier.com.

http://aws.amazon.com/api-gateway/ provides HTTPS secure access.

A <strong>Lambda function</strong> consists of your code, associated dependencies, and configuration.

To develop a new Skill as a Lambda function, see
https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/docs/developing-an-alexa-skill-as-a-lambda-functi

   Look for #awslambda in Twitter.


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





## <a name="Slack"> Slots in 3rd Party API (Slack)</a>
https://aws.amazon.com/blogs/compute/slack-dictation-an-amazon-echo-and-aws-lambda-demo/
by Tim Wagner (https://twitter.com/timallenwagner)
presents an example using AWS Lambda to post text Alexa converts to text in a Slack chat room.

Follow Tim's tweets at https://twitter.com/@lambdatips.

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


## <a name="RequestTypes"> Request Types</a>
If request sent by Alexa are being process by 
the Java library, the SpeechletServlet class determines the type of request
and calls the corresponding Speechlet method for the Session object:

* <a target="_blank" href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interface-reference#LaunchRequest">LaunchRequest</a> by Java onLaunch()

* <a target="_blank" href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interface-reference#IntentRequest">IntentRequest</a> by Java onIntent()

* <a target="_blank" href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interface-reference#SessionEndedRequest">SessionEndedRequest</a> by Java onSessionEnded()

<a target="_blank" href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interface-reference">Alexa Skills Kit Interface Reference</a>





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

https://www.youtube.com/watch?v=ZxXWphy6Rs4 An Introduction to Amazon Echo and the Alexa Skills Kit
July 3, 2015 by David Isbitski, Amazon Echo Evangelist.
His video is described at 
https://developer.amazon.com/public/community/post/Tx9JUX8VZNUZY5/Free-Video-Training-An-Introduction-to-Amazon-Echo-and-the-Alexa-Skills-K
