# Kinesis<a name="sam-property-function-kinesis"></a>

Kinesis event source configuration\.

SAM generates [AWS::Lambda::EventSourceMapping](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html) resource when this event type is set

## Syntax<a name="sam-property-function-kinesis-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-function-kinesis-syntax.yaml"></a>

```
  [BatchSize](#sam-function-kinesis-batchsize): Integer
  [Enabled](#sam-function-kinesis-enabled): Boolean
  [MaximumBatchingWindowInSeconds](#sam-function-kinesis-maximumbatchingwindowinseconds): Integer
  [StartingPosition](#sam-function-kinesis-startingposition): String
  [Stream](#sam-function-kinesis-stream): String
```

## Properties<a name="sam-property-function-kinesis-properties"></a>

 `BatchSize`   <a name="sam-function-kinesis-batchsize"></a>
The maximum number of items to retrieve in a single batch\.  
*Type*: Integer  
*Required*: No  
*Default*: 100  
*CloudFormation Compatibility*: This property is passed directly to the `[BatchSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-batchsize)` property of an `AWS::Lambda::EventSourceMapping`\.  
*Minimum*: `1`  
*Maximum*: `10000`

 `Enabled`   <a name="sam-function-kinesis-enabled"></a>
Disables the event source mapping to pause polling and invocation\.  
*Type*: Boolean  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[Enabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-enabled)` property of an `AWS::Lambda::EventSourceMapping`\.

 `MaximumBatchingWindowInSeconds`   <a name="sam-function-kinesis-maximumbatchingwindowinseconds"></a>
The maximum amount of time to gather records before invoking the function, in seconds\.  
*Type*: Integer  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[MaximumBatchingWindowInSeconds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumbatchingwindowinseconds)` property of an `AWS::Lambda::EventSourceMapping`\.

 `StartingPosition`   <a name="sam-function-kinesis-startingposition"></a>
The position in a stream from which to start reading\.  
Supported values: `TRIM_HORIZON`, `LATEST`, `AT_TIMESTAMP`\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is passed directly to the `[StartingPosition](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-startingposition)` property of an `AWS::Lambda::EventSourceMapping`\.

 `Stream`   <a name="sam-function-kinesis-stream"></a>
The ARN of the data stream or a stream consumer\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is passed directly to the `[EventSourceArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-eventsourcearn)` property of an `AWS::Lambda::EventSourceMapping`\.

## Examples<a name="sam-property-function-kinesis--examples"></a>

### Kinesis Event Source<a name="sam-property-function-kinesis--examples--kinesis-event-source"></a>

Kinesis Event Source

#### YAML<a name="sam-property-function-kinesis--examples--kinesis-event-source--yaml"></a>

```
Properties:
  BatchSize: 10
  Enabled: false
  StartingPosition: TRIM_HORIZON
  Stream: arn:aws:kinesis:us-east-1:123456789012:stream/my-stream
```