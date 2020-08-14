# Kinesis<a name="sam-property-function-kinesis"></a>

The object describing a `Kinesis` event source type\.

AWS SAM generates an [AWS::Lambda::EventSourceMapping](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html) resource when this event type is set\.

## Syntax<a name="sam-property-function-kinesis-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-kinesis-syntax.yaml"></a>

```
  [BatchSize](#sam-function-kinesis-batchsize): Integer
  [BisectBatchOnFunctionError](#sam-function-kinesis-bisectbatchonfunctionerror): Boolean
  [DestinationConfig](#sam-function-kinesis-destinationconfig): [DestinationConfig](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-destinationconfig)
  [Enabled](#sam-function-kinesis-enabled): Boolean
  [MaximumBatchingWindowInSeconds](#sam-function-kinesis-maximumbatchingwindowinseconds): Integer
  [MaximumRecordAgeInSeconds](#sam-function-kinesis-maximumrecordageinseconds): Integer
  [MaximumRetryAttempts](#sam-function-kinesis-maximumretryattempts): Integer
  [ParallelizationFactor](#sam-function-kinesis-parallelizationfactor): Integer
  [StartingPosition](#sam-function-kinesis-startingposition): String
  [Stream](#sam-function-kinesis-stream): String
```

## Properties<a name="sam-property-function-kinesis-properties"></a>

 `BatchSize`   <a name="sam-function-kinesis-batchsize"></a>
The maximum number of items to retrieve in a single batch\.  
*Type*: Integer  
*Required*: No  
*Default*: 100  
*AWS CloudFormation compatibility*: This property is passed directly to the `[BatchSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-batchsize)` property of an `AWS::Lambda::EventSourceMapping` resource\.  
*Minimum*: `1`  
*Maximum*: `10000`

 `BisectBatchOnFunctionError`   <a name="sam-function-kinesis-bisectbatchonfunctionerror"></a>
If the function returns an error, split the batch in two and retry\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[BisectBatchOnFunctionError](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-bisectbatchonfunctionerror)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `DestinationConfig`   <a name="sam-function-kinesis-destinationconfig"></a>
An Amazon SQS queue or Amazon SNS topic destination for discarded records\.  
*Type*: [DestinationConfig](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-destinationconfig)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[DestinationConfig](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-destinationconfig)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Enabled`   <a name="sam-function-kinesis-enabled"></a>
Disables the event source mapping to pause polling and invocation\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Enabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-enabled)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `MaximumBatchingWindowInSeconds`   <a name="sam-function-kinesis-maximumbatchingwindowinseconds"></a>
The maximum amount of time to gather records before invoking the function, in seconds\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MaximumBatchingWindowInSeconds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumbatchingwindowinseconds)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `MaximumRecordAgeInSeconds`   <a name="sam-function-kinesis-maximumrecordageinseconds"></a>
The maximum age of a record that Lambda sends to a function for processing\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MaximumRecordAgeInSeconds](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumrecordageinseconds)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `MaximumRetryAttempts`   <a name="sam-function-kinesis-maximumretryattempts"></a>
The maximum number of times to retry when the function returns an error\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MaximumRetryAttempts](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumretryattempts)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `ParallelizationFactor`   <a name="sam-function-kinesis-parallelizationfactor"></a>
The number of batches to process from each shard concurrently\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ParallelizationFactor](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-parallelizationfactor)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `StartingPosition`   <a name="sam-function-kinesis-startingposition"></a>
The position in a stream from which to start reading\.  
Supported values: `TRIM_HORIZON`, `LATEST`, `AT_TIMESTAMP`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[StartingPosition](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-startingposition)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Stream`   <a name="sam-function-kinesis-stream"></a>
The ARN of the data stream or a stream consumer\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventSourceArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-eventsourcearn)` property of an `AWS::Lambda::EventSourceMapping` resource\.

## Examples<a name="sam-property-function-kinesis--examples"></a>

### Kinesis Event Source<a name="sam-property-function-kinesis--examples--kinesis-event-source"></a>

Kinesis Event Source

#### YAML<a name="sam-property-function-kinesis--examples--kinesis-event-source--yaml"></a>

```
Events:
  KinesisEvent:
    Type: Kinesis
    Properties:
      Stream: arn:aws:kinesis:us-east-1:123456789012:stream/my-stream
      StartingPosition: TRIM_HORIZON
      BatchSize: 10
      Enabled: false
```