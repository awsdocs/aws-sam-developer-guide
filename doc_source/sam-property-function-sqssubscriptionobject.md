# SqsSubscriptionObject<a name="sam-property-function-sqssubscriptionobject"></a>

Specify an existing SQS queue option to SNS event

## Syntax<a name="sam-property-function-sqssubscriptionobject-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-sqssubscriptionobject-syntax.yaml"></a>

```
  [BatchSize](#sam-function-sqssubscriptionobject-batchsize): String
  [Enabled](#sam-function-sqssubscriptionobject-enabled): Boolean
  [QueueArn](#sam-function-sqssubscriptionobject-queuearn): String
  [QueuePolicyLogicalId](#sam-function-sqssubscriptionobject-queuepolicylogicalid): String
  [QueueUrl](#sam-function-sqssubscriptionobject-queueurl): String
```

## Properties<a name="sam-property-function-sqssubscriptionobject-properties"></a>

 `BatchSize`   <a name="sam-function-sqssubscriptionobject-batchsize"></a>
The maximum number of items to retrieve in a single batch for the SQS queue\.  
*Type*: String  
*Required*: No  
*Default*: 10  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Enabled`   <a name="sam-function-sqssubscriptionobject-enabled"></a>
Disables the SQS event source mapping to pause polling and invocation\.  
*Type*: Boolean  
*Required*: No  
*Default*: True  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `QueueArn`   <a name="sam-function-sqssubscriptionobject-queuearn"></a>
Specify an existing SQS queue arn\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `QueuePolicyLogicalId`   <a name="sam-function-sqssubscriptionobject-queuepolicylogicalid"></a>
Give a custom logicalId name for the [AWS::SQS::QueuePolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sqs-queuepolicy.html) resource\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `QueueUrl`   <a name="sam-function-sqssubscriptionobject-queueurl"></a>
Specify the queue URL associated with the `QueueArn` property\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-sqssubscriptionobject--examples"></a>

### Existing SQS for SNS event<a name="sam-property-function-sqssubscriptionobject--examples--existing-sqs-for-sns-event"></a>

Example to add existing SQS queue for subscibing to an SNS topic\.

#### YAML<a name="sam-property-function-sqssubscriptionobject--examples--existing-sqs-for-sns-event--yaml"></a>

```
QueuePolicyLogicalId: CustomQueuePolicyLogicalId
QueueArn:
  Fn::GetAtt: MyCustomQueue.Arn
QueueUrl:
  Ref: MyCustomQueue
BatchSize: 5
```