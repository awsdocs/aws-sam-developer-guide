# AWS SAM Accelerate<a name="accelerate"></a>

You can use AWS SAM Accelerate to update and monitor serverless applications in AWS Cloud during development\.

AWS SAM Accelerate speeds up deployments from your development environment to the AWS Cloud by using AWS service APIs instead of AWS CloudFormation to deploy code updates\. AWS SAM Accelerate also supports automatic deployments to the AWS Cloud as you make changes to your application\.

By deploying to the AWS Cloud during development, you can identify issues with your application that are difficult to detect in your local environment\. For example, testing in the AWS Cloud can help you identify issues with IAM roles or API authorization\.

The [sam sync](sam-cli-command-reference-sam-sync.md) command deploys your local changes to the AWS Cloud\.

 You can use the [sam logs](sam-cli-command-reference-sam-logs.md) and [sam traces](sam-cli-command-reference-sam-traces.md) commands to monitor your serverless application\.

For a hands\-on example of using AWS SAM Accelerate, see [Module 6 \- AWS SAM Accelerate](https://s12d.com/sam-ws-en-accelerate) in *The Complete AWS SAM Workshop*\.

**Topics**
+ [Getting started with AWS SAM Accelerate](accelerate-getting-started.md)