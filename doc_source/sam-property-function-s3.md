# S3<a name="sam-property-function-s3"></a>

The object describing an `S3` event source type\.

## Syntax<a name="sam-property-function-s3-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-s3-syntax.yaml"></a>

```
  [Bucket](#sam-function-s3-bucket): String
  [Events](#sam-function-s3-events): String | List
  [Filter](#sam-function-s3-filter): [NotificationFilter](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket-notificationconfiguration-config-filter.html)
```

## Properties<a name="sam-property-function-s3-properties"></a>

 `Bucket`   <a name="sam-function-s3-bucket"></a>
S3 bucket name\. This bucket must exist in the same template\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is similar to the `[BucketName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket.html#cfn-s3-bucket-name)` property of an `AWS::S3::Bucket` resource\. This is a required field in SAM\. This field only accepts a reference to the S3 bucket created in this template

 `Events`   <a name="sam-function-s3-events"></a>
The Amazon S3 bucket event for which to invoke the AWS Lambda function\. See [Amazon S3 supported event types](http://docs.aws.amazon.com/AmazonS3/latest/dev/NotificationHowTo.html#supported-notification-event-types) for a list of valid values\.  
*Type*: String \| List  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Event](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket-notificationconfig-lambdaconfig.html#cfn-s3-bucket-notificationconfig-lambdaconfig-event)` property of the `AWS::S3::Bucket` `LambdaConfiguration` data type\.

 `Filter`   <a name="sam-function-s3-filter"></a>
The filtering rules that determine which Amazon S3 objects invoke the Lambda function\. For information about Amazon S3 key name filtering, see [Configuring Amazon S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/dev/NotificationHowTo.html) in the Amazon Simple Storage Service Developer Guide\.  
*Type*: [NotificationFilter](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket-notificationconfiguration-config-filter.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Filter](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket-notificationconfiguration-config-filter.html)` property of the `AWS::S3::Bucket` `LambdaConfiguration` data type\.

## Examples<a name="sam-property-function-s3--examples"></a>

### S3\-Event<a name="sam-property-function-s3--examples--s3-event"></a>

Example of an S3 Event\.

#### YAML<a name="sam-property-function-s3--examples--s3-event--yaml"></a>

```
Events:
  S3Event:
    Type: S3
    Properties:
      Bucket:
        Ref: ImagesBucket     # This must be the name of an S3 bucket declared in the same template file
      Events: s3:ObjectCreated:*
      Filter:
        S3Key:
          Rules:
          - Name: prefix      # or "suffix"
            Value: value      # The value to search for in the S3 object key names
```