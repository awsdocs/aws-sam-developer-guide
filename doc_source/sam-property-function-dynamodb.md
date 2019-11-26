# DynamoDB<a name="sam-property-function-dynamodb"></a>

DynamoDB streaming event source type\.

SAM generates [AWS::Lambda::EventSourceMapping](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html) resource when this event type is set

## Syntax<a name="sam-property-function-dynamodb-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-function-dynamodb-syntax.yaml"></a>

```
  [BatchSize](#sam-function-dynamodb-batchsize): Integer
  [Enabled](#sam-function-dynamodb-enabled): Boolean
  [MaximumBatchingWindowInSeconds](#sam-function-dynamodb-maximumbatchingwindowinseconds): Integer
  [StartingPosition](#sam-function-dynamodb-startingposition): String
  [Stream](#sam-function-dynamodb-stream): String
```

## Properties<a name="sam-property-function-dynamodb-properties"></a>

 `BatchSize`   <a name="sam-function-dynamodb-batchsize"></a>
The maximum number of items to retrieve in a single batch\.  
*Type*: Integer  
*Required*: No  
*Default*: 100  
*CloudFormation Compatibility*: This property is passed directly to the `[BatchSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-batchsize)` property of an `AWS::Lambda::EventSourceMapping`\.  
*Minimum*: `1`  
*Maximum*: `1000`

 `Enabled`   <a name="sam-function-dynamodb-enabled"></a>
Disables the event source mapping to pause polling and invocation\.  
*Type*: Boolean  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[Enabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-enabled)` property of an `AWS::Lambda::EventSourceMapping`\.

 `MaximumBatchingWindowInSeconds`   <a name="sam-function-dynamodb-maximumbatchingwindowinseconds"></a>
The maximum amount of time to gather records before invoking the function, in seconds\.  
*Type*: Integer  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[MaximumBatchingWindowInSeconds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumbatchingwindowinseconds)` property of an `AWS::Lambda::EventSourceMapping`\.

 `StartingPosition`   <a name="sam-function-dynamodb-startingposition"></a>
The position in a stream from which to start reading\.  
Supported values: `TRIM_HORIZON`, `LATEST`\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is passed directly to the `[StartingPosition](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-startingposition)` property of an `AWS::Lambda::EventSourceMapping`\.

 `Stream`   <a name="sam-function-dynamodb-stream"></a>
ARN of the DynamoDB stream\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is passed directly to the `[EventSourceArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-eventsourcearn)` property of an `AWS::Lambda::EventSourceMapping`\.

## Examples<a name="sam-property-function-dynamodb--examples"></a>

### DynamoDB Event<a name="sam-property-function-dynamodb--examples--dynamodb-event"></a>

DynamoDB Event

#### YAML<a name="sam-property-function-dynamodb--examples--dynamodb-event--yaml"></a>

```
Properties:
  BatchSize: 10
  Enabled: false
  StartingPosition: TRIM_HORIZON
  Stream: arn:aws:dynamodb:us-east-1:123456789012:table/TestTable/stream/2016-08-11T21:21:33.291
```