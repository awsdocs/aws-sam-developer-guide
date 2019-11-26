# Deploying Serverless Applications<a name="serverless-deploying"></a>

AWS SAM uses AWS CloudFormation as the underlying deployment mechanism\. For more information, see [What Is AWS CloudFormation?](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/)\.

You can deploy your application by using AWS SAM command line interface \(CLI\) commands\. You can also use other AWS services that integrate with AWS SAM to automate your deployments\.

## Packaging and Deploying Using the AWS SAM CLI<a name="serverless-sam-cli-using-package-and-deploy"></a>

After you develop and test your serverless application locally, you can deploy your application by using the `sam package` and `sam deploy` commands\.

**Note**  
Both the `sam package` and `sam deploy` commands described in this section are identical to their AWS CLI equivalent commands [ `aws cloudformation package`](http://docs.aws.amazon.com/cli/latest/reference/cloudformation/package.html) and [ `aws cloudformation deploy`](http://docs.aws.amazon.com/cli/latest/reference/cloudformation/deploy/index.html), respectively\.

The `sam package` command zips your code artifacts, uploads them to Amazon S3, and produces a packaged AWS SAM template file that's ready to be used\. The `sam deploy` command uses this file to deploy your application\. For example, the following command generates a `packaged.yaml` file:

```
# Package SAM template
sam package --template-file sam.yaml --s3-bucket mybucket --output-template-file packaged.yaml
```

The following `sam deploy` command takes the packaged AWS SAM template file that was created earlier, and deploys your serverless application:

```
# Deploy packaged SAM template
sam deploy --template-file ./packaged.yaml --stack-name mystack --capabilities CAPABILITY_IAM
```

**Note**  
To deploy an application that contains one or more nested applications, you must include the `CAPABILITY_AUTO_EXPAND` capability in the `sam deploy` command\.

## Publishing Serverless Applications<a name="serverless-deploying-publishing"></a>

The AWS Serverless Application Repository is a service that hosts serverless applications that are built using AWS SAM\. If you want to share serverless applications with others, you can publish them in the AWS Serverless Application Repository\. You can also search, browse, and deploy serverless applications that have been published by others\. For more information, see [ What Is the AWS Serverless Application Repository?](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/what-is-serverlessrepo.html)\.

## Automating Deployments<a name="serverless-deploying-automated"></a>

You can use AWS SAM with a number of other AWS services to automate the deployment process of your serverless application\.
+ **CodeBuild**: You use CodeBuild to build, locally test, and package your serverless application\. For more information, see [What Is CodeBuild?](https://docs.aws.amazon.com/codebuild/latest/userguide/)\.
+ **CodeDeploy**: You use [CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html) to gradually deploy updates to your serverless applications\. For more information on how to do this, see [Deploying Serverless Applications Gradually](automating-updates-to-serverless-apps.md)\.
+ **CodePipeline**: You use CodePipeline to model, visualize, and automate the steps that are required to release your serverless application\. For more information, see [What Is CodePipeline?](https://docs.aws.amazon.com/codepipeline/latest/APIReference/)\.

**Topics**
+ [Deploying Serverless Applications Gradually](automating-updates-to-serverless-apps.md)