# SQS<a name="sam-property-function-sqs"></a>

The object describing an `SQS` event source type\.

SAM generates [AWS::Lambda::EventSourceMapping](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html) resource when this event type is set

## Syntax<a name="sam-property-function-sqs-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-sqs-syntax.yaml"></a>

```
  [BatchSize](#sam-function-sqs-batchsize): Integer
  [Enabled](#sam-function-sqs-enabled): Boolean
  [Queue](#sam-function-sqs-queue): String
```

## Properties<a name="sam-property-function-sqs-properties"></a>

 `BatchSize`   <a name="sam-function-sqs-batchsize"></a>
The maximum number of items to retrieve in a single batch\.  
*Type*: Integer  
*Required*: No  
*Default*: 10  
*AWS CloudFormation compatibility*: This property is passed directly to the `[BatchSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-batchsize)` property of an `AWS::Lambda::EventSourceMapping` resource\.  
*Minimum*: `1`  
*Maximum*: `10`

 `Enabled`   <a name="sam-function-sqs-enabled"></a>
Disables the event source mapping to pause polling and invocation\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Enabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-enabled)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Queue`   <a name="sam-function-sqs-queue"></a>
The ARN of the queue\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventSourceArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-eventsourcearn)` property of an `AWS::Lambda::EventSourceMapping` resource\.

## Examples<a name="sam-property-function-sqs--examples"></a>

### SQS Event<a name="sam-property-function-sqs--examples--sqs-event"></a>

SQS Event

#### YAML<a name="sam-property-function-sqs--examples--sqs-event--yaml"></a>

```
Events:
  SQSEvent:
    Type: SQS
    Properties:
      Queue: arn:aws:sqs:us-west-2:012345678901:my-queue
      BatchSize: 10
      Enabled: false
```