# Tutorial: Deploying a Hello World Application<a name="serverless-getting-started-hello-world"></a>

In this guide, you download, build, and deploy a sample Hello World application using AWS SAM\. You then test the application in the AWS Cloud, and optionally test it locally on your development host\.

This application implements a simple API backend\. It consists of an API Gateway endpoint and a Lambda function\. When you send a GET request to the API Gateway endpoint, the Lambda function is invoked\. This function returns a `hello world` message\.

The following diagram shows the components of this application:

![\[A diagram that shows a Lambda function that's invoked when you send a GET request to the API Gateway endpoint\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/images/sam-getting-started-hello-world.png)

The following is a preview of commands that you run to create your Hello World application\. For more details about each of these commands, see the sections later in this page

```
#Step 1 - Download a sample application
sam init

#Step 2 - Build your application
cd sam-app
sam build

#Step 3 - Deploy your application
sam deploy --guided
```

## Prerequisites<a name="serverless-getting-started-hello-world-prerequisites"></a>

This guide assumes that you've completed the steps in the [Installing the AWS SAM CLI](serverless-sam-cli-install.md) for your OS\. It assumes that you've done the following:

1. Created an AWS account\.

1. Configured IAM permissions\.

1. Installed Docker\. Note: Docker is only a prerequisite for testing your application locally\.

1. Installed Homebrew\. Note: Homebrew is only a prerequisite for Linux and macOS\.

1. Installed the AWS SAM CLI\. Note: Make sure you have version 0\.33\.0 or later\. You can check which version you have by executing the command `sam --version`\.

## Step 1: Download a Sample AWS SAM Application<a name="serverless-getting-started-hello-world-initialize"></a>

**Command to run:**

```
sam init
```

Follow the on\-screen prompts\. For this tutorial we recommend you choose AWS Quick Start Templates, the runtime of your choice, and the Hello World Example\.

**Example output:**

```
   
 -----------------------
 Generating application:
 -----------------------
 Name: sam-app
 Runtime: python3.7
 Dependency Manager: pip
 Application Template: hello-world
 Output Directory: .

 Next steps can be found in the README file at ./sam-app/README.md
```

**What AWS SAM is doing:**

This command creates a directory with the name you provided as the project name\. The contents of the project directory are similar to the following \(these contents are created when one of the Python runtimes and the Hello World Example are chose\):

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

First change into the project directory \(that is, the directory where the `template.yaml` file for the sample application is located; by default is `sam-app`\), then run this command:

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
 [*] Deploy: sam deploy --guided
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

## Step 3: Deploy Your Application to the AWS Cloud<a name="serverless-getting-started-hello-world-deploy"></a>

**Command to run:**

```
sam deploy --guided
```

Follow the on\-screen prompts\. You can just respond with `Enter` to accept the default options provided in the interactive experience\.

**Example output:**

```
 
    Deploying with following values
    ===============================
    Stack name                 : sam-app
    Region                     : us-east-1
    Confirm changeset          : False
    Deployment s3 bucket       : sam-bucket
    Capabilities               : ["CAPABILITY_IAM"]
    Parameter overrides        : {}

 Initiating deployment
 =====================

 Waiting for changeset to be created..

 CloudFormation stack changeset
 ---------------------------------------------------------------------------------------------------------------------------------------------------
 Operation                                         LogicalResourceId                                 ResourceType
 ---------------------------------------------------------------------------------------------------------------------------------------------------
 + Add                                             HelloWorldFunctionHelloWorldPermissionProd        AWS::Lambda::Permission
 + Add                                             ServerlessRestApiDeployment47fc2d5f9d             AWS::ApiGateway::Deployment
 + Add                                             ServerlessRestApiProdStage                        AWS::ApiGateway::Stage
 + Add                                             ServerlessRestApi                                 AWS::ApiGateway::RestApi
 * Modify                                          HelloWorldFunctionRole                            AWS::IAM::Role
 * Modify                                          HelloWorldFunction                                AWS::Lambda::Function
 ---------------------------------------------------------------------------------------------------------------------------------------------------

 2019-11-21 14:33:24 - Waiting for stack create/update to complete

 CloudFormation events from changeset
 -------------------------------------------------------------------------------------------------------------------------------------------------
 ResourceStatus                       ResourceType                         LogicalResourceId                    ResourceStatusReason
 -------------------------------------------------------------------------------------------------------------------------------------------------
 UPDATE_IN_PROGRESS                   AWS::IAM::Role                       HelloWorldFunctionRole               -
 UPDATE_COMPLETE                      AWS::IAM::Role                       HelloWorldFunctionRole               -
 UPDATE_IN_PROGRESS                   AWS::Lambda::Function                HelloWorldFunction                   -
 UPDATE_COMPLETE                      AWS::Lambda::Function                HelloWorldFunction                   -
 CREATE_IN_PROGRESS                   AWS::ApiGateway::RestApi             ServerlessRestApi                    -
 CREATE_COMPLETE                      AWS::ApiGateway::RestApi             ServerlessRestApi                    -
 CREATE_IN_PROGRESS                   AWS::ApiGateway::RestApi             ServerlessRestApi                    Resource creation Initiated
 CREATE_IN_PROGRESS                   AWS::ApiGateway::Deployment          ServerlessRestApiDeployment47fc2d5   Resource creation Initiated
                                                                          f9d
 CREATE_IN_PROGRESS                   AWS::Lambda::Permission              HelloWorldFunctionHelloWorldPermis   Resource creation Initiated
                                                                          sionProd
 CREATE_IN_PROGRESS                   AWS::Lambda::Permission              HelloWorldFunctionHelloWorldPermis   -
                                                                          sionProd
 CREATE_IN_PROGRESS                   AWS::ApiGateway::Deployment          ServerlessRestApiDeployment47fc2d5   -
                                                                          f9d
CREATE_COMPLETE                      AWS::ApiGateway::Deployment          ServerlessRestApiDeployment47fc2d5   -
                                                                          f9d
 CREATE_IN_PROGRESS                   AWS::ApiGateway::Stage               ServerlessRestApiProdStage           -
 CREATE_IN_PROGRESS                   AWS::ApiGateway::Stage               ServerlessRestApiProdStage           Resource creation Initiated
 CREATE_COMPLETE                      AWS::ApiGateway::Stage               ServerlessRestApiProdStage           -
 CREATE_COMPLETE                      AWS::Lambda::Permission              HelloWorldFunctionHelloWorldPermis   -
                                                                          sionProd
 UPDATE_COMPLETE_CLEANUP_IN_PROGRES   AWS::CloudFormation::Stack           sam-app                              -
 S
 UPDATE_COMPLETE                      AWS::CloudFormation::Stack           sam-app                              -
 -------------------------------------------------------------------------------------------------------------------------------------------------

 Stack sam-app outputs:
 ---------------------------------------------------------------------------------------------------------------------------------------------------
 OutputKey-Description                                                     OutputValue
 ---------------------------------------------------------------------------------------------------------------------------------------------------
 HelloWorldFunctionIamRole - Implicit IAM Role created for Hello World     arn:aws:iam::123456789012:role/sam-app-
 function                                                                  HelloWorldFunctionRole-104VTJ0TST7M0
 HelloWorldApi - API Gateway endpoint URL for Prod stage for Hello World   https://0ks2zue0zh.execute-api.us-east-1.amazonaws.com/Prod/hello/
 function
 HelloWorldFunction - Hello World Lambda Function ARN                      arn:aws:lambda:us-east-1:123456789012:function:sam-app-
                                                                          HelloWorldFunction-1TY92MJX0BXU5
 ---------------------------------------------------------------------------------------------------------------------------------------------------

 Successfully created/updated stack - sam-app in us-east-1
```

**What AWS SAM is doing:**

This command deploys your application to the AWS cloud\. It take the deployment artifacts you build with the `sam build` command, packages and uploads them to an Amazon S3 bucket created by AWS SAM CLI, and deploys the application using AWS CloudFormation\. In the output of the deploy command you can see the changes being made to your AWS CloudFormation stack\. 

If your application created a HTTP endpoint, the Outputs generated by `sam deploy` also show you the endpoint URL for your test application\. You can use `curl` to send a request to your application using that endpoint URL\. For example:

```
curl https://<restapiid>.execute-api.us-east-1.amazonaws.com/Prod/hello/
```

You should see output like the following after successfully deploying your application:

```
 
 {"message": "hello world"}
```

If you see `{"message": "hello world"}` after executing the `curl` command, it means that you've successfully deployed your serverless application to AWS, and are calling your live Lambda function\. Otherwise, see the [Troubleshooting](#serverless-getting-started-hello-world-troubleshooting) section later in this tutorial\.

## Step 4: Testing Your Application Locally \(Optional\)<a name="serverless-getting-started-hello-world-test-locally"></a>

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

### SAM CLI error: "no such option: \-\-app\-template"<a name="serverless-getting-started-hello-world-troubleshooting-app-template"></a>

When executing `sam init`, you see the following error:

```
 
Error: no such option: --app-template
```

This means that you are using an older version of the AWS SAM CLI that does not support the `--app-template` parameter\. To fix this, you can either update your version of AWS SAM CLI to 0\.30\.0 or later, or omit the `--app-template` parameter from the `sam init` command\.

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

1. Created, built, and deployed a serverless application to AWS with AWS SAM\.

1. Tested your application locally by using the AWS SAM CLI and Docker\.

1. Deleted the AWS resources that you no longer need\.

## Next Steps<a name="serverless-getting-started-hello-world-next-steps"></a>

You're now ready to start building your own applications using the AWS SAM CLI\.

To help you get started, you can download any of the example applications from the AWS SAM GitHub repository\. To access this repository, see [AWS SAM example applications](https://github.com/awslabs/serverless-application-model/tree/master/examples/apps)\.