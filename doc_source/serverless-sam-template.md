# Declaring Serverless Resources<a name="serverless-sam-template"></a>

AWS SAM defines three types of resources that are specifically designed for serverless applications:

**Topics**
+ [AWS::Serverless::Function](#serverless-sam-template-function)
+ [AWS::Serverless::Api](#serverless-sam-template-api)
+ [AWS::Serverless::SimpleTable](#serverless-sam-template-simpletable)

## AWS::Serverless::Function<a name="serverless-sam-template-function"></a>

This resource type describes configuration information for creating a Lambda function\. You can describe any event source that you want to attach to the Lambda function—such as Amazon S3, Amazon DynamoDB Streams, and Amazon Kinesis Data Streams\.

The following is an example of a serverless function:

```
AWS::Serverless::Function
  Handler: index.js
  Runtime: nodejs6.10
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

For a list of properties, see [AWS::Serverless::Function](https://github.com/awslabs/serverless-application-model/blob/develop/versions/2016-10-31.md#awsserverlessfunction) in the AWS SAM GitHub repository\.

## AWS::Serverless::Api<a name="serverless-sam-template-api"></a>

This resource type describes an API Gateway resource\. It's useful for advanced use cases where you want full control and flexibility when you configure your APIs\. For most scenarios, we recommend that you create APIs by specifying this resource type as an event source of your `AWS::Serverless::Function` resource, as shown in the preceding example\.

```
AWS::Serverless::API
  Properties:
    StageName: prod
    DefinitionUri: swagger.yml
```

For a list of properties, see [AWS::Serverless::Api](https://github.com/awslabs/serverless-application-model/blob/develop/versions/2016-10-31.md#awsserverlessapi) in the AWS SAM GitHub repository\.

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

For a list of properties, see [AWS::Serverless::SimpleTable](https://github.com/awslabs/serverless-application-model/blob/develop/versions/2016-10-31.md#awsserverlesssimpletable) in the AWS SAM GitHub repository\.

For reference documentation for SAM template resources, see [AWS SAM Specification](https://github.com/awslabs/serverless-application-model/blob/develop/versions/2016-10-31.md) on GitHub\.