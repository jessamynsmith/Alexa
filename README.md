# Alexa

Based on https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/getting-started-guide

When a user asks Alexa a question or tells Alexa to do something, that request is sent 
thru the wi-fi over the public internet to the Alexa service in the Amazon cloud.
The service sends back text that Alexa converts to speech to the user. 

Borrowing a term from Android, <strong>intents</strong> are what a cloud-based service can handle,
using case-insensitive alphabetical characters.

An <strong>intent schema</strong> maps what services are processed based on users' spoken utterance text.

<strong>slots</strong> associated with an intent have a name and a type
https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interaction-model-reference

https://github.com/MrEggsalad/Echo-Roku-Voice-Control
Use Amazon Echo to control Roku 
utilizing Roku's External Control Guide API http://sdkdocs.roku.com/display/sdkdoc/External+Control+Guide .

0. Since Amazon Echo cannot access devices on your local area network, 
    set up port forwarding on your router for port 8060 to your Roku's IP.

Following:
https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/docs/developing-an-alexa-skill-as-a-lambda-function

0. In an internet browser, go to http://whatismyip.com to get your public IP address, such as 72.21.61.71.
1. Click "Check for Proxy".

0. In the AWS Management Console, select the Lambda eventing service.
1. Select the <strong>US East (N. Virginia)</strong> region, the only region supported by the Alexa Skills Kit.
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


https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/handling-requests-sent-by-alexa

WARNING: Using 'todo' items for identifying tasks. It seems like 'todo' processing at amazon performs extra processing on the text to clean it up when it's a todo.


## <a name="JavaSample"> Java Sample</a>
https://github.com/dwdamon/echolib
is a Java library for using amazon echo
for configuration driven automation of tasks driven by the Amazon Echo Todo list. 

send tweets and start programs from Amazon echo.
with wakeup command "Alexa simon says"
