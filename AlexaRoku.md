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

      * Alexa, tell Roku to play
      * Alexa, tell Roku to pause
      * Alexa, tell Roku to forward

15) QUESTION: Is there a Privacy Policy URL and Terms of Use URL I can use without having my own website?

16) QUESTION: Is there a Privacy Policy URL I can use without having my own website?

17) Check the Export Compliance checkbox.

18) Click Save or, if you're ready, Submit for Certification.
