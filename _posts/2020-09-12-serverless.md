---
title: "Deploy a Severless Website"
date: 2020-09-12
tags: [writing, aws]
header:
  image: "/images/banner-binary-3441007_1920.jpg"
excerpt: "Serverless, Lambda, API Gateway, S3, Route53"
mathjax: "true"
---
## Deploy a Serverless Website with Lambda, API Gateway, S3 and Route53
_____

In this tutorial, you will learn how to deploy a serverless website utilizing S3 for static website hosting and Lambda and API Gateway to deliver dynamic content. Route53 may also be used to register and connect a domain name.

In order to follow along you will need:
	- an AWS account
	- basic understanding HTML
	- text editor 


## Step 1: Login to the AWS Management Console.

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step1-console.png" alt="AWS Screenshot" width="640">



## Step 2: Navigate to S3.

- Navigate to S3 by typing it into the search bar or looking under Storage Services.


## Step 3: Create a new bucket in S3.

- Click **Create a Bucket**

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step3-createbucket-1.png" alt="AWS Screenshot" width="640">

- Name your bucket. 
    If you intend to use your own domain name, the bucket name must match the second-level domain name exactly. That is, the part of the domain before .com, .org, .edu, etc. 
    Additionally, remember that bucket names must be globally unique. Globally meaning, unique across all aws accounts, not just your account.
    Be sure to note the ***Region*** for this bucket.  S3, Lambda, and API Gateway are all regional services.

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step3-createbucket-2.png" alt="AWS Screenshot" width="640">

- Uncheck block all public access.

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step3-createbucket-3.png" alt="AWS Screenshot" width="640">

- Click ***Create bucket***


## Step 3b (Optional): Make your S3 bucket public.  

If you are using an existing bucket, you must make it public in order to enable static website hosting.

- Click on the bucket's name within the S3 console.

- Click the ***Permissions*** tab. This will automatically open on ***Block public access.***

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step3b-public-1.png" alt="AWS Screenshot" width="640">

- Click on ***Edit*** 

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step3b-public-2.png" alt="AWS Screenshot" width="640">

- Uncheck ***Block all public access.***

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step3b-public-3.png" alt="AWS Screenshot" width="640">

- Click ***Save*** Then type ***confirm*** into the pop window, and then click ***Confirm.***

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step3b-public-4.png" alt="AWS Screenshot" width="640">


## Step 4: Enable Static Web Hosting

- Click on the bucket name.

- Select **Properties** in in the top menu bar.

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step4-statichosting-1.png" alt="AWS Screenshot" width="640">

- Select ***Static website hosting.***

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step4-statichosting-2.png" alt="AWS Screenshot" width="640">

- Type in index.html and error.html where prompted and click ***Save***.

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step4-statichosting-3.png" alt="AWS Screenshot" width="640">


### Step 5: Domain Registry (Optional)
- Navigate to Route53
- If you haven't already, register your domain name and remember if must match the bucket name. This process can take up to 72 hours to complete, but it often finished before then. As an alernative to registering and connecting a domain name, the S3 bucket will have it's own URL.


### Step 6: Open Lambda Console 

- Navigate to Lambda by typing it into the search bar or looking under Compute Services.

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step6-lambda-1.png" alt="AWS Screenshot" width="640">


### Step 7: Create a Function

- Click ***Create a Function.***

- Select ***Author from scratch***

- Name you function 

- For runtime select ***Python3.6***

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step7-lambda-1.png" alt="AWS Screenshot" width="640">

- Expand ***Choose or create an execution role*** If this is your first time using Lambda you will need to create a new role. 

- Select ***Create a new role from AWS policy templates***

- Name it.

- Search for the 'Simple microservice permissions' policy template

- Click ***Create Function***

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step7-lambda-2.png" alt="AWS Screenshot" width="640">


### Step 8:  Update your Lambda Function.

- Once your function has been created you'll see the ***Designer*** at the top of the page. Scroll down to IDE, ***Function code***.



- Delete boiler plate and replace with the below. 

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

- Click ***Save*** within ***Function code.*** This should cause the other ***Save*** function to turn gray.

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step8-lambda-1.png" alt="AWS Screenshot" width="640">


## Step 9: Add triggers

- Scroll back up to the ***Designer*** and click on ***Add triggers***

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step9-triggers-1.png" alt="AWS Screenshot" width="640">

- Add ***API Gateway*** as a trigger.  

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step9-triggers-2.png" alt="AWS Screenshot" width="640">

Please note, ***Security*** is left open in this demonstration, however that is not reccommend for a live site.  Please check see the [AWS best practices](https://aws.amazon.com/architecture/security-identity-compliance/?cards-all.sort-by=item.additionalFields.sortDate&cards-all.sort-order=desc) for more detail. 

<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-12-serverless/step9-triggers-3.png" alt="AWS Screenshot" width="640">


## Step 10: Copy the invocation url 
-Click the expand arrow on Details in the API Gateway box below the design, copy the invocation url (which won't work until we configure it.

### Step 11: Click on the title which will open API Gateway

### Step 12: Delete default method

### Step 13: Create New Method

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
