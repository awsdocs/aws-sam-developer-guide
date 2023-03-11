# EventSource<a name="sam-property-function-eventsource"></a>

The object describing the source of events which trigger the function\. Each event consists of a type and a set of properties that depend on that type\. For more information about the properties of each event source, see the topic corresponding to that type\.

## Syntax<a name="sam-property-function-eventsource-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-eventsource-syntax.yaml"></a>

```
  [Properties](#sam-function-eventsource-properties): AlexaSkill | Api | CloudWatchEvent | CloudWatchLogs | Cognito | DocumentDB | DynamoDB | EventBridgeRule | HttpApi | IoTRule | Kinesis | MQ | MSK | S3 | Schedule | ScheduleV2 | SelfManagedKafka | SNS | SQS
  [Type](#sam-function-eventsource-type): String
```

## Properties<a name="sam-property-function-eventsource-properties"></a>

 `Properties`   <a name="sam-function-eventsource-properties"></a>
Object describing properties of this event mapping\. The set of properties must conform to the defined Type\.  
*Type*: [AlexaSkill](sam-property-function-alexaskill.md) \| [Api](sam-property-function-api.md) \| [CloudWatchEvent](sam-property-function-cloudwatchevent.md) \| [CloudWatchLogs](sam-property-function-cloudwatchlogs.md) \| [Cognito](sam-property-function-cognito.md) \| [DocumentDB](sam-property-function-documentdb.md) \| [DynamoDB](sam-property-function-dynamodb.md) \| [EventBridgeRule](sam-property-function-eventbridgerule.md) \| [HttpApi](sam-property-function-httpapi.md) \| [IoTRule](sam-property-function-iotrule.md) \| [Kinesis](sam-property-function-kinesis.md) \| [MQ](sam-property-function-mq.md) \| [MSK](sam-property-function-msk.md) \| [S3](sam-property-function-s3.md) \| [Schedule](sam-property-function-schedule.md) \| [ScheduleV2](sam-property-function-schedulev2.md) \| [SelfManagedKafka](sam-property-function-selfmanagedkafka.md) \| [SNS](sam-property-function-sns.md) \| [SQS](sam-property-function-sqs.md)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Type`   <a name="sam-function-eventsource-type"></a>
The event type\.  
*Valid values*: `AlexaSkill`, `Api`, `CloudWatchEvent`, `CloudWatchLogs`, `Cognito`, `DocumentDB`, `DynamoDB`, `EventBridgeRule`, `HttpApi`, `IoTRule`, `Kinesis`, `MQ`, `MSK`, `S3`, `Schedule`, `ScheduleV2`, `SelfManagedKafka`, `SNS`, `SQS`  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-eventsource--examples"></a>

### APIEvent<a name="sam-property-function-eventsource--examples--apievent"></a>

Example of using an API event

#### YAML<a name="sam-property-function-eventsource--examples--apievent--yaml"></a>

```
ApiEvent:
  Type: Api
  Properties:
    Method: get
    Path: /group/{user}
    RestApiId: 
      Ref: MyApi
```