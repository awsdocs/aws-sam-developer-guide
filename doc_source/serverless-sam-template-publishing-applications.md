# Publishing Serverless Applications Using the AWS SAM CLI<a name="serverless-sam-template-publishing-applications"></a>

You can use the AWS SAM CLI to publish your application to the AWS Serverless Application Repository to make it available for others to find and deploy\.

The application you want to publish must be one that you've defined using AWS SAM, and that you've tested locally and/or in the AWS Cloud\. The application's deployment package and AWS SAM template are the inputs to the steps below\.

The following instructions either create a new application, create a new version of an existing application, or update the metadata of an existing application\. This depends on whether the application already exists in the AWS Serverless Application Repository, and whether any application metadata is changing\. For more information about application metadata that's used to publish applications, see [AWS SAM Template Metadata Section Properties](serverless-sam-template-publishing-applications-metadata-properties.md)\.

## Prerequisites<a name="serverless-sam-template-publishing-applications-prerequisites"></a>

Before you publish an application to the AWS Serverless Application Repository, you need the following:
+ A valid AWS account with an IAM user that has administrator permissions\. See [Set Up an AWS Account](https://docs.aws.amazon.com/lambda/latest/dg/setup.html)\.
+ Version 1\.16\.77 or later of the AWS CLI installed\. See [Installing the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)\.
+ The AWS SAM CLI \(command line interface\) installed\. See [Installing the AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)\.
+ A valid AWS Serverless Application Model \(AWS SAM\) template\.
+ Your application code and dependencies referenced by the AWS SAM template\.
+ A semantic version for your application \(required to share your application publicly\)\.
+ A URL that points to your application's source code\.
+ A README\.md file\. This file should describe how customers can use your application, and how to configure it before deploying it in their own AWS accounts\. 
+ A LICENSE\.txt file \(required to share your application publicly\)\.
+ A valid Amazon S3 bucket policy that grants the service read permissions for artifacts uploaded to Amazon S3 when you packaged your application\. To do this, follow these steps:

  1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

  1. Choose the Amazon S3 bucket that you used to package your application\.

  1. Choose the **Permissions** tab\.

  1. Choose the **Bucket Policy** button\.

  1. Paste the following policy statement into the **Bucket policy editor**\. Make sure to substitute your bucket name in the Resource property value\.

     ```
      1. {
      2.     "Version": "2012-10-17",
      3.     "Statement": [
      4.         {
      5.             "Effect": "Allow",
      6.             "Principal": {
      7.                 "Service":  "serverlessrepo.amazonaws.com"
      8.             },
      9.             "Action": "s3:GetObject",
     10.             "Resource": "arn:aws:s3:::<your-bucket-name>/*"
     11.         }
     12.     ]
     13. }
     ```

  1. Choose the **Save** button\.

## Step 1: Add a Metadata Section to the AWS SAM Template<a name="serverless-sam-template-publishing-applications-step1"></a>

First add a `Metadata` section to your AWS SAM template\. Provide the application information to be published to the AWS Serverless Application Repository\.

The following is an example `Metadata` section:

```
Metadata:
  AWS::ServerlessRepo::Application:
    Name: my-app
    Description: hello world
    Author: user1
    SpdxLicenseId: Apache-2.0
    LicenseUrl: LICENSE.txt
    ReadmeUrl: README.md
    Labels: ['tests']
    HomePageUrl: https://github.com/user1/my-app-project
    SemanticVersion: 0.0.1
    SourceCodeUrl: https://github.com/user1/my-app-project

Resources:
  HelloWorldFunction:
    Type: AWS::Lambda::Function
      Properties:
        ...
        CodeUri: source-code1
        ...
```

For more information about the properties of the `Metadata` section in the AWS SAM template, see [AWS SAM Template Metadata Section Properties](serverless-sam-template-publishing-applications-metadata-properties.md)\.

## Step 2: Package the Application<a name="serverless-sam-template-publishing-applications-step2"></a>

Execute the following AWS SAM CLI command:

```
sam-app> sam package \
    --template-file template.yaml \
    --output-template-file packaged.yaml \
    --s3-bucket <your-bucket-name>
```

The command uploads the application artifacts to Amazon S3 and outputs a new template file called `packaged.yaml`\. You use this file in the next step to publish the application to the AWS Serverless Application Repository\. The `packaged.yaml` template file is similar to the original template file \(`template.yaml`\), but has a key difference—the `CodeUri`, `LicenseUrl`, and `ReadmeUrl` properties point to the Amazon S3 bucket and objects that contain the respective artifacts\.

The following snippet from an example `packaged.yaml` template file shows the `CodeUri` property: 

```
MySampleFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: s3://bucketname/fbd77a3647a4f47a352fcObjectGUID

...
```

## Step 3: Publish the Application<a name="serverless-sam-template-publishing-applications-step3"></a>

Execute the following AWS SAM CLI command:

```
sam-app> sam publish \
    --template packaged.yaml \
    --region us-east-1
```

The output of the `sam publish` command includes a link to the AWS Serverless Application Repository directly to your application\. You can also go to the AWS Serverless Application Repository landing page directly and search for your application\.

Your application is set to private by default, so it isn't visible to other AWS accounts\. In order to share your application with others, you must either make it public or grant permission to a specific list of AWS accounts\. For information on sharing your application by using the AWS CLI, see [Using Resource\-based Policies for the AWS Serverless Application Repository](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/access-control-resource-based.html)\. For information on sharing your application using the console, see [Sharing an Application Through the Console](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/serverlessrepo-how-to-publish.html#share-application)\.

## Additional Topics<a name="serverless-sam-template-publishing-applications-additional-topics"></a>
+ [AWS SAM Template Metadata Section Properties](serverless-sam-template-publishing-applications-metadata-properties.md)