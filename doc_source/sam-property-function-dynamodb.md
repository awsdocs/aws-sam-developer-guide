# DynamoDB<a name="sam-property-function-dynamodb"></a>

DynamoDB streaming event source type\.

SAM generates [AWS::Lambda::EventSourceMapping](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html) resource when this event type is set

## Syntax<a name="sam-property-function-dynamodb-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-function-dynamodb-syntax.yaml"></a>

```
  [BatchSize](#sam-function-dynamodb-batchsize): Integer
  [BisectBatchOnFunctionError](#sam-function-dynamodb-bisectbatchonfunctionerror): Boolean
  [DestinationConfig](#sam-function-dynamodb-destinationconfig): [DestinationConfig](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-destinationconfig)
  [Enabled](#sam-function-dynamodb-enabled): Boolean
  [MaximumBatchingWindowInSeconds](#sam-function-dynamodb-maximumbatchingwindowinseconds): Integer
  [MaximumRecordAgeInSeconds](#sam-function-dynamodb-maximumrecordageinseconds): Integer
  [MaximumRetryAttempts](#sam-function-dynamodb-maximumretryattempts): Integer
  [ParallelizationFactor](#sam-function-dynamodb-parallelizationfactor): Integer
  [StartingPosition](#sam-function-dynamodb-startingposition): String
  [Stream](#sam-function-dynamodb-stream): String
```

## Properties<a name="sam-property-function-dynamodb-properties"></a>

 `BatchSize`   <a name="sam-function-dynamodb-batchsize"></a>
The maximum number of items to retrieve in a single batch\.  
*Type*: Integer  
*Required*: No  
*Default*: 100  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[BatchSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-batchsize)` property of an `AWS::Lambda::EventSourceMapping`\.  
*Minimum*: `1`  
*Maximum*: `1000`

 `BisectBatchOnFunctionError`   <a name="sam-function-dynamodb-bisectbatchonfunctionerror"></a>
If the function returns an error, split the batch in two and retry\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[BisectBatchOnFunctionError](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-bisectbatchonfunctionerror)` property of an `AWS::Lambda::EventSourceMapping`\.

 `DestinationConfig`   <a name="sam-function-dynamodb-destinationconfig"></a>
An Amazon SQS queue or Amazon SNS topic destination for discarded records\.  
*Type*: [DestinationConfig](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-destinationconfig)  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[DestinationConfig](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-destinationconfig)` property of an `AWS::Lambda::EventSourceMapping`\.

 `Enabled`   <a name="sam-function-dynamodb-enabled"></a>
Disables the event source mapping to pause polling and invocation\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[Enabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-enabled)` property of an `AWS::Lambda::EventSourceMapping`\.

 `MaximumBatchingWindowInSeconds`   <a name="sam-function-dynamodb-maximumbatchingwindowinseconds"></a>
The maximum amount of time to gather records before invoking the function, in seconds\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[MaximumBatchingWindowInSeconds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumbatchingwindowinseconds)` property of an `AWS::Lambda::EventSourceMapping`\.

 `MaximumRecordAgeInSeconds`   <a name="sam-function-dynamodb-maximumrecordageinseconds"></a>
The maximum age of a record that Lambda sends to a function for processing\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[MaximumRecordAgeInSeconds](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumrecordageinseconds)` property of an `AWS::Lambda::EventSourceMapping`\.

 `MaximumRetryAttempts`   <a name="sam-function-dynamodb-maximumretryattempts"></a>
The maximum number of times to retry when the function returns an error\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[MaximumRetryAttempts](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumretryattempts)` property of an `AWS::Lambda::EventSourceMapping`\.

 `ParallelizationFactor`   <a name="sam-function-dynamodb-parallelizationfactor"></a>
The number of batches to process from each shard concurrently\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[ParallelizationFactor](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-parallelizationfactor)` property of an `AWS::Lambda::EventSourceMapping`\.

 `StartingPosition`   <a name="sam-function-dynamodb-startingposition"></a>
The position in a stream from which to start reading\.  
Supported values: `TRIM_HORIZON`, `LATEST`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[StartingPosition](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-startingposition)` property of an `AWS::Lambda::EventSourceMapping`\.

 `Stream`   <a name="sam-function-dynamodb-stream"></a>
ARN of the DynamoDB stream\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[EventSourceArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-eventsourcearn)` property of an `AWS::Lambda::EventSourceMapping`\.

## Examples<a name="sam-property-function-dynamodb--examples"></a>

### DynamoDB Event<a name="sam-property-function-dynamodb--examples--dynamodb-event"></a>

DynamoDB Event

#### YAML<a name="sam-property-function-dynamodb--examples--dynamodb-event--yaml"></a>

```
Properties:
  Stream: arn:aws:dynamodb:us-east-1:123456789012:table/TestTable/stream/2016-08-11T21:21:33.291
  StartingPosition: TRIM_HORIZON
  BatchSize: 10
  Enabled: false
```