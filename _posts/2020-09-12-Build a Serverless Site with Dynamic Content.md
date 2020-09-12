# Build a Serverless Site with Dynamic Content using Lambda, API Gateway, S3 and Route53

In this tutorial, you will learn how to deploy a serverless website utilizing Lambda, API Gateway, S3 and Route53. The use of Route53 is optional if you do not wish you use your own domain name. 

In order to follow along you will need:
	- an AWS account
	- basic understanding HTML
	- text editor 

### Step 1: Login to the AWS Management Console.

### Step 2: Navigate to S3.

### Step 3: Create a new bucket in S3.
- Click **Create a Bucket**
- Name your bucket. *Note: If you intend to use your own domain name, the bucket name must match the domain name exactly.*       

### Step 3b:Make the bucket public.  
Make Bucket Public: If you are using an existing bucket, you can make it public.

#*ADD DETAILS*

### Step 4:  Enable Static Web Hosting
- Click on the bucket name.
- Select **Properties** in in the top menu bar.
> properties 

> configure static website hosting

index.html

error.html

> save



### Route53 OPTIONAL STEP

### Step X: Navigate to Route 53

Step X:  OPTIONAL Register a Domain Name (Can take up to 72 hours)

ALT you can use s3 bucket url

check availability remember top level domain (part before .com/.org) must match bucket name

register



Lambda

Step X:  Open Lambda Console (Under Compute) Note the region you are in.



Step X: Select Create a Function.

a. Select Author from scratch

b. Name you function 

c. For runtime select Python3.8

d. Select role

If this is your first time using Lambda you will need to create a new role.

i. Create New Role from Template

ii. give it a name, ie myLambdaRole

iii. Search for the 'Simple Microservice permissions' policy template

e. Click Create Function



Step X:  Change the function's code.

Once your function has been created you'll see the Designer at the top of the page. Scroll down to IDE, Function code.

a. Delete boiler plate and replace with the below. 

```

def lambda_handler(event, context):

    print("In lambda handler")

    resp = {

        "statusCode": 200,

        "headers": {

            "Access-Control-Allow-Origin": "*",

        },

        "body": "Serverless Website" 

    }

    return resp

```

Don't forget to click save in the top right corner.





Step X: Add triggers

a. Scroll back up to the Designer 

b. click Add triggers

c. add API Gateway 

You will getting a warning that says "Configuration required" - proceed to the next step



Step X:  Configure triggers

The window to configure triggers will appear below Designer.

a. Under API dropdown, select Create a new API

b. API name

c. Deployment stage, select production

d. Security, endpoint > open which leaves it open & public Add more sec info

e. click add



Step X:  SAVE FUNCTION

Step X:  Click the expand arrow on Details in the API Gateway box below the design, copy the invocation url (which won't work until we configure it.



API GATEWAY

Step X: Click on the title which will open API Gateway

Step X: Delete default method

Step X: Create New Method

a. From Actions drop down menu select create new method

b. GET from new method drop down

c. click little 'tick' next to GET

d. Integration type: Lambda Function

e. check 'Use Lambda Proxy integration'

f. select lambda region

g.type function name and it should autopopulate

h. leave default timeout selected

i. save (you will see confirmation window with arn of the lambda) confirm 



Step X: Deploy API

a. Actions > Deploy API

b. deployment stage: prod

c. Description : serverless website etc

d. click deploy - and you will be takes to the Stages page with API Gateway





Step X: Stages

a. clicking deploy in the previous step will automatically bring you to this page.  It is also accessible on the left hand menu within API Gateway.

b. select prod

c. invoke url - copy this for the next step



HTML

Step X: Add the invoke url to your html file.

 change the    `xhttp.open(<invoke-url>, true):`

Step X:  Upload html/code to S3.

a. Navigate to S3.

b. If you're bucket is not already public, make it so.

c. Upload html files

d. select files

e. Select 'make public' under the 'More' dropdown menu

f. confirm by clicking 'make public'



Route53 OPTIONAL

Step X: Navigate to Route53, under Networking

Step X: Hosted Zones

a. click hosted zones

b.  select domain

Step X: Create Record Set

a. click it

b. Select Alias - You s3 website should autopopulate

If it doesn't  - then they don't match.

c. click create - creates A record



Step X: Visit your site.

Go to domain or s3 URL to test! Click button sends request to to API Gateway.

remember give the dns cache time to clear before testing it 
