# What is the AWS Serverless Application Model \(AWS SAM\)?<a name="what-is-sam"></a>

The AWS Serverless Application Model \(AWS SAM\) is an open\-source framework that you can use to build [serverless applications](https://aws.amazon.com/serverless/) on AWS\.

A **serverless application** is a combination of Lambda functions, event sources, and other resources that work together to perform tasks\. Note that a serverless application is more than just a Lambda function—it can include additional resources such as APIs, databases, and event source mappings\.

You can use AWS SAM to define your serverless applications\. AWS SAM consists of the following components:
+ **AWS SAM template specification**\. You use this specification to define your serverless application\. It provides you with a simple and clean syntax to describe the functions, APIs, permissions, configurations, and events that make up a serverless application\. You use an AWS SAM template file to operate on a single, deployable, versioned entity that's your serverless application\. For the full AWS SAM template specification, see [AWS Serverless Application Model \(AWS SAM\) specification](sam-specification.md)\.

   
+ **AWS SAM command line interface \(AWS SAM CLI\)**\. You use this tool to build serverless applications that are defined by AWS SAM templates\. The CLI provides commands that enable you to verify that AWS SAM template files are written according to the specification, invoke Lambda functions locally, step\-through debug Lambda functions, package and deploy serverless applications to the AWS Cloud, and so on\. For details about how to use the AWS SAM CLI, including the full AWS SAM CLI Command Reference, see [AWS SAM CLI command reference](serverless-sam-reference.md#serverless-sam-cli)\.

This guide shows you how to use AWS SAM to define, test, and deploy a simple serverless application\. It also provides an [example application](serverless-getting-started-hello-world.md) that you can download, test locally, and deploy to the AWS Cloud\. You can use this example application as a starting point for developing your own serverless applications\.

## Benefits of using AWS SAM<a name="benefits-of-using-sam"></a>

Because AWS SAM integrates with other AWS services, creating serverless applications with AWS SAM provides the following benefits:
+ **Single\-deployment configuration**\. AWS SAM makes it easy to organize related components and resources, and operate on a single stack\. You can use AWS SAM to share configuration \(such as memory and timeouts\) between resources, and deploy all related resources together as a single, versioned entity\.

   
+ **Extension of AWS CloudFormation**\. Because AWS SAM is an extension of AWS CloudFormation, you get the reliable deployment capabilities of AWS CloudFormation\. You can define resources by using AWS CloudFormation in your AWS SAM template\. Also, you can use the full suite of resources, intrinsic functions, and other template features that are available in AWS CloudFormation\.

   
+ **Built\-in best practices**\. You can use AWS SAM to define and deploy your infrastructure as config\. This makes it possible for you to use and enforce best practices such as code reviews\. Also, with a few lines of configuration, you can enable safe deployments through CodeDeploy, and can enable tracing by using AWS X\-Ray\.

   
+ **Local debugging and testing**\. The AWS SAM CLI lets you locally build, test, and debug serverless applications that are defined by AWS SAM templates\. The CLI provides a Lambda\-like execution environment locally\. It helps you catch issues upfront by providing parity with the actual Lambda execution environment\. To step through and debug your code to understand what the code is doing, you can use AWS SAM with AWS toolkits like the [AWS Toolkit for JetBrains](https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/), [AWS Toolkit for PyCharm](https://aws.amazon.com/pycharm/), [AWS Toolkit for IntelliJ](https://aws.amazon.com/intellij/), and [AWS Toolkit for Visual Studio Code](https://aws.amazon.com/visualstudiocode/)\. This tightens the feedback loop by making it possible for you to find and troubleshoot issues that you might run into in the cloud\.

   
+ **Deep integration with development tools**\. You can use AWS SAM with a suite of AWS tools for building serverless applications\. You can discover new applications in the [AWS Serverless Application Repository](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/)\. For authoring, testing, and debugging AWS SAM–based serverless applications, you can use the [AWS Cloud9 IDE](https://docs.aws.amazon.com/cloud9/latest/user-guide/)\. To build a deployment pipeline for your serverless applications, you can use [CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/), [CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/), and [CodePipeline](https://docs.aws.amazon.com/codepipeline/latest/userguide/)\. You can also use [AWS CodeStar](https://docs.aws.amazon.com/codestar/latest/userguide/) to get started with a project structure, code repository, and a CI/CD pipeline that's automatically configured for you\. To deploy your serverless application, you can use the [Jenkins plugin](https://plugins.jenkins.io/aws-sam/)\. You can use the [Stackery\.io toolkit](https://www.stackery.io/product/aws-sam/) to build production\-ready applications\.

## Next step<a name="building-serverless-applications-nextstep"></a>

   [Getting started with AWS SAM](serverless-getting-started.md) 