# Managing resource access and permissions<a name="sam-permissions"></a>

For your AWS resources to interact with one another, the proper access and permissions must be configured between your resources, requiring the configuration of AWS Identity and Access Management \(IAM\) users, roles, and policies to accomplish your interaction in a secure manner\. To learn more, see [Controlling access with AWS Identity and Access Management](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-iam-template.html) in the *AWS CloudFormation User Guide*\.

The AWS Serverless Application Model \(AWS SAM\) provides two options that simplify management of access and permissions for your serverless applcations\.

1. AWS SAM connectors

1. AWS SAM policy templates

## AWS SAM connectors<a name="sam-permissions-intro-connectors"></a>

Connectors are a way to grant model the permissions needed for two services in your SAM template to successfully interact. Connectors are defined with the `Connectors` resource attribute or as an AWS SAM abstract resource type, identified as `AWS::Serverless::Connector`. SAM connectors can be used to grant `Read` and `Write` access of data and events from a supported AWS resource to another\. To learn more about AWS SAM connectors, see [Managing resource permissions with AWS SAM connectors](managing-permissions-connectors.md)\.

## AWS SAM policy templates<a name="sam-permissions-intro-policy-templates"></a>

AWS SAM policy templates are pre\-defined sets of permissions that you can add to your AWS SAM templates to manage access and permissions between your AWS Lambda functions, AWS Step Functions state machines and the resources they interact with\. To learn more about AWS SAM policy templates, see [AWS SAM policy templates](serverless-policy-templates.md)\.

## AWS CloudFormation mechanisms<a name="sam-permissions-intro-cloudformation"></a>

AWS CloudFormation mechanisms include the configuring of IAM users, roles, and policies to manage permissions between your AWS resources\. To learn more, see [Managing permissions with AWS CloudFormation mechanisms](sam-permissions-cloudformation.md)\.

## Best practices<a name="sam-permissions-intro-best-practices"></a>

Throughout your serverless applications, you can use multiple methods to configure permissions between your resources\. Therefore, you can select the best option for each scenario and use multiple options together throughout your applications\. Here are a few things to consider when choosing the best option for you:
+ AWS SAM connectors and policy templates both reduce the IAM expertise required to facilitate secure interactions between your AWS resources\. Use connectors and policy templates when supported\.
+ AWS SAM connectors provide a simple and intuitive short\-hand syntax to define permissions in your AWS SAM templates and require the least amount of IAM expertise\. When both AWS SAM connectors and policy templates are supported, use AWS SAM connectors\.
+ AWS SAM connectors can provision `Read` and `Write` access of data and events between supported AWS SAM source and destination resources\. For a list of supported resources, see [AWS SAM connector reference](reference-sam-connector.md)\. When supported, use AWS SAM connectors\.
+ While AWS SAM policy templates are limited to permissions between your Lambda functions, Step Functions state machines and the AWS resources they interact with, policy templates do support all CRUD operations\. When supported, and when an AWS SAM policy template for your scenario is available, use AWS SAM policy templates\. For a list of available policy templates, see [AWS SAM policy templates](serverless-policy-templates.md)\.
+ For all other scenarios, or when granularity is required, use AWS CloudFormation mechanisms\.
