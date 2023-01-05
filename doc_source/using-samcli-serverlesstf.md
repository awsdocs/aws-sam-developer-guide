# Using the AWS SAM CLI with Serverless\.tf for local debugging and testing<a name="using-samcli-serverlesstf"></a>


|  | 
| --- |
|  Terraform support is in preview release for the AWS SAM CLI and is subject to change\. To provide feedback and submit feature requests, create a [GitHub Issue](https://github.com/aws/aws-sam-cli/issues/new?labels=area%2Fterraform)\.  | 

The AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) can be used with Serverless\.tf modules for local debugging and testing of your AWS Lambda functions and layers\. The following AWS SAM CLI commands are supported:
+ sam local invoke
+ sam local start\-lambda

To begin using the AWS SAM CLI with your Serverless\.tf modules, update to the latest version Serverless\.tf and the AWS SAM CLI\.

**Note**  
Serverless\.tf version 4\.6\.0 and newer supports AWS SAM CLI integration\.

To learn more about Serverless\.tf, see the [terraform\-aws\-lambda\-module](https://registry.terraform.io/modules/terraform-aws-modules/lambda/aws/latest)\.