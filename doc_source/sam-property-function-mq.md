# MQ<a name="sam-property-function-mq"></a>

The object describing an `MQ` event source type\. For more information, see [Using Lambda with Amazon MQ](https://docs.aws.amazon.com/lambda/latest/dg/with-mq.html) in the *AWS Lambda Developer Guide*\.

AWS SAM generates an [AWS::Lambda::EventSourceMapping](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html) resource when this event type is set\.

**Note:** To have an Amazon MQ queue in a virtual private cloud \(VPC\) but your Lambda function in a public network, your function's execution role must include the following permissions: `ec2:CreateNetworkInterface`, `ec2:DeleteNetworkInterface`, `ec2:DescribeNetworkInterfaces`, `ec2:DescribeSecurityGroups`, `ec2:DescribeSubnets`, `ec2:DescribeVpcs`\. For more information, see [Execution role permissions](https://docs.aws.amazon.com/lambda/latest/dg/with-mq.html#events-mq-permissions) in the *AWS Lambda Developer Guide*\.

## Syntax<a name="sam-property-function-mq-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-mq-syntax.yaml"></a>

```
  [BatchSize](#sam-function-mq-batchsize): Integer
  [Broker](#sam-function-mq-broker): String
  [Enabled](#sam-function-mq-enabled): Boolean
  [Queues](#sam-function-mq-queues): List
  [SecretsManagerKmsKeyId](#sam-function-mq-secretsmanagerkmskeyid): String
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
If true, the event source mapping is active\. To pause polling and invocation, set to `false`\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Enabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-enabled)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Queues`   <a name="sam-function-mq-queues"></a>
The name of the Amazon MQ broker destination queue to consume\.  
*Type*: List  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Queues](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-queues)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `SecretsManagerKmsKeyId`   <a name="sam-function-mq-secretsmanagerkmskeyid"></a>
The AWS Key Management Service \(AWS KMS\) key ID of a customer managed key from AWS Secrets Manager\. This property is required if you use a customer managed key from Secrets Manager, but your Lambda execution role doesn't include the `kms:Decrypt` permission\.  
The value of this property is a UUID\. For example: `1abc23d4-567f-8ab9-cde0-1fab234c5d67`\.  
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `SourceAccessConfigurations`   <a name="sam-function-mq-sourceaccessconfigurations"></a>
The Secrets Manager secret that stores your broker credentials\. Specify secrets using the [SourceAccessConfigurations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-sourceaccessconfiguration.html) data type\.  
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
      Enabled: true
```