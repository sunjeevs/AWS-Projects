# Serverless Reminder Application

In this stage of the application, an S3 bucket and static website hosting will be created to host the application front end. The source files for the front end will be downloaded, configured to connect to the specific API Gateway, and then uploaded to S3. Finally, some application tests will be run to verify its functionality.

# STAGE 5A - Create the S3 Bucket

Move to the S3 Console 
Click `Create bucket`  
Choose a unique bucket name
Scroll Down and **UNTICK** `Block all public access`  
Tick the box under `Turning off block all public access might result in this bucket and the objects within becoming public` to acknowledge you understand that you can make the bucket public.  
Scroll Down to the bottom and click `Create bucket`  


# STAGE 5B - Set the Bucket as Public

Go into the bucket you just created.  
Click the `Permissions` tab.  
Scroll down and in the `Bucket Policy` area, click `Edit`. 


in the box, paste the code below

```
{
    "Version":"2012-10-17",
    "Statement":[
      {
        "Sid":"PublicRead",
        "Effect":"Allow",
        "Principal": "*",
        "Action":["s3:GetObject"],
        "Resource":["REPLACEME_MEETING_O_TRON_BUCKET_ARN/*"]
      }
    ]
  }

```
Replace the `REPLACEME_MEETING_O_TRON_BUCKET_ARN` (being careful NOT to include the `/*`) with the bucket ARN, which you can see near to `Bucket ARN `
Click `Save Changes`  


# STAGE 5C - Enable Static Hosting

Next we need to enable static hosting on the S3 bucket so that it can be used as a front end website.  
Click on the `Properties Tab`  
Scroll down and locate `Static website hosting`  
Click `Edit`  
Select `Enable` 
Select `Host a static website`  
For both `Index Document` and `Error Document` enter `index.html` 
Click `Save Changes`  
Scroll down and locate `Static website hosting` again.  
Under `Bucket Website Endpoint` copy and note down the bucket endpoint URL.  
  

# STAGE 5D - Upload and Test

Return to the S3 console
Click on the `Objects` Tab.  
Click `Upload`  
Drag the 4 files from the Frontend folder onto this tab, including the serverless.js file.

Click `Upload` and wait for it to complete.  
Click `Exit`  
Verify All 4 files are in the `Objects` area of the bucket.  


Open the `MeetingOTron URL` you just noted down in a new tab.  
What is seen is a simple HTML web page created by the HTML file itself and the `main.css` stylesheet.
When we click buttons .. that calls the `.js` file which is the starting point for the serverless application

Ok to test the application, fill in what's required.
then enter the `MeetingOTron Customer Address` in the email box, this is the email which you verified right at the start as the customer for this application.  

open a new tab to the `Step functions console` 
Click on `MeetingOTron`  
Click on the `Logging` tab, you will see no logs
CLick on the `Executions` tab, you will see no executions..

Move back to the web application tab (s3 bucket)  
then click on the Button to send an email.  

Got back to the Step functions console
make sure the `Executions` Tab is selected
click the `Refresh` Icon
Click the `execution`  
Watch the graphic .. see how the `Timer state` is highlighted
The step function is now executing and it has its own state ... its a serverless flow.
Keep waiting, and after 120 seconds the visual will update showing the flow through the state machine

- Timer .. waits 120 seconds
- `Email` invokes the lambda function to send an email
- `NextState` in then moved through, then finally `END`

Scroll to the top, click `ExeuctionInput` and you can see the information entered on the webpage.
This was send it, via the `JS` running in browser, to the API gateway, to the `api_lambda` then through to the `statemachine`

Click `MeetingOTron` at the top of the page  
Click on the `Logging` Tab  
Because the roles we created had `CWLogs` permissions the state machine is able to log to CWLogs
Review the logs and ensure you are happy with the flow.  

# STAGE 5 - Done

At this point thats everything .. you now have a fully functional serverless application

- Loads HTML & JS From S3 & Static hosting
- Communicates via `JS` to API Gateway 
- Uses `api_lambda` as backing resource
- Runs a statemachine passing in parameters
- State machine sends email
- State machine terminates

  
