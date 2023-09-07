# Serverless Reminder Application

# STAGE 2A - Create the Lambda Execution Role for Lambda

In this stage of the demo, an IAM role needs to be created, which will be used by the email_reminder_lambda to interact with other AWS services. It could be created manually, but it's easier to complete this step using CloudFormation to expedite the process.
 
Use the CloudFormation Template given.

Wait for the Stack to move into the `CREATE_COMPLETE` state before moving into the next  

Move to the IAM Console and review the execution role  
Notice that it provides SES, SNS and Logging permissions to whatever assumes this role.    
This is what gives lambda the permissions to interact with those services    


# STAGE 2B - Create the email_reminder_lambda function

Next, the lambda function will be created, which will be used by the serverless application to create an email and then send it using `SES`.
Move to the lambda console 
Click on `Create Function`  
Select `Author from scratch`  
For `Function name` enter `email_reminder_lambda`  
and for runtime click the dropdown and pick `Python 3.9`  
Expand `Change default execution role`  
Pick to `Use an existing Role`  
Click the `Existing Role` dropdown and pick `LambdaRole` (there will be randomness and thats ok)  
Click `Create Function`  

# STAGE 2C - Configure the email_reminder_lambda function

Scroll down, to `Function code`  
in the `lambda_function` code box, select all the code and delete it  

Paste in this code

```
import boto3, os, json

FROM_EMAIL_ADDRESS = 'sunjeevsomu02+sending@gmail.com'

ses = boto3.client('ses')

def lambda_handler(event, context):
    # Print event data to logs .. 
    print("Received event: " + json.dumps(event))
    # Publish message directly to email, provided by EmailOnly or EmailPar TASK
    ses.send_email( Source=FROM_EMAIL_ADDRESS,
        Destination={ 'ToAddresses': [ event['Input']['email'] ] }, 
        Message={ 'Subject': {'Data': 'Schedule your meetings!'},
            'Body': {'Text': {'Data': event['Input']['message']}}
        }
    )
    return 'Success!'

```

This function will send an email to an address it's supplied with (by step functions) and it will be FROM the email address we specify.    
Select `REPLACE_ME` and replace with the `Application Sending Address` which you noted down in `STAGE1`    
Click `Deploy` to configure the lambda function    
Scroll all the way to the top, and click the `copy` icon next to the lambda function ARN.  
Note this ARN down somewhere same as the `email_reminder_lambda` ARN    

# STAGE 2 - DONE   

At this point, the lambda function has been configured, which will eventually be used to send emails on behalf of the serverless application.
