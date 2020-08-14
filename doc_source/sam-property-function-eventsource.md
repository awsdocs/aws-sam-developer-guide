# EventSource<a name="sam-property-function-eventsource"></a>

The object describing the source of events which trigger the function\. Each event consists of a type and a set of properties that depend on that type\. For more information about the properties of each event source, see the topic corresponding to that type\.

## Syntax<a name="sam-property-function-eventsource-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-eventsource-syntax.yaml"></a>

```
  [Properties](#sam-function-eventsource-properties): S3 | SNS | Kinesis | DynamoDB | SQS | Api | Schedule | CloudWatchEvent | EventBridgeRule | CloudWatchLogs | IoTRule | AlexaSkill | Cognito | HttpApi | MSK
  [Type](#sam-function-eventsource-type): String
```

## Properties<a name="sam-property-function-eventsource-properties"></a>

 `Properties`   <a name="sam-function-eventsource-properties"></a>
Object describing properties of this event mapping\. The set of properties must conform to the defined Type\.  
*Type*: [S3](sam-property-function-s3.md) \| [SNS](sam-property-function-sns.md) \| [Kinesis](sam-property-function-kinesis.md) \| [DynamoDB](sam-property-function-dynamodb.md) \| [SQS](sam-property-function-sqs.md) \| [Api](sam-property-function-api.md) \| [Schedule](sam-property-function-schedule.md) \| [CloudWatchEvent](sam-property-function-cloudwatchevent.md) \| [EventBridgeRule](sam-property-function-eventbridgerule.md) \| [CloudWatchLogs](sam-property-function-cloudwatchlogs.md) \| [IoTRule](sam-property-function-iotrule.md) \| [AlexaSkill](sam-property-function-alexaskill.md) \| [Cognito](sam-property-function-cognito.md) \| [HttpApi](sam-property-function-httpapi.md) \| [MSK](sam-property-function-msk.md)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Type`   <a name="sam-function-eventsource-type"></a>
The event type\.  
Supported values: `S3`, `SNS`, `Kinesis`, `DynamoDB`, `SQS`, `Api`, `Schedule`, `CloudWatchEvent`, `CloudWatchLogs`, `IoTRule`, `AlexaSkill`, `Cognito`, `EventBridgeRule`, `HttpApi`, `MSK`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-eventsource--examples"></a>

### API\-Event<a name="sam-property-function-eventsource--examples--api-event"></a>

Example of using an API Event

#### YAML<a name="sam-property-function-eventsource--examples--api-event--yaml"></a>

```
ApiEvent:
  Type: Api
  Properties:
    Method: get
    Path: /group/{user}
    RestApiId: 
      Ref: MyApi
```