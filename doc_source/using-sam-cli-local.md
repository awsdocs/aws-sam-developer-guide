# Using sam local<a name="using-sam-cli-local"></a>

Use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam local` command to test your serverless applications locally\.

For an introduction to the AWS SAM CLI, see [What is the AWS SAM CLI?](what-is-sam.md#what-is-sam-cli)\.

## Prerequisites<a name="using-sam-cli-local-prerequisites"></a>

To use `sam local`, install the AWS SAM CLI by completing the following:
+ [AWS SAM prerequisites](prerequisites.md)\.
+ [Installing the AWS SAM CLI](install-sam-cli.md)\.

Before using `sam local`, we recommend a basic understanding of the following:
+ [Configuring the AWS SAM CLI](using-sam-cli-configure.md)\.
+ [Using sam init](using-sam-cli-init.md)\.
+ [Using sam build](using-sam-cli-build.md)\.
+ [Using sam deploy](using-sam-cli-deploy.md)\.

## Using the sam local command<a name="using-sam-cli-local-command"></a>

Use the `sam local` command with any of its subcommands to perform different types of local testing for your application\.

```
$ sam local <subcommand>
```

To learn more about each subcommand, see the following:
+ **[sam local generate\-event](using-sam-cli-local-generate-event.md)** – Generate AWS service events for local testing\.
+ **[sam local invoke](using-sam-cli-local-invoke.md)** – Initiate a one\-time invocation of an AWS Lambda function locally\.
+ **[sam local start\-api](using-sam-cli-local-start-api.md)** – Run your Lambda functions using a local HTTP server\.
+ **[sam local start\-lambda](using-sam-cli-local-start-lambda.md)** – Run your Lambda functions using a local HTTP server for use with the AWS CLI or SDKs\.