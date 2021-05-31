# AWS Cloud Development Kit \(CDK\) \(Preview\)<a name="serverless-cdk"></a>


****  

|  | 
| --- |
| CDK integration with the AWS SAM CLI is currently in public preview\. During public preview, CDK integration with the AWS SAM CLI may be subject to backwards incompatible changes\. | 

You can use the AWS SAM CLI to locally test and build serverless applications defined using the AWS Cloud Development Kit \(CDK\)\. Because the AWS SAM CLI works within the CDK project structure, you can still use the [CDK Toolkit](https://docs.aws.amazon.com/cdk/latest/guide/cli.html) for creating, modifying, and deploying your CDK applications\.

For information about installing and configuring the CDK, see [Getting started with the CDK](https://docs.aws.amazon.com/cdk/latest/guide/getting_started.html) in the *AWS Cloud Development Kit \(CDK\) Developer Guide*\.

**Note**  
The AWS SAM CLI only supports Lambda functions created with the standard Lambda construct\. For information about the standard Lambda construct, see [@aws\-cdk/aws\-lambda module](https://docs.aws.amazon.com/cdk/api/latest/docs/aws-lambda-readme.html)\.

**Topics**
+ [Getting started with AWS SAM and the CDK](serverless-cdk-getting-started.md)
+ [Locally testing CDK applications](serverless-cdk-testing.md)
+ [Building CDK applications](serverless-cdk-building.md)