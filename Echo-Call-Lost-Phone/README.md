This page provies a baby-step by step tutorial on how to setup to 

## <a name="Description"> Description</a>

  Call a phone by saying to Amazon Echo running a skill AWS Lambda running node.

## <a name="ExamplePhrases"> Example Phrases</a>

  * <strong>Alexa, tell Phone to call me</strong>
  * Alexa, tell Phone to call Jack
  * Alexa, tell Phone to call Amy

The code is inspired by Alan Cone's brilliant work shared at:

  https://github.com/MrEggsalad/Echo-Call-Lost-Phone

## <a name="NewARN"> Create an Alexa Skill to get an ARN</a>

0. Use an internet browser to address 
  <a target="_blank" href="https://developer.amazon.com/edw/home.html#/">
  https://developer.amazon.com/edw/home.html</a>

0. Click the yellow <strong>Add a New Skill</strong> at the right.
1. For Name: Phone
2. For Invocation Name: Phone.
3. For Version: 1.0.
4. For Endpoint, click <strong>Lambda ARN (Amazon Resource Name)</strong>
5. In the Endpoint form field, enter: ???

 ``` 
arn:aws:lambda:us-east-1:000000000000:function:myFunction
 ```

0. Click Save.
0. Highlight the <strong>Application ID</strong> at the top of the screen and 
   press Ctrl+C to copy the string to the invisible Clipboard.

   amzn1.echo-sdk-ams.app.399228c6-3452-461b-92ef-7af1ff8a4111

  This will be pasted into other files.

0. Click Next.

0. <a name="IntentSchema"> Specify Intent Schema</a>

 ```
{
  "intents": [
    {
      "intent": "CallIntent",
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
0. <a name="SampleUtterances"> Specify Sample Utterances</a>

 ```
CallIntent call {Name|Control}
 ```

4. Replace "Name" with your name.
0. Click Next.
1. Click Enable so skill is enabled for testing on this account.
0. Click Next.

1. <a name="CreatePicture"> Create a picture</a>

   Find a graphic on http://images.google.com, then edit it to a 108x108 pixel png file. 

0. Click the icon to download the image.
1. For Category, select Home-Automation.
2. For Skill Description, type the description above.
3. For Example Phrases, use <a href="#ExamplePhrases"> the one above</a>.
0. Click Save.
1. Click <strong>Submit for Certification</strong>.


## <a name="NewZIP"> Package .ZIP</a>

7. and utilize intentSchema.json and 



## <a name="NewLambda"> New Lambda Amazon Web Service</a>

0. Use an internet browser to address <a target="_blank" href="http://console.amazon.com/">
   http://console.amazon.com/, the AWS Management Console</a>.
0. Select the AWS <strong>Lambda</strong> eventing service.
1. Select the <strong>US East (N. Virginia)</strong> region.

    Initially the only region supported by the Alexa Skills Kit was "US East (N. Virginia)".

    <a target="_blank" href="http://aws.amazon.com/about-aws/whats-new/2015/06/aws-lambda-available-in-asia-pacific-tokyo/">
    On Jun 29, 2015, availability of AWS Lambda was announced</a>
    forUS East (N. Virginia), US West (Oregon), EU (Ireland), and Asia Pacific (Tokyo) regions.
    
0. Click the blue <strong>Get Started Now</strong>. Otherwise, click Create a <strong>Lambda Function</strong>.
0. In <strong>Step 1: Select blueprint</strong>, scroll down and click <strong>Skip</strong>
   instead of clicking "alexa-skills-kit-color-expert".
0. In <strong>Step 2: Configure function</strong>, clicking the Learn More link creates a new tab.
0. For Name: <strong>Phone</strong> (starting with a capital letter), or type whatever you're building.

   For Description: `Phone call from the Echo via AWS Lambda running node`.
   
   This is different from the name spoken after Alexa, tell ...
   
0. For Runtime, select Node.js because the example has a .js file (AlexaSkill.js)
   to populate the inline code editor with code that implements a simple Alexa skill.
0. In the Lambda function code section, select <strong>Upload a .ZIP file</strong>.
1. For <strong>Handler</strong>, leave the default <strong>index.handler</strong>.
0. For <strong>Role</strong>, select the recommended <strong>* Basic execution role</strong>.

   A new tab appears. Leave the supplied IAM Role: Create a new IAM Role and Role Name: lambda_basic_execution.
   
0. Click the blue <strong>Allow</strong> button at the lower-right of the screen.
0. Under the Advanced settings section, leave default Memory (MB) 128 and Timeout 3.
0. Click the blue <strong>Next</strong> button.


0. Click Next to accept the default Alexa Skills Kit as the Event source type.
0. Specify Function Name: Whatever.
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

# Echo-Call-Lost-Phone
Use Amazon Echo to call your lost phone.

## Setup

Refer to https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/docs/developing-an-alexa-skill-as-a-lambda-function for more detailed information.

1. In index.js on line 35 replace "Name" with your name.
2. In index.js on line 37 replace ###-###-#### in var post_data with your phone number.
3. Compress index.js and AlexaSkill.js into a ZIP archive and upload to AWS Lambda.
4. Save and Invoke using the following:

 ```
{
  "version": "1.0",
  "session": {
    "new": false,
    "application": {
      "applicationId": "amzn1.echo-sdk-ams.app.[unique-value-here]"
    },
    "sessionId": "session1234",
    "attributes": {},
    "user": {
      "userId": null
    }
  },
  "request": {
    "type": "IntentRequest",
    "requestId": "request5678",
    "intent": {
      "name": "CallIntent",
      "slots": {
        "Control": {
          "name": "Control",
          "value": "Name"
        }
      }
    }
  }
}
 ```

6. Save everything and tell Alexa to do call you and wait for your phone to ring.

