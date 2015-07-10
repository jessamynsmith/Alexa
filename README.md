# Alexa

https://github.com/MrEggsalad/Echo-Roku-Voice-Control
Use Amazon Echo to control Roku 
utilizing Roku's External Control Guide API http://sdkdocs.roku.com/display/sdkdoc/External+Control+Guide .

0. Since Amazon Echo cannot access devices on your local area network, 
    set up port forwarding on your router for port 8060 to your Roku's IP.

0. In the AWS Management Console, select the Lambda eventing service.
0. Select the US East (N. Virginia) region. It's only region the Alexa Skills Kit supports.
1. If you have no Lambda functions yet, click Get Started Now. Otherwise, click Create a Lambda Function.
0. Enter a Name and Description for the function.
0. For the Code template, select Alexa Skills Kit Colors.
    This populates the inline code editor with code that implements a simple Alexa skill.



Set the Role to a basic execution role. This defines the AWS resources the function can access.
Click Create to save your new function.

https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interface-reference

https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/handling-requests-sent-by-alexa

WARNING: Using 'todo' items for identifying tasks. It seems like 'todo' processing at amazon performs extra processing on the text to clean it up when it's a todo.

https://github.com/dwdamon/echolib
is a Java library for using amazon echo
for configuration driven automation of tasks driven by the Amazon Echo Todo list. 

send tweets and start programs from Amazon echo.
with wakeup command "Alexa simon says"
