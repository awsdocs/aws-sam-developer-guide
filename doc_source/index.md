# AWS Serverless Application Model Developer Guide

-----
*****Copyright &copy; 2018 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What Is the AWS Serverless Application Model (AWS SAM)?](what-is-sam.md)
+ [Quick Start](serverless-quick-start.md)
+ [AWS SAM Template Basics](serverless-sam-template-basics.md)
   + [Declaring Serverless Resources](serverless-sam-template.md)
   + [Declaring AWS CloudFormation Resources](appendix-appendix-sam-templates-and-cf-templates.md)
+ [Testing and Debugging Serverless Applications](serverless-test-and-debug.md)
   + [Building Applications with Dependencies](serverless-sam-cli-using-build.md)
   + [Invoking Functions Locally](serverless-sam-cli-using-invoke.md)
   + [Running API Gateway Locally](serverless-sam-cli-using-start-api.md)
   + [Running Automated Tests](serverless-sam-cli-using-automated-tests.md)
   + [Generating Sample Event Payloads](serverless-sam-cli-using-generate-event.md)
   + [Working with Logs](serverless-sam-cli-logging.md)
   + [Debugging Lambda Functions Locally](serverless-sam-cli-using-debugging.md)
      + [Debugging Node.js Functions Locally](serverless-sam-cli-using-debugging-nodejs.md)
      + [Debugging Python Functions Locally](serverless-sam-cli-using-debugging-python.md)
      + [Debugging Golang Functions Locally](serverless-sam-cli-using-debugging-golang.md)
   + [Passing Additional Runtime Debug Arguments](serverless-sam-cli-using-debugging-additional-arguments.md)
   + [Validating AWS SAM Template Files](serverless-sam-cli-using-validate.md)
+ [Deploying Serverless Applications](serverless-deploying.md)
   + [Gradual Code Deployment](automating-updates-to-serverless-apps.md)
+ [Example Serverless Applications](serverless-example-applications.md)
   + [Process DynamoDB Events](serverless-example-ddb.md)
   + [Process Amazon S3 Events](serverless-example-s3.md)
+ [AWS SAM Reference](serverless-sam-reference.md)
   + [Installing the AWS SAM CLI](serverless-sam-cli-install.md)
      + [Install the AWS SAM CLI Using Pip](serverless-sam-cli-install-using-pip.md)
         + [Adjusting Path on Linux](serverless-sam-cli-install-linux-path.md)
         + [Adjusting Path on Windows](serverless-sam-cli-install-windows-path.md)
         + [Adjusting Path on macOS](serverless-sam-cli-install-mac-path.md)
      + [Installing AWS SAM CLI on Linux](serverless-sam-cli-install-linux.md)
      + [Installing AWS SAM CLI on Windows](serverless-sam-cli-install-windows.md)
      + [Installing AWS SAM CLI on macOS](serverless-sam-cli-install-mac.md)
      + [Advanced Installations](serverless-sam-cli-install-advanced.md)
   + [AWS SAM CLI Command Reference](serverless-sam-cli-command-reference.md)
      + [sam build](sam-cli-command-reference-sam-build.md)
      + [sam deploy](sam-cli-command-reference-sam-deploy.md)
      + [sam init](sam-cli-command-reference-sam-init.md)
      + [sam local generate-event](sam-cli-command-reference-sam-local-generate-event.md)
      + [sam local invoke](sam-cli-command-reference-sam-local-invoke.md)
      + [sam local start-api](sam-cli-command-reference-sam-local-start-api.md)
      + [sam local start-lambda](sam-cli-command-reference-sam-local-start-lambda.md)
      + [sam logs](sam-cli-command-reference-sam-logs.md)
      + [sam package](sam-cli-command-reference-sam-package.md)
      + [sam validate](sam-cli-command-reference-sam-validate.md)
+ [Document History for AWS Serverless Application Model](doc-history.md)