---
title: "Deploy a Severless Website"
date: 2020-09-12
tags: [writing, aws]
header:
  image: "/images/banner-binary-3441007_1920.jpg"
excerpt: "Serverless, Lambda, API Gateway, S3, Route53"
mathjax: "true"
---
# Deploy a Serverless Site with Static and Dynamic Content Using Lambda, API Gateway, S3 and Route53
_____
In this tutorial, you will learn how to deploy a serverless website utilizing S3 for static website hosting and Lambda and API Gateway to deliver dynamic content. Route53 may also be used to register and connect a domain name.

In order to follow along you will need:
	- an AWS account
	- basic understanding HTML
	- text editor 

### Step 1: Login to the AWS Management Console.

### Step 2: Navigate to S3.

### Step 3: Create a new bucket in S3.
- Click **Create a Bucket**
- Name your bucket. 
-- If you intend to use your own domain name, the bucket name must match the second-level domain name exactly. (That is, the part of the domain before .com, .org, .edu, etc) 
-- Additionally, remember that bucket names must be globally unique. (Meaning, across all aws accounts, not just your account.)

### Step 3b:Make the bucket public.  
Make Bucket Public: If you are using an existing bucket, you can make it public.

#*ADD DETAILS*

### Step 4:  Enable Static Web Hosting
- Click on the bucket name.
- Select **Properties** in in the top menu bar.
- Select configure static website hosting. Type in index.html and error.html where prompted and then click ***save***.
-- index.html
-- error.html

-- save



### Step 5: Domain Registry (Optional)
- Navigate to Route53
- If you haven't already, register your domain name and remember if must match the bucket name.  This process can take up to 72 hours to complete, but it often finished before then. As an alernative to registering and connecting a domain name, the S3 bucket will have it's own URL.


### Step 6:  Open Lambda Console (Under Compute) *Note which region you are in.*

### Step 7: Create a Function
- Select Create a Function.

a. Select Author from scratch

b. Name you function 

c. For runtime select Python3.8

d. Select role

If this is your first time using Lambda you will need to create a new role.

i. Create New Role from Template

ii. give it a name, ie myLambdaRole

iii. Search for the 'Simple Microservice permissions' policy template

e. Click Create Function


### Step 8:  Change the function's code.

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



### Step 9: Add triggers

a. Scroll back up to the Designer 

b. click Add triggers

c. add API Gateway 

You will getting a warning that says "Configuration required" - proceed to the next step



### Step 10:  Configure triggers

The window to configure triggers will appear below Designer.

a. Under API dropdown, select Create a new API

b. API name

c. Deployment stage, select production

d. Security, endpoint > open which leaves it open & public Add more sec info

e. click add

  SAVE FUNCTION

### Step 11: Copy the invocation url 
-Click the expand arrow on Details in the API Gateway box below the design, copy the invocation url (which won't work until we configure it.

### Step 12: Click on the title which will open API Gateway

### Step 13: Delete default method

### Step 14: Create New Method

a. From Actions drop down menu select create new method

b. GET from new method drop down

c. click little 'tick' next to GET

d. Integration type: Lambda Function

e. check 'Use Lambda Proxy integration'

f. select lambda region

g.type function name and it should autopopulate

h. leave default timeout selected

i. save (you will see confirmation window with arn of the lambda) confirm 


### Step 15: Deploy API

a. Actions > Deploy API

b. deployment stage: prod

c. Description : serverless website etc

d. click deploy - and you will be takes to the Stages page with API Gateway


### Step 16: Stages

a. clicking deploy in the previous step will automatically bring you to this page.  It is also accessible on the left hand menu within API Gateway.

b. select prod

c. invoke url - copy this for the next step



### HTML FILES

### Step X: Add the invoke url to your html file.

 change the    `xhttp.open(<invoke-url>, true):`

### Step X:  Upload html/code to S3.

a. Navigate to S3.

b. If you're bucket is not already public, make it so.

c. Upload html files

d. select files

e. Select 'make public' under the 'More' dropdown menu

f. confirm by clicking 'make public'



### Route53 OPTIONAL

### Step X: Navigate to Route53, under Networking

### Step X: Hosted Zones

a. click hosted zones

b.  select domain

### Step X: Create Record Set

a. click it

b. Select Alias - You s3 website should autopopulate

If it doesn't  - then they don't match.

c. click create - creates A record



### Step X: Visit your site.

Go to domain or s3 URL to test! Click button sends request to to API Gateway.

Remember to give the DNS cache time to clear before testing it.