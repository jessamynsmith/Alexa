

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
