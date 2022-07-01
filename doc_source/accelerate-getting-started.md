# Getting started with AWS SAM Accelerate<a name="accelerate-getting-started"></a>

 This topic describes what you need to use AWS SAM Accelerate, and provides instructions for building and deploying a simple application\.

## Prerequisites<a name="serverless-accelerate-getting-started-prerequisites"></a>

To use the AWS SAM Accelerate, you must install version 1\.53\.0 or greater of the AWS SAM CLI\. For installation instructions, see [Installing the AWS SAM CLI](serverless-sam-cli-install.md)\.

## Getting started with Accelerate tutorial<a name="accelerate-tutorial"></a>

In this guide, you download, build, and deploy a sample Hello World application using AWS SAM\. You then make a code change that AWS SAM Accelerate automatically deploys and test the application in the AWS Cloud\.

This application implements a basic API backend\.

### Prerequisites<a name="serverless-getting-started-accelerate-prerequisites"></a>

This tutorial assumes that you're familiar with the basics of AWS SAM\. For a more\-detailed tutorial, see [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md)\.

### Step 1: Download a sample AWS SAM application<a name="serverless-getting-started-accelerate-initialize"></a>

**Command to run:**

```
sam init --app-template hello-world --name sam-tutorial --package-type Zip --runtime python3.9
```

For this tutorial, we use a "Hello World" Python application with a `Zip` package type\.

### Step 2: Start sam sync \-\-watch<a name="serverless-getting-started-accelerate-sync-watch"></a>

First, change into the `sam-tutorial` directory, where the `template.yaml` file for the sample application is located\. Then, run the following command to start a process that watches your serverless application for changes\. Respond with `Y` when prompted to confirm that you want to use the preview feature\.

```
sam sync --watch --stack-name sam-app
```

The first time that you run the `sync --watch` command, AWS SAM starts an AWS CloudFormation deployment\. After the deployment, AWS SAM watches for changes to your serverless application\. For subsequent changes to code resources, such as Lambda functions, AWS SAM automatically deploys changes using service APIs\. For changes to infrastructure, such as IAM roles, AWS SAM automatically starts an AWS CloudFormation deployment\.

### Step 3: Make a change to your application<a name="serverless-getting-started-accelerate-update-code"></a>

With the `sync --watch` process running, update your local Lambda function code\. AWS SAM automatically builds your Lambda function, and deploys your update to the AWS Cloud\. AWS SAM calls a Lambda API to update your function's code, rather than deploying your AWS CloudFormation stack\. The change should take a few seconds to deploy\.

Change your function code to the following to write `Invoking the updated function` to your Lambda function logs:

```
import json
def lambda_handler(event, context):
    print("Invoking the updated function")
    return {
        "statusCode": 200,
        "body": json.dumps({
            "message": "hello world",
        }),
    }
```

### Step 4: Test your application and check the logs<a name="serverless-getting-started-accelerate-test"></a>

Invoke your API using `curl`, and then check the logs from your Lambda function\.

```
curl https://restapiid.execute-api.us-east-1.amazonaws.com/Prod/hello/
```

Use the [`logs`](sam-cli-command-reference-sam-logs.md) command to fetch logs from your application\.

```
sam logs --tail
```

If you see `Invoking the updated function` in the logs, you've successfully deployed Lambda function updates to the AWS Cloud\.

**Note**  
Because Accelerate used a Lambda API to update your function code, your AWS CloudFormation stack doesn't reflect the update to your application\. To update your AWS CloudFormation stack with the latest changes, run `sam sync`\.

### Clean up<a name="serverless-getting-started-accelerate-cleanup"></a>

If you no longer need the AWS resources that you created by running this tutorial, you can remove them by deleting the AWS CloudFormation stack that you deployed\.

To delete the AWS CloudFormation stack, use the `sam --delete` command:

```
sam delete --stack-name sam-app
```

### Conclusion<a name="serverless-getting-started-accelerate-conclusion"></a>

In this tutorial, you've done the following:

1. Created, built, and deployed a serverless application to AWS using AWS SAM\.

1. Used `sam sync --watch` to automatically deploy changes to the AWS Cloud\.

1. Tested your application in the AWS Cloud\.

1. Deleted the AWS resources that you no longer need\.