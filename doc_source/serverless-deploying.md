# Deploying serverless applications<a name="serverless-deploying"></a>

AWS SAM uses AWS CloudFormation as the underlying deployment mechanism\. For more information, see [What is AWS CloudFormation?](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/) in the *AWS CloudFormation User Guide*\.

You can deploy your application using AWS SAM command line interface \(CLI\) commands\. To automate your deployments, you can also use other AWS services that integrate with AWS SAM\.

The standard inputs to deploying serverless applications are the build artifacts created using the `sam build` command\. For more information about `sam build`, see [Building serverless applications](serverless-building.md)\.

## Deploying using the AWS SAM CLI<a name="serverless-sam-cli-using-package-and-deploy"></a>

After you develop and test your serverless application locally, you can deploy your application using the `sam deploy` command\.

If you want AWS SAM to guide you through the deployment with prompts, specify the `--guided` flag\. When you specify this flag, the `sam deploy` command zips your application artifacts, uploads them to either Amazon S3 \(for \.zip file archives\) or Amazon ECR \(for contain images\), and then deploys your application to the AWS Cloud\.

**Example:**

```
# Deploy an application using prompts:
sam deploy --guided
```

## Publishing serverless applications<a name="serverless-deploying-publishing"></a>

The AWS Serverless Application Repository is a service that hosts serverless applications that are built using AWS SAM\. If you want to share serverless applications with others, you can publish them in the AWS Serverless Application Repository\. You can also search, browse, and deploy serverless applications that others have published\. For more information, see [What Is the AWS Serverless Application Repository?](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/what-is-serverlessrepo.html) in the *AWS Serverless Application Repository Developer Guide*\.

## Automating deployments<a name="serverless-deploying-automated"></a>

To automate the deployment process of your serverless application, you can use AWS SAM with a number of other AWS services\.
+ **CodeBuild**: Use AWS CodeBuild to build, locally test, and package your serverless application\. For more information, see [What is AWS CodeBuild?](https://docs.aws.amazon.com/codebuild/latest/userguide/) in the *AWS CodeBuild User Guide*\.
+ **CodeDeploy**: Use [AWS CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html) to gradually deploy updates to your serverless applications\. For more information, see [Deploying serverless applications gradually](automating-updates-to-serverless-apps.md)\.
+ **CodePipeline**: Use AWS CodePipeline to model, visualize, and automate the steps that are required to release your serverless application\. For more information, see [What is AWS CodePipeline?](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html) in the *AWS CodePipeline User Guide*\.

## Troubleshooting<a name="serverless-deploying-troubleshooting"></a>

### AWS SAM CLI error: "Security Constraints Not Satisfied"<a name="troubleshooting-security-constraints"></a>

When executing `sam deploy --guided`, you are prompted with the question `HelloWorldFunction may not have authorization defined, Is this okay? [y/N]`\. If you respond to this prompt with "N" \(the default response\), you see the following error:

```
 
Error: Security Constraints Not Satisfied
```

The prompt is informing you that the application you're about to deploy may have an API Gateway API configured without authorization\. By responding "N" to this prompt \(the default\), you are saying that this is not OK\.

To fix this, you have the following options:
+ Configure your application with authorization\. For information about configuring authorization, see [Controlling access to API Gateway APIs](serverless-controlling-access-to-apis.md)\.
+ Respond to this question with "Y" to indicate that you are OK with deploying an application that has an API Gateway API configured without authorization\.