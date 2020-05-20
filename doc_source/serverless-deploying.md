# Deploying Serverless Applications<a name="serverless-deploying"></a>

AWS SAM uses AWS CloudFormation as the underlying deployment mechanism\. For more information, see [What Is AWS CloudFormation?](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/)\.

You can deploy your application by using AWS SAM command line interface \(CLI\) commands\. You can also use other AWS services that integrate with AWS SAM to automate your deployments\.

The standard input to deploying serverless applications is the build artifacts created using the `[sam build](sam-cli-command-reference-sam-build.md)`\. For more information about the `sam build` command, see [Building Serverless Applications](serverless-building.md)\.

## Deploying Using the AWS SAM CLI<a name="serverless-sam-cli-using-package-and-deploy"></a>

After you develop and test your serverless application locally, you can deploy your application by using the `sam deploy` command\.

If you want AWS SAM to guide you through the deployment with prompts, specify the `--guided` flag\. When you specify this flag, the `sam deploy` command zips your application artifacts, uploads them to Amazon Simple Storage Service \(Amazon S3\), and deploys your application to the AWS Cloud\.

**Example:**

```
# Deploy an application using prompts:
sam deploy --guided
```

## Publishing Serverless Applications<a name="serverless-deploying-publishing"></a>

The AWS Serverless Application Repository is a service that hosts serverless applications that are built using AWS SAM\. If you want to share serverless applications with others, you can publish them in the AWS Serverless Application Repository\. You can also search, browse, and deploy serverless applications that have been published by others\. For more information, see [ What Is the AWS Serverless Application Repository?](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/what-is-serverlessrepo.html)\.

## Automating Deployments<a name="serverless-deploying-automated"></a>

You can use AWS SAM with a number of other AWS services to automate the deployment process of your serverless application\.
+ **CodeBuild**: You use CodeBuild to build, locally test, and package your serverless application\. For more information, see [What Is CodeBuild?](https://docs.aws.amazon.com/codebuild/latest/userguide/)\.
+ **CodeDeploy**: You use [CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html) to gradually deploy updates to your serverless applications\. For more information, see [Deploying Serverless Applications Gradually](automating-updates-to-serverless-apps.md)\.
+ **CodePipeline**: You use CodePipeline to model, visualize, and automate the steps that are required to release your serverless application\. For more information, see [What Is CodePipeline?](https://docs.aws.amazon.com/codepipeline/latest/APIReference/)\.

**Topics**
+ [Deploying Serverless Applications Gradually](automating-updates-to-serverless-apps.md)