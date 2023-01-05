# Publishing serverless applications using the AWS SAM CLI<a name="serverless-sam-template-publishing-applications"></a>

To make your AWS SAM application available for others to find and deploy, you can use the AWS SAM CLI to publish it to the AWS Serverless Application Repository\. To publish your application using the AWS SAM CLI, you must define it using an AWS SAM template\. You also must have tested it locally or in the AWS Cloud\.

Follow the instructions in this topic to create a new application, create a new version of an existing application, or update the metadata of an existing application\. \(What you do depends on whether the application already exists in the AWS Serverless Application Repository, and whether any application metadata is changing\.\) For more information about application metadata, see [AWS SAM template Metadata section properties](serverless-sam-template-publishing-applications-metadata-properties.md)\.

## Prerequisites<a name="serverless-sam-template-publishing-applications-prerequisites"></a>

Before you publish an application to the AWS Serverless Application Repository using the AWS SAM CLI, you must have the following:
+ The AWS SAM CLI installed\. For more information, see [Installing the AWS SAM CLI](install-sam-cli.md)\. To determine whether the AWS SAM CLI is installed, run the following command:

  ```
  sam --version
  ```
+ A valid AWS SAM template\.
+ Your application code and dependencies that the AWS SAM template references\.
+ A semantic version, required only to share your application publicly\. This value can be as simple as 1\.0\.
+ A URL that points to your application's source code\.
+ A `README.md` file\. This file should describe how customers can use your application and how to configure it before deploying it in their own AWS accounts\.
+ A `LICENSE.txt` file, required only to share your application publicly\.
+ If your application contains any nested applications, you must have already published them to the AWS Serverless Application Repository\.
+ A valid Amazon Simple Storage Service \(Amazon S3\) bucket policy that grants the service read permissions for artifacts that you upload to Amazon S3 when you package your application\. To set up this policy, do the following:

  1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

  1. Choose the name of the Amazon S3 bucket that you used to package your application\.

  1. Choose **Permissions**\.

  1. On the **Permissions** tab, under **Bucket policy**, choose **Edit**\.

  1. On the **Edit bucket policy** page, paste the following policy statement into the **Policy** editor\. In the policy statement, make sure to use your bucket name in the `Resource` element and your AWS account ID in the `Condition` element\. The expression in the `Condition` element ensures that AWS Serverless Application Repository has permission to access only applications from the specified AWS account\. For more information about policy statements, see [IAM JSON policy elements reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html) in the *IAM User Guide*\.

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
     10.             "Resource": "arn:aws:s3:::<your-bucket-name>/*",
     11.             "Condition" : {
     12.                 "StringEquals": {
     13.                     "aws:SourceAccount": "123456789012"
     14.                 }
     15.             }
     16.         }
     17.     ]
     18. }
     ```

  1. Choose **Save changes**\.

## Publishing a new application<a name="serverless-sam-template-publishing-applications-new-app"></a>

### Step 1: Add a `Metadata` section to the AWS SAM template<a name="serverless-sam-template-publishing-applications-step1"></a>

First, add a `Metadata` section to your AWS SAM template\. Provide the application information to be published to the AWS Serverless Application Repository\.

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

For more information about the `Metadata` section of the AWS SAM template, see [AWS SAM template Metadata section properties](serverless-sam-template-publishing-applications-metadata-properties.md)\.

### Step 2: Package the application<a name="serverless-sam-template-publishing-applications-step2"></a>

Run the following AWS SAM CLI command, which uploads the application's artifacts to Amazon S3 and outputs a new template file called `packaged.yaml`:

```
sam package --output-template-file packaged.yaml --s3-bucket <your-bucket-name>
```

You use the `packaged.yaml` template file in the next step to publish the application to the AWS Serverless Application Repository\. This file is similar to the original template file \(`template.yaml`\), but it has a key difference—the `CodeUri`, `LicenseUrl`, and `ReadmeUrl` properties point to the Amazon S3 bucket and objects that contain the respective artifacts\.

The following snippet from an example `packaged.yaml` template file shows the `CodeUri` property:

```
MySampleFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: s3://bucketname/fbd77a3647a4f47a352fcObjectGUID

...
```

### Step 3: Publish the application<a name="serverless-sam-template-publishing-applications-step3"></a>

To publish a private version of your AWS SAM application to the AWS Serverless Application Repository, run the following AWS SAM CLI command:

```
sam publish --template packaged.yaml --region us-east-1
```

The output of the `sam publish` command includes a link to your application on the AWS Serverless Application Repository\. You can also go directly to the [AWS Serverless Application Repository landing page](https://serverlessrepo.aws.amazon.com/applications) and search for your application\.

### Step 4: Share the application \(optional\)<a name="serverless-sam-template-publishing-applications-step4"></a>

By default, your application is set to private, so it isn't visible to other AWS accounts\. To share your application with others, you must either make it public or grant permission to a specific list of AWS accounts\.

For information about sharing your application using the AWS CLI, see [AWS Serverless Application Repository Resource\-Based Policy Examples](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/security_iam_resource-based-policy-examples.html) in the *AWS Serverless Application Repository Developer Guide*\. For information on sharing your application using the AWS Management Console, see [Sharing an Application](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/serverlessrepo-how-to-publish.html#share-application) in the *AWS Serverless Application Repository Developer Guide*\.

## Publishing a new version of an existing application<a name="serverless-sam-template-publishing-applications-new-version"></a>

After you've published an application to the AWS Serverless Application Repository, you might want to publish a new version of it\. For example, you might have changed your Lambda function code or added a new component to your application architecture\.

To update an application that you've previously published, publish the application again using the same process detailed previously\. In the `Metadata` section of the AWS SAM template file, provide the same application name that you originally published it with, but include a new `SemanticVersion` value\.

For example, consider an application published with the name `SampleApp` and a `SemanticVersion` of `1.0.0`\. To update that application, the AWS SAM template must have the application name `SampleApp` and a `SemanticVersion` of `1.0.1` \(or anything other than `1.0.0`\)\.

## Additional topics<a name="serverless-sam-template-publishing-applications-additional-topics"></a>
+ [AWS SAM template Metadata section properties](serverless-sam-template-publishing-applications-metadata-properties.md)