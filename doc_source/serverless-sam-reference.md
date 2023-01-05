# AWS SAM reference<a name="serverless-sam-reference"></a>

## AWS SAM specification<a name="serverless-sam-spec"></a>

The AWS SAM specification is an open\-source specification under the Apache 2\.0 license\. The current version of the AWS SAM specification is available in the [AWS Serverless Application Model \(AWS SAM\) specification](sam-specification.md)\.

AWS SAM templates are an extension of AWS CloudFormation templates\. For the full reference for AWS CloudFormation templates, see [Template reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html) in the *AWS CloudFormation User Guide*\.

## AWS SAM CLI command reference<a name="serverless-sam-cli"></a>

The AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) is a command line tool that you can use with AWS SAM templates and supported third\-party integrations to build and run your serverless applications\.

You can use the AWS SAM CLI commands to develop, test, and deploy your serverless applications to the AWS Cloud\. The following are some examples of AWS SAM CLI commands:
+ `sam init` – If you're a first\-time AWS SAM CLI user, you can run the `sam init` command without any parameters to create a Hello World application\. The command generates a preconfigured AWS SAM template and example application code in the language that you choose\.
+ `sam local invoke` and `sam local start-api` – Use these commands to test your application code locally, before deploying it to the AWS Cloud\.
+ `sam logs` – Use this command to fetch logs that your Lambda function generates\. This can help you with testing and debugging your application after you've deployed it to the AWS Cloud\.
+ `sam package` – Use this command to bundle your application code and dependencies into a *deployment package*\. You need the deployment package to upload your application to the AWS Cloud\.
+ `sam deploy` – Use this command to deploy your serverless application to the AWS Cloud\. It creates the AWS resources and sets permissions and other configurations that are defined in the AWS SAM template\.

For instructions about installing the AWS SAM CLI, see [Installing the AWS SAM CLI](install-sam-cli.md)\.

## AWS SAM policy templates<a name="serverless-policy-temps"></a>

With AWS SAM, you can choose from a list of policy templates to scope your AWS Lambda function's permissions to the resources that your application uses\.

## Topics<a name="reference-sam-topics"></a>
+ [AWS Serverless Application Model \(AWS SAM\) specification](sam-specification.md)
+ [AWS SAM CLI command reference](serverless-sam-cli-command-reference.md)
+ [AWS SAM CLI configuration file](serverless-sam-cli-config.md)
+  [AWS SAM connector reference](reference-sam-connector.md) 
+ [AWS SAM policy templates](serverless-policy-templates.md)
+ [Image repositories](serverless-image-repositories.md)
+ [Telemetry in the AWS SAM CLI](serverless-sam-telemetry.md)
+ [Managing resource access and permissions](sam-permissions.md)