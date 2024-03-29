This page (shortened to https://goo.gl/oM2EiL) provides a baby-step by step tutorial on how to set an Alexa skill running AWS Lambda Node.js service to make an automated (robot) call to a *static* phone number by saying to Amazon Echo:

## <a name="ExamplePhrases"> Example Phrases</a>

  <strong>Alexa, tell Phone to call Wilson</strong>

	* "Alexa" is the wake word.
	* "Phone" is the intent.
	* "Wilson" is the name to send.

As of this writing, even though the Amazon Echo hardware has both microphones and spearkers,
Alexa cannot function like a speakerphone.

	* "Alexa call my phone"

is what initiatiates IFTTT recipe
https://ifttt.com/recipes/288400-find-your-phone-by-asking-alexa
to combine the Alexa Channel and Phone Call Channel.

The code described here was inspired by Alan Cone's brilliant work shared at:
https://github.com/MrEggsalad/Echo-Call-Lost-Phone

Refer to https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/docs/developing-an-alexa-skill-as-a-lambda-function for more detailed information.

??? in this marks my "doubts", where I'm stuck or don't understand.


## <a name="Stsps"> Steps</a>
<a target="_blank" title="alexa_skill_diagram_v01" href="https://cloud.githubusercontent.com/assets/300046/8888819/ea40f816-327a-11e5-91ed-550b1fea01dd.png">
<img alt="alexa_skill_diagram_v01" src="https://cloud.githubusercontent.com/assets/300046/8888819/ea40f816-327a-11e5-91ed-550b1fea01dd.png" /></a>


## <a name="TOC"> Contents</a>
Here are the steps to make this work:

0. <a href="#NewAppId"> Create an Alexa Skill to get the Application ID</a>
	0. <a name="SampleUtterances"> Specify Sample Utterances</a>
	0. <a name="CreatePicture"> Create a picture</a>
0. <a href="#Repo"> Establish and Edit Files</a>
0. <a href="#Index.JS"> Edit Index.js File</a>
0. <a href="#NewZIP"> Package .ZIP</a>
0. <a href="#NewLambda"> Create New Lambda Amazon Web Service</a>
0. <a href="#SampleEventTest"> Define Sample Event Template</a>
0. <a href="#Submit"> Submit for Certification</a>
0. <a href="#TestWS"> Test Web Service</a>
0. <a href="#UseIt"> Talk to Alexa to Really Use It</a>
0. <a href="#ManageMemory"> Manage Memory</a>
0. <a href="#ManageLogs"> Manage Log History</a>


## <a name="NewAppId"> Create an Alexa Skill to get the Application ID</a>

0. Use an internet browser to address 
  <a target="_blank" href="https://developer.amazon.com/edw/home.html#/">
  https://developer.amazon.com/edw/home.html</a>

0. Click the yellow <strong>Add a New Skill</strong> at the right.
1. For Name: Phone
2. For Invocation Name: Phone.
3. For Version: 1.0.
4. For Endpoint, click <strong>Lambda ARN (Amazon Resource Name)</strong>
5. In the Endpoint form field, enter a placeholder:

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
0. <a name="SampleUtterances"> Specify Sample Utterances</a>, replacing "Name" with your name. For example, from:

  ```
  CallIntent call {Name|Control}
  ```

  to:

  ```
  CallIntent call {Wilson|Control}
  ```

0. Click Next.
1. Click Enable so skill is enabled for testing on this account.
0. Click Next.


0. <a name="CreatePicture"> Create a picture</a>
  <a target="_blank" href="https://cloud.githubusercontent.com/assets/300046/8825227/a7a9b624-303a-11e5-854d-a0e22c897cda.jpg">
  <img align="right" src="https://cloud.githubusercontent.com/assets/300046/8825227/a7a9b624-303a-11e5-854d-a0e22c897cda.jpg" /></a>
   Find a restriction-free graphic on <a target="_blank" href="http://images.google.com">
   http://images.google.com</a>, then edit it to a 108x108 pixel png file. 

0. Click the icon to download the image.
1. For Category, select Home-Automation.
2. For Skill Description, type the <a name="SkillDescription"> Description</a>, such as:

   Phone call from the Echo via AWS Lambda running node 

3. For Example Phrases, use <a href="#ExamplePhrases"> the one above</a>.
0. Click Save.

We do not submit for certification until the ARN End-point is generated next.


## <a name="Repo"> Establish and Edit Files</a>
The .zip file created will be uploaded in the next section.

If you have git client installed:

1. Open a git console
0. Create the folder path on your machine, such as <strong>C:/githubs/wilsonmar</strong>.
0. <strong>cd</strong> to the folder path to allow git to create the sub-folder for the new repo.
0. Clone the repo:

  ```
  git clone https://github.com/wilsonmar/Alexa.git
  ```

  This would create the repo's top folder (Alexa), containing folder <strong>Echo-Call-Lost-Phone</strong>
  which contains this tutorial and two files: index.js and AlexaSkill.js.

Alternately, if you do NOT have git client installed:

1. Create a folder on your machine such as <strong>C:/githubs</strong>.
2. Create a folder named <strong>C:/githubs/wilsonmar/Alexa/Echo-Call-Lost-Phone</strong>.
2. On the webpage https://github.com/wilsonmar/Alexa/Echo-Call-Lost-Phone,
   click <strong>Download ZIP</strong>.
4. Navigate to your Downloads folder for file <strong>Alexa-master.zip</strong>.
5. Copy 

## <a name="Index.JS"> Edit Index.js File</a>
1. Invoke a text editor.
2. Navigate to and open file <strong>index.js</strong>
3. Edit line 6 to replace text defined by "var <strong>APP_ID</strong> = " with the one <a href="#NewAppId">created above</a>.

  ```
  var APP_ID = "amzn1.echo-sdk-ams.app.99999999...
  ```

4. Add response text to be spoken by Alexa to acknowledge the request:

	```
	response.tell("Phone to Wilson placed");
	```
	
5. Edit line 35 to replace "Name" with the name associated with a phone ("Wilson" in my case):

  ```
  case "Wilson":
  ```

6. Edit line 37 to replace ###-###-#### in var post_data with <strong>your phone number</strong>:

  ```
  var post_data = 'call%5Bnumber%5D=###-###-####&call ...
  ```

7. Leave as-is the IP address:

  ``` 
  host: '70.87.222.146',
  ```

8. Use a browser to visit the IP address http://70.87.222.146 (PhoneMyPhone.com) and 
   subscribe to their email so you hear when they announce changes.

  Also consider a donation to keep their server running.

9. Save the file.


## <a name="NewZIP"> Function Package .ZIP</a>
Compress into file <strong>Archive.zip</strong> containing these files:

  * index.js (the version just edited)
  * AlexaSkill.js
  
1. Navigate to the folder containing the files to be zipped.
2. Hold down Ctrl/command to select both the index.js file and AlexaSkill.js files.
3. Right-click or Control-click the combined files, then choose <strong>Compress</strong> from the shortcut menu.
4. Make sure that the zip file is less the <strong>50 MB</strong> limit imposed for compressed function zip files
   as noted in
   https://docs.aws.amazon.com/lambda/latest/dg/limits.html

## <a name="NewLambda"> Create New Lambda Amazon Web Service</a>

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

   For <a href="#SkillDescription">Description</a>: `Phone call from the Echo via AWS Lambda running node`.
   
   This is different from the name spoken after Alexa, tell ...
   
0. For Runtime, select Node.js because the example has .js files (index.js and AlexaSkill.js)
   to populate the inline code editor with code that implements a simple Alexa skill.
0. In the Lambda function code section, select <strong>Upload a .ZIP file</strong>.
0. Click the gray <strong>Upload</strong> button.
1. Navigate to the folder containing the zip file (Archive.zip).
2. Click to select the .zip file for upload.
3. Click the <strong>Open</strong> button.

1. For <strong>Handler</strong>, leave the default <strong>index.handler</strong>.
0. For <strong>Role</strong>, click on the list. If one is listed under <strong>Use existing role</strong>,
   select it. Otherwise, select <strong>* Basic execution role</strong> and when 
   a new tab appears. Leave the supplied IAM Role: Create a new IAM Role and Role Name: lambda_basic_execution.
  Click the blue <strong>Allow</strong> button at the lower-right of the screen.

0. Under the Advanced settings section, leave default Memory (MB) <strong>128</strong> and Timeout <strong>3</strong>.
0. Click the blue <strong>Next</strong> button.
0. Click the blue <strong>Create function</strong> button.
1. Highlight the ARN at the upper-right corner of the screen, such as:

  ```
  arn:aws:lambda:us-east-1:234567891234:function:Phone 
  ```

0. Press Ctrl+C to copy it to the invisible Clipboard.


## <a name="SampleEventTest"> Define Sample Event Template</a>
0. Select Sample event template drop-down <strong>Amexa Intent - MyColorIs</strong>.

0. In place of the default provided, paste the following from file <strong>SampleTempate.json</strong>:

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

0. Change the <strong>applicationId</strong> with the <a href="#NewAppId"><strong>APP_ID</strong> created above</a>.

  ```
  "applicationId": "amzn1.echo-sdk-ams.app.[unique-value-here]"
  ```

  After pasting, remove leading and trailing blank spaces inside the double-quote characters.

4. Replace "Name" with the name associated with a phone ("Wilson" in my case):

  ```
   "value": "Name"
  ```

5. Leave "session1234" as-is.
6. Leave "request5678" as-is.
7. Click <strong>Submit</strong>.


## <a name="Submit"> Submit for Certification</a>
Return to the Amazon Developer page at https://developer.amazon.com/edw/home.html

1. Replace the placeholder with the ARN copied from the previous step: 

  ``` 
  arn:aws:lambda:us-east-1:000000000000:function:myFunction
  ```

2. If the skill had already been submitted, wait for it to be editable again.

3. Otherwise, click <strong>Submit for Certification</strong>.
4. Click Yes to confirm.


## <a name="TestWS"> Test Web Service</a>
On the console.aws.amazon.com web page:

0. Click the blue <strong>Test</strong> button to emulate what Alexa sends to the Amazon server over the public internet
   and the Lambda eventing web service.

0. Your phone should now ring.

0. If you answer, an automated voice says "Hello there ...".

0. Under the Monitoring tab, it should say "Execution result: succeeded" with this JSON:

 ```
 {
  "version": "1.0",
  "response": {
    "outputSpeech": {
      "type": "PlainText",
      "text": "Phone to Wilson placed"
    },
    "shouldEndSession": true
  },
  "sessionAttributes": {}
}
 ```

   In real life, Alexa would say the outputSpeech text above.
 

## <a name="UseIt"> Talk to Alexa to Really Use It</a>
0. Say to Alexa <a href="#ExamplePhrases"> Example Phrases</a> to tell Alexa to call the phone.

  If Alexa responds "I didn't hear a person to call", give up ???
  
  QUESTION: What is the procedure for "debugging" if Alexa doesn't understand a command???

0. Wait for your phone to ring. For how long to expect waiting, see below.


## <a name="ManageMemory"> Manage Memory</a>
On the console.aws.amazon.com web page:

0. Wait for a few minutes for the <strong>Invocation count</strong> and other charts to update under <strong>CloudWatch metris at a glance</strong>.
1. Click on the refresh ("spinner") icon.

2. Click somewhere in the Invocation duration graph, 
   then mouse over the peak of the blue Maximum, green Average, and orange Minimum lines.

0. At the bottom of the page, note the <strong>Billed duration</strong> (1000 ms for me),
   where 1000 ms (millisecond) = 1 second.

0. At the bottom of the page, compare the 
   <strong>Resources configured</strong> (128 MB) versus 
   <strong>Max memory used</strong> (27 MB).

0. Adjust the Resources configured if need be.


## <a name="ManageLogs"> Manage Log History</a>
On the console.aws.amazon.com web page:

0. Click the <strong>Monitoring</strong> tab.
1. Click View logs in CloudWatch. This opens a new browser tab.

  Log Groups > should say <strong>aws/Lambda/Phone</strong> which was automatically created when the service was created.

2. Click the checkbox to the right of <strong>Log Streams</strong>.
3. Click <strong>Delete Log Stream</strong>.

