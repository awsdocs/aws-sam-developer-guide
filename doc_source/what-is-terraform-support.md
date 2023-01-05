# What is AWS SAM CLI support for Terraform?<a name="what-is-terraform-support"></a>


|  | 
| --- |
|  Terraform support is in preview release for the AWS SAM CLI and is subject to change\. To provide feedback and submit feature requests, create a [GitHub Issue](https://github.com/aws/aws-sam-cli/issues/new?labels=area%2Fterraform)\.  | 

Use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) within your Terraform projects to perform local debugging and testing of your AWS Lambda functions and layers\.

**Topics**
+ [Local debugging and testing with AWS SAM CLI](#what-is-terraform-support-local)
+ [How the AWS SAM CLI interacts with your Terraform projects](#what-is-terraform-support-how)
+ [Benefits of AWS SAM CLI Terraform support](#what-is-terraform-support-benefits)
+ [Next steps](#what-is-terraform-support-next)

## Local debugging and testing with AWS SAM CLI<a name="what-is-terraform-support-local"></a>

The AWS SAM CLI supports the following commands for your Terraform projects:
+ sam build – Package the Lambda resources in your Terraform projects to use with the AWS SAM CLI for local debugging and testing\. For more information on sam build, see [sam build](sam-cli-command-reference-sam-build.md)\.
+ sam local invoke – Invoke an AWS Lambda function once\. For more information on sam local invoke, see [sam local invoke](sam-cli-command-reference-sam-local-invoke.md)\.
+ sam local start\-lambda – Start a local endpoint for your Lambda function in order to invoke your function locally using AWS Command Line Interface \(AWS CLI\) or SDKs\. For more information on sam local start\-lambda, see [sam local start\-lambda](sam-cli-command-reference-sam-local-start-lambda.md)\.

## How the AWS SAM CLI interacts with your Terraform projects<a name="what-is-terraform-support-how"></a>

The AWS SAM CLI uses Terraform commands to inspect the state of your project in order to identify Lambda resources with their source and package artifacts\. Optionally, a Metadata resource will need to be defined in your Terraform config files for AWS SAM CLI to reference\. With AWS SAM CLI support for Terraform, you can:
+ Use sam build to prepare for local testing\.
+ Use sam local invoke and sam local start\-lambda to debug and test your Lambda functions\.

## Benefits of AWS SAM CLI Terraform support<a name="what-is-terraform-support-benefits"></a>

With AWS SAM CLI support for Terraform, you can locally debug and test your Lambda functions immediately before applying and deploying your changes, speeding up your development and testing processes and workflows\.

## Next steps<a name="what-is-terraform-support-next"></a>

To prepare for using the AWS SAM CLI with Terraform, see [Getting started](gs-terraform-support.md)\.