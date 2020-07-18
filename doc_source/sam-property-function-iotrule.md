# IoTRule<a name="sam-property-function-iotrule"></a>

The object describing an `IoTRule` event source type\.

Creates an [AWS::IoT::TopicRule](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iot-topicrule.html) resource to declare an AWS IoT rule\. For more information see [AWS CloudFormation documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iot-topicrule.html)

## Syntax<a name="sam-property-function-iotrule-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-iotrule-syntax.yaml"></a>

```
  [AwsIotSqlVersion](#sam-function-iotrule-awsiotsqlversion): String
  [Sql](#sam-function-iotrule-sql): String
```

## Properties<a name="sam-property-function-iotrule-properties"></a>

 `AwsIotSqlVersion`   <a name="sam-function-iotrule-awsiotsqlversion"></a>
The version of the SQL rules engine to use when evaluating the rule\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[AwsIotSqlVersion](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-iot-topicrule-topicrulepayload.html#cfn-iot-topicrule-topicrulepayload-awsiotsqlversion)` property of an `AWS::IoT::TopicRule TopicRulePayload` resource\.

 `Sql`   <a name="sam-function-iotrule-sql"></a>
The SQL statement used to query the topic\. For more information, see [AWS IoT SQL Reference](https://docs.aws.amazon.com/iot/latest/developerguide/iot-rules.html#aws-iot-sql-reference) in the AWS IoT Developer Guide\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Sql](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-iot-topicrule-topicrulepayload.html#cfn-iot-topicrule-topicrulepayload-sql)` property of an `AWS::IoT::TopicRule TopicRulePayload` resource\.

## Examples<a name="sam-property-function-iotrule--examples"></a>

### IOT Rule<a name="sam-property-function-iotrule--examples--iot-rule"></a>

IOT Rule Example

#### YAML<a name="sam-property-function-iotrule--examples--iot-rule--yaml"></a>

```
IoTRule:
  Type: IoTRule
  Properties:
    Sql: SELECT * FROM 'topic/test'
```