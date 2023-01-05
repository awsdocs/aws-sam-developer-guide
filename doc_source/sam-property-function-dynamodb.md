# DynamoDB<a name="sam-property-function-dynamodb"></a>

The object describing a `DynamoDB` event source type\. For more information, see [Using AWS Lambda with Amazon DynamoDB](https://docs.aws.amazon.com/lambda/latest/dg/with-ddb.html) in the *AWS Lambda Developer Guide*\.

AWS SAM generates an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html) resource when this event type is set\.

## Syntax<a name="sam-property-function-dynamodb-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-dynamodb-syntax.yaml"></a>

```
  [BatchSize](#sam-function-dynamodb-batchsize): Integer
  [BisectBatchOnFunctionError](#sam-function-dynamodb-bisectbatchonfunctionerror): Boolean
  [DestinationConfig](#sam-function-dynamodb-destinationconfig): [DestinationConfig](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-destinationconfig)
  [Enabled](#sam-function-dynamodb-enabled): Boolean
  [FilterCriteria](#sam-function-dynamodb-filtercriteria): [FilterCriteria](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html)
  [FunctionResponseTypes](#sam-function-dynamodb-functionresponsetypes): List
  [MaximumBatchingWindowInSeconds](#sam-function-dynamodb-maximumbatchingwindowinseconds): Integer
  [MaximumRecordAgeInSeconds](#sam-function-dynamodb-maximumrecordageinseconds): Integer
  [MaximumRetryAttempts](#sam-function-dynamodb-maximumretryattempts): Integer
  [ParallelizationFactor](#sam-function-dynamodb-parallelizationfactor): Integer
  [StartingPosition](#sam-function-dynamodb-startingposition): String
  [Stream](#sam-function-dynamodb-stream): String
  [TumblingWindowInSeconds](#sam-function-dynamodb-tumblingwindowinseconds): Integer
```

## Properties<a name="sam-property-function-dynamodb-properties"></a>

 `BatchSize`   <a name="sam-function-dynamodb-batchsize"></a>
The maximum number of items to retrieve in a single batch\.  
*Type*: Integer  
*Required*: No  
*Default*: 100  
*AWS CloudFormation compatibility*: This property is passed directly to the `[BatchSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-batchsize)` property of an `AWS::Lambda::EventSourceMapping` resource\.  
*Minimum*: `1`  
*Maximum*: `1000`

 `BisectBatchOnFunctionError`   <a name="sam-function-dynamodb-bisectbatchonfunctionerror"></a>
If the function returns an error, split the batch in two and retry\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[BisectBatchOnFunctionError](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-bisectbatchonfunctionerror)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `DestinationConfig`   <a name="sam-function-dynamodb-destinationconfig"></a>
An Amazon Simple Queue Service \(Amazon SQS\) queue or Amazon Simple Notification Service \(Amazon SNS\) topic destination for discarded records\.  
*Type*: [DestinationConfig](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-destinationconfig)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[DestinationConfig](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-destinationconfig)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Enabled`   <a name="sam-function-dynamodb-enabled"></a>
Disables the event source mapping to pause polling and invocation\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Enabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-enabled)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `FilterCriteria`   <a name="sam-function-dynamodb-filtercriteria"></a>
A object that defines the criteria to determine whether Lambda should process an event\. For more information, see [AWS Lambda event filtering](https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventfiltering.html) in the *AWS Lambda Developer Guide*\.  
*Type*: [FilterCriteria](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[FilterCriteria](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `FunctionResponseTypes`   <a name="sam-function-dynamodb-functionresponsetypes"></a>
A list of the response types currently applied to the event source mapping\. For more information, see [Reporting batch item failures](https://docs.aws.amazon.com/lambda/latest/dg/with-ddb.html#services-ddb-batchfailurereporting) in the *AWS Lambda Developer Guide*\.  
*Valid values*: `ReportBatchItemFailures`  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[FunctionResponseTypes](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-functionresponsetypes)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `MaximumBatchingWindowInSeconds`   <a name="sam-function-dynamodb-maximumbatchingwindowinseconds"></a>
The maximum amount of time to gather records before invoking the function, in seconds\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MaximumBatchingWindowInSeconds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumbatchingwindowinseconds)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `MaximumRecordAgeInSeconds`   <a name="sam-function-dynamodb-maximumrecordageinseconds"></a>
The maximum age of a record that Lambda sends to a function for processing\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MaximumRecordAgeInSeconds](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumrecordageinseconds)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `MaximumRetryAttempts`   <a name="sam-function-dynamodb-maximumretryattempts"></a>
The maximum number of times to retry when the function returns an error\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MaximumRetryAttempts](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumretryattempts)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `ParallelizationFactor`   <a name="sam-function-dynamodb-parallelizationfactor"></a>
The number of batches to process from each shard concurrently\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ParallelizationFactor](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-parallelizationfactor)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `StartingPosition`   <a name="sam-function-dynamodb-startingposition"></a>
The position in a stream from which to start reading\.  
*Valid values*: `TRIM_HORIZON` or `LATEST`  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[StartingPosition](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-startingposition)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Stream`   <a name="sam-function-dynamodb-stream"></a>
The Amazon Resource Name \(ARN\) of the DynamoDB stream\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventSourceArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-eventsourcearn)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `TumblingWindowInSeconds`   <a name="sam-function-dynamodb-tumblingwindowinseconds"></a>
The duration, in seconds, of a processing window\. The valid range is 1 to 900 \(15 minutes\)\.  
For more information, see [Tumbling windows](https://docs.aws.amazon.com/lambda/latest/dg/with-ddb.html#streams-tumbling) in the *AWS Lambda Developer Guide*\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[TumblingWindowInSeconds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-tumblingwindowinseconds)` property of an `AWS::Lambda::EventSourceMapping` resource\.

## Examples<a name="sam-property-function-dynamodb--examples"></a>

### DynamoDB event source for existing DynamoDB table<a name="sam-property-function-dynamodb--examples--dynamodb-event-source-for-existing-dynamodb-table"></a>

DynamoDB event source for a DynamoDB table that already exists in an AWS account\.

#### YAML<a name="sam-property-function-dynamodb--examples--dynamodb-event-source-for-existing-dynamodb-table--yaml"></a>

```
Events:
  DDBEvent:
    Type: DynamoDB
    Properties:
      Stream: arn:aws:dynamodb:us-east-1:123456789012:table/TestTable/stream/2016-08-11T21:21:33.291
      StartingPosition: TRIM_HORIZON
      BatchSize: 10
      Enabled: false
```

### DynamoDB Event for DynamoDB Table Declared in Template<a name="sam-property-function-dynamodb--examples--dynamodb-event-for-dynamodb-table-declared-in-template"></a>

DynamoDB Event for a DynamoDB table that is declared in the same template file\.

#### YAML<a name="sam-property-function-dynamodb--examples--dynamodb-event-for-dynamodb-table-declared-in-template--yaml"></a>

```
Events:
  DDBEvent:
    Type: DynamoDB
    Properties:
      Stream: 
        !GetAtt MyDynamoDBTable.StreamArn   # This must be the name of a DynamoDB table declared in the same template file
      StartingPosition: TRIM_HORIZON
      BatchSize: 10
      Enabled: false
```