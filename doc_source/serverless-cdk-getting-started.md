# Getting started with AWS SAM and the AWS CDK<a name="serverless-cdk-getting-started"></a>


****  

|  | 
| --- |
| CDK integration with the AWS SAM CLI is currently in public preview\. During public preview, CDK integration with the AWS SAM CLI may be subject to backwards incompatible changes\. | 

This topic describes what you need to use the AWS SAM CLI with AWS CDK applications, and provides instructions for building and locally testing a simple AWS CDK application\.

## Prerequisites<a name="serverless-cdk-getting-started-prerequisites"></a>

To use the AWS SAM CLI with AWS CDK, you must install the AWS CDK, and the public preview version of the AWS SAM CLI\.
+ For information about installing the AWS CDK, see [Getting started with the AWS CDK](https://docs.aws.amazon.com/cdk/latest/guide/getting_started.html) in the *AWS Cloud Development Kit \(CDK\) Developer Guide*\.
+ To install the public preview version of the AWS SAM CLI, follow the same instructions for [Installing the AWS SAM CLI](serverless-sam-cli-install.md) the OS of your development host, but use the public preview download link or installation command as listed below:
  + **Linux:** The private preview build is available with this download link: [AWS SAM CLI beta CDK build](https://github.com/aws/aws-sam-cli/releases/download/sam-cli-beta-cdk/aws-sam-cli-linux-x86_64.zip)\.
  + **Windows:** The private preview is available with this download link: [AWS SAM CLI beta CDK build](https://github.com/aws/aws-sam-cli/releases/download/sam-cli-beta-cdk/AWS_SAM_CLI_64_PY3.msi)\.
  + **macOS:** The private preview is available using the following command `brew install aws-sam-cli-beta-cdk`\.

  To verify you have installed the public preview version, run the `sam-beta-cdk --version` command\. The output of this command is in the form `1.X.Y.dev<YYYYMMDDHHmm>`, for example:

  ```
  SAM CLI, version 1.22.0.dev202104281200
  ```

## Locally testing a AWS CDK application<a name="serverless-cdk-tutorial-hello-world"></a>

To locally test an AWS CDK application using the AWS SAM CLI, you must start with a AWS CDK application that contains a Lambda function\. If you don't already have a AWS CDK application that contains a Lambda function, you can follow the instructions for [Creating a serverless application using the AWS CDK](https://docs.aws.amazon.com/cdk/latest/guide/serverless_example.html) in the *AWS Cloud Development Kit \(CDK\) Developer Guide*\.

**Note**  
The AWS SAM CLI only supports Lambda functions created with the standard Lambda construct\. For information about the standard Lambda construct, see [@aws\-cdk/aws\-lambda module](https://docs.aws.amazon.com/cdk/api/latest/docs/aws-lambda-readme.html)\.

Locally testing your AWS CDK application involves using the AWS SAM CLI to locally invoke a Lambda function defined in your application\. To do this, you need the function identifier that you want to invoke, and the stack name where the function is defined\.

For example, consider a stack and a function that are declared with the following sample:

```
app = new HelloCdkStack(app, "HelloCdkStack",
   ...
)

class HelloCdkStack extends cdk.Stack {
  constructor(scope: cdk.Construct, id: string, props?: cdk.StackProps) {
    ...
    const fn = new lambda.Function(this, 'MyFunction', {
  		...
	});
}
```

The following command locally invokes the Lambda function defined in example presented above:

```
sam-beta-cdk local invoke HelloCdkStack/MyFunction
```

For more information about options available for test AWS CDK applications using AWS SAM CLI, see [Locally testing AWS CDK applications](serverless-cdk-testing.md)\.