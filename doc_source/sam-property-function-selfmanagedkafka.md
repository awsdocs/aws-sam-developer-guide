# SelfManagedKafka<a name="sam-property-function-selfmanagedkafka"></a>

The object describing a `SelfManagedKafka` event source type\. For more information, see [Using AWS Lambda with with self\-managed Apache Kafka](https://docs.aws.amazon.com/lambda/latest/dg/with-kafka.html) in the *AWS Lambda Developer Guide*\.

AWS Serverless Application Model \(AWS SAM\) generates an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html) resource when this event type is set\.

## Syntax<a name="sam-property-function-selfmanagedkafka-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax\.

### YAML<a name="sam-property-function-selfmanagedkafka-syntax.yaml"></a>

```
  [BatchSize](#sam-function-selfmanagedkafka-batchsize): Integer
  [ConsumerGroupId](#sam-function-selfmanagedkafka-consumergroupid): String
  [Enabled](#sam-function-selfmanagedkafka-enabled): Boolean
  [FilterCriteria](#sam-function-selfmanagedkafka-filtercriteria): [FilterCriteria](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html)
  [KafkaBootstrapServers](#sam-function-selfmanagedkafka-kafkabootstrapservers): List
  [SourceAccessConfigurations](#sam-function-selfmanagedkafka-sourceaccessconfigurations): [SourceAccessConfigurations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-sourceaccessconfigurations)
  [Topics](#sam-function-selfmanagedkafka-topics): List
```

## Properties<a name="sam-property-function-selfmanagedkafka-properties"></a>

 `BatchSize`   <a name="sam-function-selfmanagedkafka-batchsize"></a>
The maximum number of records in each batch that Lambda pulls from your stream and sends to your function\.  
*Type*: Integer  
*Required*: No  
*Default*: 100  
*AWS CloudFormation compatibility*: This property is passed directly to the `[BatchSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-batchsize)` property of an `AWS::Lambda::EventSourceMapping` resource\.  
*Minimum*: `1`  
*Maximum*: `10000`

 `ConsumerGroupId`   <a name="sam-function-selfmanagedkafka-consumergroupid"></a>
A string that configures how events will be read from Kafka topics\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[SelfManagedKafkaConfiguration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Enabled`   <a name="sam-function-selfmanagedkafka-enabled"></a>
Disables the event source mapping to pause polling and invocation\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Enabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-enabled)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `FilterCriteria`   <a name="sam-function-selfmanagedkafka-filtercriteria"></a>
A object that defines the criteria to determine whether Lambda should process an event\. For more information, see [AWS Lambda event filtering](https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventfiltering.html) in the *AWS Lambda Developer Guide*\.  
*Type*: [FilterCriteria](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[FilterCriteria](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `KafkaBootstrapServers`   <a name="sam-function-selfmanagedkafka-kafkabootstrapservers"></a>
The list of bootstrap servers for your Kafka brokers\. Include the port, for example `broker.example.com:xxxx`  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `SourceAccessConfigurations`   <a name="sam-function-selfmanagedkafka-sourceaccessconfigurations"></a>
An array of the authentication protocol, VPC components, or virtual host to secure and define your event source\.  
*Valid values*: `BASIC_AUTH | CLIENT_CERTIFICATE_TLS_AUTH | SASL_SCRAM_256_AUTH | SASL_SCRAM_512_AUTH | SERVER_ROOT_CA_CERTIFICATE`  
*Type*: List of [SourceAccessConfiguration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-sourceaccessconfiguration.html)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ SourceAccessConfigurations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-sourceaccessconfigurations)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Topics`   <a name="sam-function-selfmanagedkafka-topics"></a>
The name of the Kafka topic\.  
*Type*: List  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Topics](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-topics)` property of an `AWS::Lambda::EventSourceMapping` resource\.

## Examples<a name="sam-property-function-selfmanagedkafka--examples"></a>

### Self\-managed Kafka event source<a name="sam-property-function-selfmanagedkafka--examples--self-managed-kafka-event-source"></a>

The following is an example of a `SelfManagedKafka` event source type\.

#### YAML<a name="sam-property-function-selfmanagedkafka--examples--self-managed-kafka-event-source--yaml"></a>

```
Events:
  SelfManagedKafkaEvent:
    Type: SelfManagedKafka
    Properties:
      BatchSize: 1000
      Enabled: true
      KafkaBootstrapServers:
        - abc.xyz.com:xxxx
      SourceAccessConfigurations: 
        -  Type: BASIC_AUTH
           URI: arn:aws:secretsmanager:us-west-2:123456789012:secret:my-path/my-secret-name-1a2b3c
      Topics:
        - MyKafkaTopic
```