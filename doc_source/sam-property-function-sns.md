# SNS<a name="sam-property-function-sns"></a>

SNS event source configuration\.

SAM generates [AWS::SNS::Subscription](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sns-subscription.html) resource when this event type is set

## Syntax<a name="sam-property-function-sns-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-function-sns-syntax.yaml"></a>

```
  [FilterPolicy](#sam-function-sns-filterpolicy): [SnsFilterPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sns-subscription.html#cfn-sns-subscription-filterpolicy)
  [Region](#sam-function-sns-region): String
  [SqsSubscription](#sam-function-sns-sqssubscription): Boolean | [SqsSubscriptionObject](sam-property-function-sqssubscriptionobject.md)
  [Topic](#sam-function-sns-topic): String
```

## Properties<a name="sam-property-function-sns-properties"></a>

 `FilterPolicy`   <a name="sam-function-sns-filterpolicy"></a>
The filter policy JSON assigned to the subscription\. For more information, see [GetSubscriptionAttributes](https://docs.aws.amazon.com/sns/latest/api/API_GetSubscriptionAttributes.html) in the Amazon Simple Notification Service API Reference\.  
*Type*: [SnsFilterPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sns-subscription.html#cfn-sns-subscription-filterpolicy)  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[FilterPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sns-subscription.html#cfn-sns-subscription-filterpolicy)` property of an `AWS::SNS::Subscription`\.

 `Region`   <a name="sam-function-sns-region"></a>
For cross\-region subscriptions, the region in which the topic resides\.  
If no region is specified, CloudFormation uses the region of the caller as the default\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[Region](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sns-subscription.html#cfn-sns-subscription-region)` property of an `AWS::SNS::Subscription`\.

 `SqsSubscription`   <a name="sam-function-sns-sqssubscription"></a>
Set this property to true, or specify `SqsSubscriptionObject` to enable batching SNS topic notifications in an SQS queue\. Setting this property to `true` creates a new SQS queue, whereas specifying a `SqsSubscriptionObject` uses an existing SQS queue\.  
*Type*: Boolean \| [SqsSubscriptionObject](sam-property-function-sqssubscriptionobject.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `Topic`   <a name="sam-function-sns-topic"></a>
The ARN of the topic to subscribe to\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is passed directly to the `[TopicArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sns-subscription.html#topicarn)` property of an `AWS::SNS::Topic`\.

## Examples<a name="sam-property-function-sns--examples"></a>

### SNS Event Source Example<a name="sam-property-function-sns--examples--sns-event-source-example"></a>

SNS Event Source Example

#### YAML<a name="sam-property-function-sns--examples--sns-event-source-example--yaml"></a>

```
Properties:
  FilterPolicy:
    price_usd:
    - numeric:
      - '>='
      - 100
    store:
    - example_corp
  SqsSubscription: true
  Topic: arn:aws:sns:us-east-1:123456789012:my_topic
```