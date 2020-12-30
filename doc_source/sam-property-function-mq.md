# MQ<a name="sam-property-function-mq"></a>

The object describing an `MQ` event source type\.

AWS SAM generates an [AWS::Lambda::EventSourceMapping](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html) resource when this event type is set\.

## Syntax<a name="sam-property-function-mq-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-mq-syntax.yaml"></a>

```
  [BatchSize](#sam-function-mq-batchsize): Integer
  [Broker](#sam-function-mq-broker): String
  [Enabled](#sam-function-mq-enabled): Boolean
  [Queues](#sam-function-mq-queues): List
  [SourceAccessConfigurations](#sam-function-mq-sourceaccessconfigurations): List
```

## Properties<a name="sam-property-function-mq-properties"></a>

 `BatchSize`   <a name="sam-function-mq-batchsize"></a>
The maximum number of items to retrieve in a single batch\.  
*Type*: Integer  
*Required*: No  
*Default*: 100  
*AWS CloudFormation compatibility*: This property is passed directly to the `[BatchSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-batchsize)` property of an `AWS::Lambda::EventSourceMapping` resource\.  
*Minimum*: `1`  
*Maximum*: `10000`

 `Broker`   <a name="sam-function-mq-broker"></a>
The Amazon Resource Name \(ARN\) of the Amazon MQ broker\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventSourceArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-eventsourcearn)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Enabled`   <a name="sam-function-mq-enabled"></a>
If true, the event source mapping is active\. To pause polling polling and invocation, set to false\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Enabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-enabled)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Queues`   <a name="sam-function-mq-queues"></a>
The name of the Amazon MQ broker destination queue to consume\.  
*Type*: List  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Queues](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-queues)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `SourceAccessConfigurations`   <a name="sam-function-mq-sourceaccessconfigurations"></a>
The AWS Secrets Manager secret that stores your broker credentials\. Specify secrets using the [SourceAccessConfigurations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-sourceaccessconfiguration.html) data type\.  
*Type*: List  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[SourceAccessConfigurations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-sourceaccessconfigurations)` property of an `AWS::Lambda::EventSourceMapping` resource\.

## Examples<a name="sam-property-function-mq--examples"></a>

### Amazon MQ event source<a name="sam-property-function-mq--examples--amazon-mq-event-source"></a>

The following is an example of an `MQ` event source type for an Amazon MQ broker\.

#### YAML<a name="sam-property-function-mq--examples--amazon-mq-event-source--yaml"></a>

```
Events:
  MQEvent:
    Type: MQ
    Properties:
      Broker: arn:aws:mq:us-east-2:123456789012:broker:MyBroker:b-1234a5b6-78cd-901e-2fgh-3i45j6k178l9
      Queues: List of queues
      SourceAccessConfigurations:
        - Type: String
          URI: String
       BatchSize: 200
       Enabled: True
```