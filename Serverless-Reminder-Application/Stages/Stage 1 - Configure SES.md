# Serverless Reminder Application

# STAGE 1A - VERIFY SES APPLICATION SENDING EMAIL ADDRESS

This application is going to send reminder messages via SMS and Email.  It will use the simple email service or SES. In production, it could be configured to allow sending from the application email, to any users of the application. SES starts off in sandbox mode, which means we can only sent to verified addresses (to avoid spamming). 

Move to the `SES` console
Click on `Verified Identities` under Configuration 
Click `Create Identity`  
Check the 'Email Address' checkbox  
Ideally we'll need a `sending` email address for the application and a `receiving email address` for your test customer. But we can use the same email for both.  

For the application email ... the email the app will send from i'm going to use `sunjeevsomu02+sending@gmail.com`  
Enter whatever email you want to use to send in the box (it needs to be a valid address as it will be checked)  
Click `Create Identity`  
An email containing a link to click will be received at this address. 
Click that link   
You should see a `Congratulations!` message  
Return to the SES console and `Refresh` the browser, the verification status should now be `verified`  
Record this address somewhere save as the `Application Sending Address`  

# STAGE 1B - VERIFY SES APPLICATION CUSTOMER EMAIL ADDRESS

If you want to use a different email address for the test customer (recommended), follow the steps below  
Click `Create Identity`  
Check the 'Email Address' checkbox 
For application email ... the email for my test customer is  `sunjeevsomu02+receiving@gmail.com`  
Enter whatever email you want to use to send in the box (it needs to be a valid address as it will be checked)  
Click `Create Identity`   
An email containing a link to click will be received at this address.  
Click that link   
You should see a `Congratulations!` message  
Return to the SES console and refresh your browser, the verification status should now be `verified`  
Record this address somewhere save as the `Application Customer Address`   

# STAGE 1 - DONE   

At this point we have whitelisted 2 email addresses for use with SES.  

- the `Application Sending Address`. 
- the `Application Customer Address`. 

These will be configured and used by the application in later stages. 
