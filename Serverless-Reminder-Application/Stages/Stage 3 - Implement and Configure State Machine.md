## Serverless Reminder Application

# STAGE 3A - Create State Machine Role

In this stage of the demo you need to create an IAM role which the state machine will use to interact with other AWS services.  

Refer to the CFN template give, create the stack

Wait for the Stack to move into the `CREATE_COMPLETE` state before moving into the next 

Move to the IAM Console and review the STATE MACHINE role
note how it gives 

- logging permissions
- the ability to invoke the email lambda function when it needs to send emails
- the ability to use SNS to send text messages

# STAGE 3B - Create State Machine

Move to the AWS Step Functions
Click the `Hamburger Menu` at the top left and click `State Machines`  
Click `Create State Machine`  
Select `Write your workflow in code` which will allow you to use Amazon States Language  
Scroll down
for `type` select `standard`  
Open this in a new tab https://learn-cantrill-labs.s3.amazonaws.com/aws-serverless-pet-cuddle-o-tron/pet-cuddle-o-tron.json  
this is the Amazon States Language (ASL) file for the `pet-cuddle-o-tron` state machine  
Copy the contents into your clipboard   
Move back to the step functions console   
Select all of the code snippet and delete it  
Paste in your clipboard  

Click the `Refresh` icon on the right side area ... next to the visual map of the state machine.  
Look through the visual overview and the ASL .. and make sure you understand the flow through the state machine.  

The state machine starts ... and then waits for a certain time period based on the `Timer` state. This is controlled by the web front end you will deploy soon. Then the `email` is used Which sends an email reminder

The state machine will control the flow through the serverless application.. once stated it will coordinate other AWS services as required.  

# STAGE 3C - Configure State Machine

In the state machine ASL (the code on the left) locate the `EmailOnly` definition.  
Look for `EMAIL_LAMBDA_ARN` which is a placeholder, replace this with the email_reminder_lambda ARN you noted down previously. This is the ARN of the lambda function you created.

Scroll down to the bottom and click `next` 
For `State machine name` use `MeetingOTron`  
Scroll down and under `Permissions` select `Choose an existing role` and select `StateMachineRole` from the dropdown (it should be the only one, if you have multiple select the correct one and there will be random which is fine as this was created by CloudFormation)
Scroll down, under `Logging`, change the `Log Level` to `All`  
Scroll down to the bottom and click `Create state machine`  

Locate the `ARN` for the state machine on the top left... note this down somewhere safe as `State Machine ARN`  


# STAGE 3 - Done

At this point we have configured the state machine which is the core part of the serverless application.  
The state machine controls the flow through the application and is responsible for interacting with other AWS products and services.  

