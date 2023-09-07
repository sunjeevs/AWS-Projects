# Serverless Reminder Application

In this stage, the front end API for the serverless application will be created. The front end loads from S3, runs in your browser, and communicates with this API. API Gateway will be used for the API Endpoint, and Lambda will be used to provide the backing compute. First, the supporting API_LAMBDA will be created, and then the API Gateway will be set up.

# STAGE 4A - Create the API Lambda Function which supports API Gateway

Move to the Lambda console
Click on `Create Function`  
for `Function Name` use `api_lambda`  
for `Runtime` use `Python 3.9`  
Expand `Change default execution role`  
Select `Use an existing role`  
Choose the `LambdaRole` from the dropdown  
Click `Create Function`  


This is the lambda function which will support the API Gateway

# STAGE 4B - Configure the Lambda Function

Scroll down, and remove all the code from the `lambda_function` text box  
Open the link in a new tab to the python code given in Codes folder. 
Move back to the Lambda console.  
Select the existing lambda code and delete it.  
Paste the code into the lambda fuction.  

This is the function which will provide compute to API Gateway.  
It's job is to be called by API Gateway when its used by the serverless front end part of the application (loaded by S3)
It accepts some information from us, via API Gateway and then it starts a state machine execution - which is the logic of the application.  

Locate the `YOUR_STATEMACHINE_ARN` placeholder and replace this with the State Machine ARN noted down in the previous step.  
Click `Deploy` to save the lambda function and configuration.     


# STAGE 4C - Create API

Now we have the api_lambda function created, the next step is to create the API Gateway, API and Method which the front end part of the serverless application will communicate with.  
Move to the API Gateway console 
Click `APIs` on the menu on the left  
Locate the `REST API` box, and click `Build`
If you see a popup dialog `Create your first API` dismiss it by clicking `OK`  
Under `Create new API` ensure `New API` is selected.  

For `API name*` enter `petcuddleotron`  
for `Endpoint Type` pick `Regional` 
Click `create API`  

# STAGE 4D - Create Resource

Click the `Actions` dropdown and Click `Create Resource`  
Under resource name enter `meetingotron`  
Towards the bottom **MAKE SURE TO TICK** `Enable API Gateway CORS`.  
This relaxes the restrictions on things calling on our API with a different DNS name, it allows the code loaded from the S3 bucket to call the API gateway endpoint.  
**if this box isn't checked, the API will fail**   
Click `Create Resource`  

# STAGE 4E - Create Method

Ensure you have the `/meetingotron` resource selected, click `Actions` dropdown and click `create method`  
In the small dropdown box which appears below `/meetingotron` select `POST` and click the `tick` symbol next to it.  
this method is what the front end part of the application will make calls to.  
Its what the api_lambda will provide services for.  

Ensure for `Integration Type` that `Lambda Function` is selected.  
Make sure `us-east-1` is selected for `Lambda Region`  
In the `Lambda Function` box.. start typing `api_lambda` and it should autocomplete, click this auto complete (**Make sure you pick api_lambda and not email reminder lambda**)  

Make sure that `Use Default Timeout` box **IS** ticked.  
Make sure that `Use Lambda Proxy integration` box **IS** ticked, this makes sure that all of the information provided to this API is sent on to lambda for processing in the `event` data structure.  
**if this box isn't checked, the API will fail**  
Click `Save`  

# STAGE 4F - Deploy API

Now the API, Resource and Method are configured - we now need to deploy the API out to API gateway, specifically an API Gateway STAGE.  
Click `Actions` Dropdown and `Deploy API`  
For `Deployment Stage` select `New Stage`  
for stage name and stage description enter `prod`  
Click `Deploy`  

At the top of the screen will be an `Invoke URL` .. note this down.  
This URL will be used by the client side component of the serverless application and this will be unique to everyone.    


# STAGE 4 - Done

At this point we have configured the last part of the AWS side of the serveless application.   

We now have :-

- SES Configured
- An Email Lambda function to send email using SES
- A State Machine configured which can send EMAIL after a certain time period when invoked.
- An API, Resource & Method, which use a lambda function for backing deployed out to the PROD stage of API Gateway
 

