# Schoology-API

A tutorial on how to use the schoology REST API. Created as I could find no step by step process and the documentation was lacking. 

# Conditions

I got this working on a student account, and am unsure if it will work on a teacher/admin account however I imagine it would. Ensure you have software like <a href="postman.com">postman</a> to send test API Requests and a decent understanding of REST API's, and in particular Oauth. 

# Login

Log into your schoology account and go to your user API Credentials. These can be found at [your district schoology address]/api. For example, https://schoology.dpsk12.org/api
This will bring up a screen that lists your consumer key, and your consumer secret. These will be used later for authorization.

# Oauth Authorization

To get an OAuth token and secret, first open postman and input this URL: https://api.schoology.com/v1/oauth/request_token?oauth_consumer_key=&oauth_timestamp=&oauth_signature_method=PLAINTEXT&oauth_version=1.0&oauth_nonce=&oauth_signature=

For oauth_consumer_key, enter the consumer key from your schoology API Page <br/>
For oauth_timestamp, enter the current Unix time code, you will need to do this each time you send a request. You can find the current time code <a href="https://www.epochconverter.com/">here</a>.<br/>
For oauth_signature_method, we can use plaintext since API calls are made with HTTPS instead of HTTP<br/>
For oauth_version, we are using OAuth 1.0, so it is set to 1.0<br/>
For oauth_nonce, enter any random short string. <br/>
For oauth_signature, enter your consumer secret (found on the same page as your consumer key) %26, for example, "123456789012345678901234567890%26"<br/>

Send the request as a GET, and record the response. 

A successful response should give status 200, and 3 things. A oauth_token, oauth_token_secret, and an xoauth_token_ttl. 

# Application Authorization

Now that you have made Oauth keys, you must authorize your application on an account. To do this, input this URL into postman and set the following parameters. https://[your district schoology address]/oauth/authorize?oauth_consumer_key=&oauth_token=&oauth_token_secret=

For oauth_consumer_key, enter your OAuth consumer key from your schoology API Page <br/>
For oauth_token, enter your OAuth token from your Oauth Authorization response.<br/>
For oauth_token_secret, enter your OAuth token secret from your Oauth Authorization Response<br/>

Instead of running this link in postman, copy and paste it into your web browser and approve your application. If done successfully, the user will be prompted to Approve or Deny the application's request for access. Select Approve and navigate back to postman.

# Sending an API Request

We can now send an API request using postman, or any http client. For this example, we will get information about an assignment, such as its name, due date, and many more properties. 

Re-enter the paramaters from Oauth Authorization, but use this link: https://api.schoology.com/v1/sections/[class ID/assignments?oauth_consumer_key=&oauth_timestamp=&oauth_signature_method=PLAINTEXT&oauth_version=1.0&oauth_nonce=&oauth_signature=

Now you can change [class ID] to the id of the class you want to get assignment data from. To find this ID, navigate to the class on schoology, and grab the 10 digit number from the URL and enter it as the [class ID]. When run successfully as a GET request, this link will return all data about every assignment in a class. To see more examples, visit the <a href="https://developers.schoology.com/api-documentation/example-requestsresponses">API Examples</a>. 

# Ending

So that's it! This is how you can make basic requests to the schoology API. As previously mentioned, this is intended for a student account, however, I would imagine it would work on a Teacher/Admin Account. The API Also supports Posting data with the POST function, to in theory teachers could post a new assignment or other content automatically with a POST command. 

Keep in mind, OAuth tokens and secrets expire after 1 hour and will need to be regenerated. 

I hope this helps you get started with the Schoology API, I am by no means an expert, just someone who got it to work.
