This page provies a baby-step by step tutorial on how to setup to 

## <a name="SkillDescription"> Description</a>

  call a phone by saying to Amazon Echo (referencing a skill AWS Lambda running Node.js):

Refer to https://developer.amazon.com/appsandservices/solutions/alexa/alexa-skills-kit/docs/developing-an-alexa-skill-as-a-lambda-function for more detailed information.


## <a name="ExamplePhrases"> Example Phrases</a>

  * <strong>Alexa, tell Phone to call Wilson</strong>

The code was inspired by Alan Cone's brilliant work shared at:

  https://github.com/MrEggsalad/Echo-Call-Lost-Phone

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


1. <a name="CreatePicture"> Create a picture</a>

   Find a graphic on http://images.google.com, then edit it to a 108x108 pixel png file. 

0. Click the icon to download the image.
1. For Category, select Home-Automation.
2. For Skill Description, type the <a href="#SkillDescription"> Description</a> above.
3. For Example Phrases, use <a href="#ExamplePhrases"> the one above</a>.
0. Click Save.

We do not submit for certification until the ARN End-point is generated next.


## <a name="Repo"> Establish and Edit Files</a>
The .zip file created will be uploaded in the next section.

If you have git client installed:

1. Open a git console
0. cd to the folder on your machine such as <strong>C:/githubs/wilsonmar</strong>.
0. Clone the whole repo:

  ```
  git clone https://github.com/wilsonmar/Alexa.git
  ```

  This would install the Alexa folder, containing folder <strong>Echo-Call-Lost-Phone</strong>
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
3. Edit line 6 to replace text defined by "var APP_ID = " with yours.

  ```
  var APP_ID = "amzn1.echo-sdk-ams.app.99999999...
  ```

4. Edit line 35 to replace "Name" with your name ("Wilson" in my case):

  ```
  case "Wilson":
  ```

5. Edit line 37 to replace ###-###-#### in var post_data with your phone number:

  ```
  var post_data = 'call%5Bnumber%5D=###-###-####&call ...
  ```

6. Leave as-is the IP address:

  ``` 
  host: '70.87.222.146',
  ```

6. Save the file.


## <a name="NewZIP"> Package .ZIP</a>
Compress into file <strong>Archive.zip</strong> containing these files:

  * index.js (the version just edited)
  * AlexaSkill.js
  
1. Navigate to the folder containing the files to be zipped.
2. Hold down Ctrl/command to select both the index.js file and AlexaSkill.js files.
3. Right-click or Control-click the combined files, then choose <strong>Compress</strong> from the shortcut menu.


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
1. Navigate to the folder containing the zip file.
2. Double click on the Archive.zip file to select it for upload.

1. For <strong>Handler</strong>, leave the default <strong>index.handler</strong>.
0. For <strong>Role</strong>, click on the list. If one is listed under <strong>Use existing role</strong>,
   select it. Otherwise, select <strong>* Basic execution role</strong> and when 
   a new tab appears. Leave the supplied IAM Role: Create a new IAM Role and Role Name: lambda_basic_execution.
  Click the blue <strong>Allow</strong> button at the lower-right of the screen.

0. Under the Advanced settings section, leave default Memory (MB) 128 and Timeout 3.
0. Click the blue <strong>Next</strong> button.
0. Click the blue <strong>Create function</strong> button.
1. Highlight the ARN at the upper-right corner of the screen, such as:

  ```
  arn:aws:lambda:us-east-1:234567891234:function:Phone 
  ```

0. Press Ctrl+C to copy it to the invisible Clipboard.


## <a name="Submit"> Submit for Certification</a>
Return to the Amazon Developer page at https://developer.amazon.com/edw/home.html

1. Replace the placeholder with the ARN copied from the previous step: 

  ``` 
  arn:aws:lambda:us-east-1:000000000000:function:myFunction
  ```

2. If the skill had already been submitted, wait for it to be editable again.

3. Otherwise, click <strong>Submit for Certification</strong>.
4. Click Yes to confirm.


## <a name="UseIt"> Use It</a>
4. Say <a href="#ExamplePhrases"> Example Phrases</a> to tell Alexa to call the phone.
5. Wait for your phone to ring.

