# Tutorial: Deploying a Hello World Application<a name="serverless-getting-started-hello-world"></a>

In this guide, you download, build, and deploy a sample Hello World application using AWS SAM\. You then test the application in the AWS Cloud, and optionally test it locally on your development host\.

This application implements a simple API backend\. It consists of an API Gateway endpoint and a Lambda function\. When you send a GET request to the API Gateway endpoint, the Lambda function is invoked\. This function returns a `hello world` message\.

The following diagram shows the components of this application:

![\[A diagram that shows a Lambda function that's invoked when you send a GET request to the API Gateway endpoint\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/images/sam-getting-started-hello-world.png)

The following is a preview of commands that you run to create your Hello World application\. For more details about each of these commands, see the sections later in this page

```
#Make sure that the Region for this bucket aligns with where you deploy
aws s3 mb s3://bucketname --region region  # Example regions: us-east-1, ap-east-1, eu-central-1, sa-east-1

#Step 1 - Download a sample application
sam init --runtime python3.7

#Step 2 - Build your application
cd sam-app
sam build

#Step 3 - Package your application
sam package --output-template packaged.yaml --s3-bucket bucketname

#Step 4 - Deploy your application
sam deploy --template-file packaged.yaml --region us-west-2 --capabilities CAPABILITY_IAM --stack-name aws-sam-getting-started
```

## Prerequisites<a name="serverless-getting-started-hello-world-prerequisites"></a>

This guide assumes that you've completed the steps in the [Installing the AWS SAM CLI](serverless-sam-cli-install.md) for your OS\. It assumes that you've done the following:

1. Created an AWS account\.

1. Configured IAM permissions\.

1. Installed the AWS CLI\.

1. Created an Amazon S3 bucket\.

1. Installed Docker\. Note: Docker is only a prerequisite for testing your application locally\.

1. Installed Homebrew\. Note: Homebrew is only a prerequisite for Linux and macOS\.

1. Installed the AWS SAM CLI\.

In addition, the sample application in this tutorial requires Python 3\.7\. If you need to download Python 3\.7, see [Download Python](https://www.python.org/downloads/)\.

## Step 1: Download a Sample AWS SAM Application<a name="serverless-getting-started-hello-world-initialize"></a>

**Command to run:**

```
sam init --runtime python3.7
```

**Example output:**

```
   
 [+] Initializing project structure...

 Project generated: ./sam-app

 Steps you can take next within the project folder
 ===================================================
 [*] Invoke Function: sam local invoke HelloWorldFunction --event event.json
 [*] Start API Gateway locally: sam local start-api

 Read sam-app/README.md for further instructions

[*] Project initialization is now complete
```

**What AWS SAM is doing:**

This command creates a directory named `sam-app` with the following folder structure, and then makes it your current directory:

```
 
 sam-app/
   ├── README.md
   ├── events/
   │   └── event.json
   ├── hello_world/
   │   ├── __init__.py
   │   ├── app.py            #Contains your AWS Lambda handler logic.
   │   └── requirements.txt  #Contains any Python dependencies the application requires, used for sam build
   ├── template.yaml         #Contains the AWS SAM template defining your application's AWS resources.
   └── tests/
       └── unit/
           ├── __init__.py
           └── test_handler.py
```

There are three especially important files:
+ `template.yaml`: Contains the AWS SAM template that defines your application's AWS resources\.
+ `hello_world/app.py`: Contains your actual Lambda handler logic\.
+ `hello_world/requirements.txt`: Contains any Python dependencies that the application requires, and is used for `sam build`\.

## Step 2: Build Your Application<a name="serverless-getting-started-hello-world-build"></a>

**Command to run:**

From the `sam-app` directory \(that is, the directory where the `template.yaml` file for the sample application is located\), run this command:

```
sam build
```

**Example output:**

```
  
 Build Succeeded

 Built Artifacts  : .aws-sam/build
 Built Template   : .aws-sam/build/template.yaml

 Commands you can use next
 =========================
 [*] Invoke Function: sam local invoke
 [*] Package: sam package --s3-bucket <yourbucket>
```

**What AWS SAM is doing:**

The AWS SAM CLI comes with abstractions for a number of Lambda runtimes to build your dependencies, and copies the source code into staging folders so that everything is ready to be packaged and deployed\. The `sam build` command builds any dependencies that your application has, and copies your application source code to folders under `aws-sam/build` to be zipped and uploaded to Lambda\.

You can see the following top\-level tree under `.aws-sam`:

```
 
 .aws_sam/
   └── build/
       ├── HelloWorldFunction/
       └── template.yaml
```

`HelloWorldFunction` is a directory that contains your `app.py` file, as well as third\-party dependencies that your application uses\.

## Step 3: Package Your Application for Deployment<a name="serverless-getting-started-hello-world-package"></a>

**Command to run:**

```
sam package --output-template packaged.yaml --s3-bucket bucketname
```

**Example output:**

```
 
 Uploading to 8eaa458acdd2b83bd86a45d4d256ef73  558700 / 558700.0  (100.00%)
 Successfully packaged artifacts and wrote output template to file packaged.yaml.
 Execute the following command to deploy the packaged template:

 aws cloudformation deploy --template-file packaged.yaml --stack-name <YOUR STACK NAME>
```

**Note**  
For *bucketname* in this command, you need an Amazon S3 bucket that the `sam package` command can use to store the deployment package\. The deployment package is used when you deploy your application in a later step\. If you need to create a bucket for this purpose, run the following command to create an Amazon S3 bucket:  

```
aws s3 mb s3://bucketname --region region  # Example regions: us-east-1, ap-east-1, eu-central-1, sa-east-1
```

**What AWS SAM is doing:**

This command takes your Lambda handler source code and any third\-party dependencies, zips everything, and uploads the zip file to your Amazon S3 bucket\. That bucket and file location are then noted in the `packaged.yaml` file\. You use the `packaged.yaml` file to deploy the application in the next step\.

## Step 4: Deploy Your Application to the AWS Cloud<a name="serverless-getting-started-hello-world-deploy"></a>

**Command to run:**

```
sam deploy --template-file packaged.yaml --region region --capabilities CAPABILITY_IAM --stack-name aws-sam-getting-started
```

**Example output:**

```
 
 Waiting for changeset to be created..
 Waiting for stack create/update to complete
 Successfully created/updated stack - aws-sam-getting-started
```

**What AWS SAM is doing:**

This command deploys your application to the AWS Cloud\. It's important that this command explicitly includes both of the following:
+ The AWS Region to deploy to\. This Region must match the Region of the Amazon S3 source bucket\.
+ The `CAPABILITY_IAM` parameter, because creating new Lambda functions involves creating new IAM roles\.

 For more information about capabilities, see [CreateStack](https://docs.aws.amazon.com/goto/WebAPI/cloudformation-2010-05-15/CreateStack) in the *AWS CloudFormation API Reference*\.

## Step 5: Test Your Application in the AWS Cloud<a name="serverless-getting-started-hello-world-test-in-cloud"></a>

**Command to run:**

```
aws cloudformation describe-stacks --stack-name aws-sam-getting-started --region region --query "Stacks[].Outputs"
```

After running this command, you see details of the stack that you just created, including an `OutputKey` of `HelloWorldApi`, which looks something like the following:

```
 
 {
     "OutputKey": "HelloWorldApi",
     "OutputValue": "https://<restapiid>.execute-api.us-east-1.amazonaws.com/Prod/hello/",
     "Description": "API Gateway endpoint URL for Prod stage for Hello World function"
 }
```

The `OutputValue` of this object is the endpoint URL of your stack\. You can use `curl` to send a request to your application using that endpoint URL\. For example:

```
curl https://<restapiid>.execute-api.us-east-1.amazonaws.com/Prod/hello/
```

You should see output like the following after successfully deploying your application:

```
 
 {"message": "hello world"}
```

**What AWS SAM is doing:**

For this step, AWS SAM isn't actually doing anything\. Instead, you're using an AWS CloudFormation command to retrieve information about your serverless application \(that is, the *AWS CloudFormation stack*\), and then using `curl` to send a request to your application's endpoint URL\.

If you see `{"message": "hello world"}` after executing the `curl` command, it means that you've successfully deployed your serverless application to AWS, and are calling your live Lambda function\. Otherwise, see the [Troubleshooting](#serverless-getting-started-hello-world-troubleshooting) section later in this tutorial\.

## Step 6: Testing Your Application Locally \(Optional\)<a name="serverless-getting-started-hello-world-test-locally"></a>

When you're developing your application, you might also find it useful to test locally\. The AWS SAM CLI provides the `sam local` command to run your application using Docker containers that simulate the execution environment of Lambda\. There are two options to do this: 
+ Host your API locally
+ Invoke your Lambda function directly

This step describes both options\.

### Host Your API Locally<a name="serverless-getting-started-hello-world-test-locally-host"></a>

**Command to run:**

```
sam local start-api
```

**Example output:**

```
 
 2019-07-12 15:27:58 Mounting HelloWorldFunction at http://127.0.0.1:3000/hello [GET]
 2019-07-12 15:27:58 You can now browse to the above endpoints to invoke your functions. You do not need to restart/reload SAM CLI while working on your functions, changes will be reflected instantly/automatically. You only need to restart SAM CLI if you update your AWS SAM template
 2019-07-12 15:27:58  * Running on http://127.0.0.1:3000/ (Press CTRL+C to quit)

 Fetching lambci/lambda:python3.7 Docker container image......................................................................................................................................................................................
 2019-07-12 15:28:56 Mounting /<working-development-path>/sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated inside runtime container
 START RequestId: 52fdfc07-2182-154f-163f-5f0f9a621d72 Version: $LATEST
 END RequestId: 52fdfc07-2182-154f-163f-5f0f9a621d72
 REPORT RequestId: 52fdfc07-2182-154f-163f-5f0f9a621d72  Duration: 4.42 ms       Billed Duration: 100 ms Memory Size: 128 MB     Max Memory Used: 22 MB
 2019-07-12 15:28:58 No Content-Type given. Defaulting to 'application/json'.
 2019-07-12 15:28:58 127.0.0.1 - - [12/Jul/2019 15:28:58] "GET /hello HTTP/1.1" 200 -
```

It might take a while for the Docker image to load\. After it's loaded, you can use `curl` to send a request to your application that's running on your local host:

```
curl http://127.0.0.1:3000/hello
```

**Example output:**

```
 
 2019-07-12 15:29:57 Invoking app.lambda_handler (python3.7)
 2019-07-12 15:29:57 Found credentials in shared credentials file: ~/.aws/credentials

 Fetching lambci/lambda:python3.7 Docker container image......
 2019-07-12 15:29:58 Mounting /<working-development-path>/sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated inside runtime container
 START RequestId: 52fdfc07-2182-154f-163f-5f0f9a621d72 Version: $LATEST
 END RequestId: 52fdfc07-2182-154f-163f-5f0f9a621d72
 REPORT RequestId: 52fdfc07-2182-154f-163f-5f0f9a621d72  Duration: 7.92 ms       Billed Duration: 100 ms Memory Size: 128 MB     Max Memory Used: 22 MB
 {"statusCode":200,"body":"{\"message\": \"hello world\"}"}
```

**What AWS SAM is doing:**

The `start-api` command starts up a local endpoint that replicates your REST API endpoint\. It downloads an execution container that you can run your function locally in\. The end result is the same output that you saw when you called your function in the AWS Cloud\.

### Making One\-off Invocations<a name="serverless-getting-started-hello-world-test-locally-invoke"></a>

**Command to run:**

```
sam local invoke "HelloWorldFunction" -e events/event.json
```

**Example output:**

```
 
 2019-07-01 14:08:42 Found credentials in shared credentials file: ~/.aws/credentials
 2019-07-01 14:08:42 Invoking app.lambda_handler (python3.7)

 Fetching lambci/lambda:python3.7 Docker container image...............................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................
 2019-07-01 14:09:39 Mounting /<working-development-path>/sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated inside runtime container
 START RequestId: 52fdfc07-2182-154f-163f-5f0f9a621d72 Version: $LATEST
 END RequestId: 52fdfc07-2182-154f-163f-5f0f9a621d72
 REPORT RequestId: 52fdfc07-2182-154f-163f-5f0f9a621d72    Duration: 3.51 ms    Billed Duration: 100 ms    Memory Size: 128 MB    Max Memory Used: 22 MB    
 {"statusCode":200,"body":"{\"message\": \"hello world\"}"}
```

**What AWS SAM is doing:**

The `invoke` command directly invokes your Lambda functions, and can pass input event payloads that you provide\. With this command, you pass the event payload in the file `event.json` that's provided by the sample application\.

Your initialized application came with a default `aws-proxy` event for API Gateway\. A number of values are prepopulated for you\. In this case, the `HelloWorldFunction` doesn't care about the particular values, so a stubbed request is OK\. You can specify a number of values to be substituted in to the request to simulate what you would expect from an actual request\. This following is an example of generating your own input event and comparing the output with the default `event.json` object: 

```
sam local generate-event apigateway aws-proxy --body "" --path "hello" --method GET > api-event.json
$ diff api-event.json event.json
```

**Example output:**

```
 
 <   "body": "",
 ---
 >   "body": "{\"message\": \"hello world\"}",
 4,6c4,6
 <   "path": "/hello",
 <   "httpMethod": "GET",
 <   "isBase64Encoded": true,
 ---
 >   "path": "/path/to/resource",
 >   "httpMethod": "POST",
 >   "isBase64Encoded": false,
 11c11
 <     "proxy": "/hello"
 ---
 >     "proxy": "/path/to/resource"
 56c56
 <     "path": "/prod/hello",
 ---
 >     "path": "/prod/path/to/resource",
 58c58
 <     "httpMethod": "GET",
 ---
 >     "httpMethod": "POST",
```

## Troubleshooting<a name="serverless-getting-started-hello-world-troubleshooting"></a>

### Curl Error: "Missing Authentication Token"<a name="serverless-getting-started-hello-world-troubleshooting-curl-auth-token"></a>

When trying to invoke the API Gateway endpoint, you see the following error:

```
 
 {"message":"Missing Authentication Token"}
```

This means that you've attempted to send a request to the correct domain, but the URI isn't recognizable\. To fix this, verify the full URL, and update the `curl` command with the correct URL\.

### Curl Error: "curl: \(6\) Could not resolve: \.\.\."<a name="serverless-getting-started-hello-world-troubleshooting-curl-domain-not-found"></a>

When trying to invoke the API Gateway endpoint, you see the following error:

```
 
 curl: (6) Could not resolve: endpointdomain (Domain name not found)
```

This means that you've attempted to send a request to an invalid domain\. This can happen if your serverless application failed to deploy successfully, or if you have a typo in your `curl` command\. Verify that the application was deployed successfully by using the AWS CloudFormation console or AWS CLI, and that your `curl` command is correct\.

## Clean Up<a name="serverless-getting-started-hello-world-cleanup"></a>

If you no longer need the AWS resources you created by running this tutorial, you can remove them by deleting the AWS CloudFormation stack that you deployed\.

To delete the AWS CloudFormation stack created with this tutorial using the AWS Management Console, follow these steps:

1. Sign in to the AWS Management Console and open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/)\.

1. In the left navigation pane, choose **Stacks**\.

1. In the list of stacks, choose **aws\-sam\-getting\-started**\.

1. Choose **Delete**\.

When done, the status of the of the stack will change to **DELETE\_COMPLETE**\.

Alternatively, you can delete the AWS CloudFormation stack by executing the following AWS CLI command:

```
aws cloudformation delete-stack --stack-name aws-sam-getting-started --region region
```

### Verify Deleted Stack<a name="serverless-getting-started-hello-world-cleanup-verify"></a>

For both methods of deleting the AWS CloudFormation stack, you can verify it was deleted by going to the [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/), choosing **Stacks** in the left navigation pane, and choosing **Deleted** in the dropdown to the right of the search text box\. You should see your stack name **aws\-sam\-getting\-started** in the list of deleted stacks\.

## Conclusion<a name="serverless-getting-started-hello-world-conclusion"></a>

In this tutorial, you've done the following:

1. Created, built, packaged, and deployed a serverless application to AWS with AWS SAM\.

1. Tested your application locally by using the AWS SAM CLI and Docker\.

1. Deleted the AWS resources that you no longer need\.

## Next Steps<a name="serverless-getting-started-hello-world-next-steps"></a>

You're now ready to start building your own applications using the AWS SAM CLI\.

To help you get started, you can download any of the example applications from the AWS SAM GitHub repository\. To access this repository, see [AWS SAM example applications](https://github.com/awslabs/serverless-application-model/tree/master/examples/apps)\.