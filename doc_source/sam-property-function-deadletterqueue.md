# DeadLetterQueue<a name="sam-property-function-deadletterqueue"></a>

Specifies an SQS queue or SNS topic that AWS Lambda \(Lambda\) sends events to when it can't process them\. For more information about dead letter queue functionality, see [AWS Lambda Function Dead Letter Queues](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html#dlq)\.

SAM will automatically add appropriate permission to your Lambda function execution role to give Lambda service access to the resource\. sqs:SendMessage will be added for SQS queues and sns:Publish for SNS topics\.

## Syntax<a name="sam-property-function-deadletterqueue-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-deadletterqueue-syntax.yaml"></a>

```
  [TargetArn](#sam-function-deadletterqueue-targetarn): String
  [Type](#sam-function-deadletterqueue-type): String
```

## Properties<a name="sam-property-function-deadletterqueue-properties"></a>

 `TargetArn`   <a name="sam-function-deadletterqueue-targetarn"></a>
The Amazon Resource Name \(ARN\) of an Amazon SQS queue or Amazon SNS topic\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[TargetArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-deadletterconfig.html#cfn-lambda-function-deadletterconfig-targetarn)` property of the `AWS::Lambda::Function` `DeadLetterConfig` data type\.

 `Type`   <a name="sam-function-deadletterqueue-type"></a>
The type of dead letter queue\.  
Supported values: `SNS`, `SQS`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-deadletterqueue--examples"></a>

### DeadLetterQueue<a name="sam-property-function-deadletterqueue--examples--deadletterqueue"></a>

Dead Letter Queue example for an SNS topic\.

#### YAML<a name="sam-property-function-deadletterqueue--examples--deadletterqueue--yaml"></a>

```
DeadLetterQueue:
  Type: SNS
  TargetArn: arn:aws:sns:us-east-2:123456789012:my-topic
```