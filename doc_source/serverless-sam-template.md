# Declaring Serverless Resources<a name="serverless-sam-template"></a>

AWS SAM defines the following resources that are specifically designed for serverless applications:

**Topics**
+ [AWS::Serverless::Api](#serverless-sam-template-api)
+ [AWS::Serverless::Application](#serverless-sam-template-application)
+ [AWS::Serverless::Function](#serverless-sam-template-function)
+ [AWS::Serverless::LayerVersion](#serverless-sam-template-layerversion)
+ [AWS::Serverless::SimpleTable](#serverless-sam-template-simpletable)

## AWS::Serverless::Api<a name="serverless-sam-template-api"></a>

This resource type describes an API Gateway resource\. It's useful for advanced use cases where you want full control and flexibility when you configure your APIs\. For most scenarios, we recommend that you create APIs by specifying this resource type as an event source of your `AWS::Serverless::Function` resource, as shown in the following example\.

```
AWS::Serverless::API
  Properties:
    StageName: prod
    DefinitionUri: swagger.yml
```

For a list of properties, see [AWS::Serverless::Api](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessapi) in the AWS SAM GitHub repository\.

## AWS::Serverless::Application<a name="serverless-sam-template-application"></a>

This resource type embeds a serverless application from the AWS Serverless Application Repository or from an Amazon S3 bucket as a nested application\. Nested applications are deployed as nested stacks, which can contain multiple other resources\. For more information about nested applications, see [Nested Applications](serverless-sam-template-nested-applications.md)\.

The following is an example of a nested application from the AWS Serverless Application Repository:

```
AWS::Serverless::Application
  Properties:
    Location:
      ApplicationId: arn:aws:serverlessrepo:region:account-id:applications/application-name
      SemanticVersion: 1.0.0
    Parameters:
      StringParameter: parameter-value
      IntegerParameter: 2
```

The following is an example of a nested application that's hosted in an Amazon S3 bucket\. In this example, *sam\-template\-object* is the name of a packaged AWS SAM template:

```
AWS::Serverless::Application
  Properties:
    Location: https://s3.region.amazonaws.com/bucket-name/sam-template-object
    Parameters:
      StringParameter: parameter-value
      IntegerParameter: 2
```

For a list of properties, see [AWS::Serverless::Application](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessapplication) in the AWS SAM GitHub repository\.

For details about how to obtain the required values of an application that you want to nest, see [Nested Applications](serverless-sam-template-nested-applications.md)\.

## AWS::Serverless::Function<a name="serverless-sam-template-function"></a>

This resource type describes configuration information for creating a Lambda function\. You can describe any event source that you want to attach to the Lambda function—such as Amazon S3, Amazon DynamoDB Streams, and Amazon Kinesis Data Streams\.

The following is an example of a serverless function:

```
AWS::Serverless::Function
  Handler: index.js
  Runtime: nodejs8.10
  CodeUri: 's3://my-code-bucket/my-function.zip'
  Description: Creates thumbnails of uploaded images
  MemorySize: 1024
  Timeout: 15
  Policies:
   - AWSLambdaExecute # Managed Policy
   - Version: '2012-10-17' # Policy Document
     Statement:
       - Effect: Allow
         Action:
           - s3:GetObject
           - s3:GetObjectACL
         Resource: 'arn:aws:s3:::my-bucket/*'
  Environment:
    Variables:
      TABLE_NAME: my-table
  Events:
    PhotoUpload:
      Type: S3
      Properties:
        Bucket: my-photo-bucket
  Tags:
    AppNameTag: ThumbnailApp
    DepartmentNameTag: ThumbnailDepartment
```

For a list of properties, see [AWS::Serverless::Function](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessfunction) in the AWS SAM GitHub repository\.

## AWS::Serverless::LayerVersion<a name="serverless-sam-template-layerversion"></a>

This resource type creates a Lambda layer version \(LayerVersion\) that contains library or runtime code that's needed by a Lambda function\. When a serverless layer version is transformed, AWS SAM also transforms the logical ID of the resource so that old layer versions aren't automatically deleted by AWS CloudFormation when the resource is updated\.

The following is an example of a layer version:

```
AWS::Serverless::LayerVersion
  Properties:
    LayerName: MyLayer
    Description: Layer description
    ContentUri: 's3://my-bucket/my-layer.zip'
    CompatibleRuntimes:
      - nodejs8.10
      - nodejs8.10
    LicenseInfo: 'Available under the MIT-0 license.'
    RetentionPolicy: Retain
```

For a list of properties, see [AWS::Serverless::LayerVersion](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlesslayerversion) in the AWS SAM GitHub repository\.

## AWS::Serverless::SimpleTable<a name="serverless-sam-template-simpletable"></a>

 This resource type provides simple syntax for describing how to create DynamoDB tables\. Here's an example:

```
AWS::Serverless::SimpleTable
  Properties:
    PrimaryKey:
      Name: id
      Type: String
    ProvisionedThroughput:
      ReadCapacityUnits: 5
      WriteCapacityUnits: 5
```

For a list of properties, see [AWS::Serverless::SimpleTable](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlesssimpletable) in the AWS SAM GitHub repository\.

For reference documentation for SAM template resources, see [AWS SAM Specification](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md) on GitHub\.