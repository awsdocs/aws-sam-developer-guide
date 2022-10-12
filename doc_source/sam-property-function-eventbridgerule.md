# EventBridgeRule<a name="sam-property-function-eventbridgerule"></a>

The object describing an `EventBridgeRule` event source type, which sets your serverless function as the target of an Amazon EventBridge rule\. For more information, see [What Is Amazon EventBridge?](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html) in the *Amazon EventBridge User Guide*\.

AWS SAM generates an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html) resource when this event type is set\.

## Syntax<a name="sam-property-function-eventbridgerule-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-eventbridgerule-syntax.yaml"></a>

```
  [DeadLetterConfig](#sam-function-eventbridgerule-deadletterconfig): DeadLetterConfig
  [Enabled](#sam-function-eventbridgerule-enabled): Boolean
  [EventBusName](#sam-function-eventbridgerule-eventbusname): String
  [Input](#sam-function-eventbridgerule-input): String
  [InputPath](#sam-function-eventbridgerule-inputpath): String
  [Pattern](#sam-function-eventbridgerule-pattern): [EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)
  [RetryPolicy](#sam-function-eventbridgerule-retrypolicy): [RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)
  [Target](#sam-function-eventbridgerule-target): Target
```

## Properties<a name="sam-property-function-eventbridgerule-properties"></a>

 `DeadLetterConfig`   <a name="sam-function-eventbridgerule-deadletterconfig"></a>
Configure the Amazon Simple Queue Service \(Amazon SQS\) queue where EventBridge sends events after a failed target invocation\. Invocation can fail, for example, when sending an event to a Lambda function that doesn't exist, or when EventBridge has insufficient permissions to invoke the Lambda function\. For more information, see [Event retry policy and using dead\-letter queues](https://docs.aws.amazon.com/eventbridge/latest/userguide/rule-dlq.html) in the *Amazon EventBridge User Guide*\.  
**Note:** The [AWS::Serverless::Function](sam-resource-function.md) resource type has a similar data type, `DeadLetterQueue`, which handles failures that occur after successful invocation of the target Lambda function\. Examples of these types of failures include Lambda throttling, or errors returned by the Lambda target function\. For more information about the function `DeadLetterQueue` property, see [AWS Lambda function dead\-letter queues](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html#dlq) in the *AWS Lambda Developer Guide*\.  
*Type*: [DeadLetterConfig](sam-property-function-deadletterconfig.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[DeadLetterConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-deadletterconfig)` property of the `AWS::Events::Rule` `Target` data type\. The AWS SAM version of this property includes additional subproperties, in case you want AWS SAM to create the dead\-letter queue for you\.

 `Enabled`   <a name="sam-function-eventbridgerule-enabled"></a>
Indicates whether the rule is enabled\.  
To disable the rule, set this property to `false`\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[State](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-state)` property of an `AWS::Events::Rule` resource\. If this property is set to `true` then AWS SAM passes `ENABLED`, otherwise it passes `DISABLED`\.

 `EventBusName`   <a name="sam-function-eventbridgerule-eventbusname"></a>
The event bus to associate with this rule\. If you omit this property, AWS SAM uses the default event bus\.  
*Type*: String  
*Required*: No  
*Default*: Default event bus  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventBusName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventbusname)` property of an `AWS::Events::Rule` resource\.

 `Input`   <a name="sam-function-eventbridgerule-input"></a>
Valid JSON text passed to the target\. If you use this property, nothing from the event text itself is passed to the target\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Input](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-input)` property of an `AWS::Events::Rule Target` resource\.

 `InputPath`   <a name="sam-function-eventbridgerule-inputpath"></a>
When you don't want to pass the entire matched event to the target, use the `InputPath` property to describe which part of the event to pass\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[InputPath](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-inputpath)` property of an `AWS::Events::Rule Target` resource\.

 `Pattern`   <a name="sam-function-eventbridgerule-pattern"></a>
Describes which events are routed to the specified target\. For more information, see [Events and Event Patterns in EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eventbridge-and-event-patterns.html) in the *Amazon EventBridge User Guide*\.  
*Type*: [EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)` property of an `AWS::Events::Rule` resource\.

 `RetryPolicy`   <a name="sam-function-eventbridgerule-retrypolicy"></a>
A `RetryPolicy` object that includes information about the retry policy settings\. For more information, see [Event retry policy and using dead\-letter queues](https://docs.aws.amazon.com/eventbridge/latest/userguide/rule-dlq.html) in the *Amazon EventBridge User Guide*\.  
*Type*: [RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)` property of the `AWS::Events::Rule` `Target` data type\.

 `Target`   <a name="sam-function-eventbridgerule-target"></a>
The AWS resource that EventBridge invokes when a rule is triggered\. You can use this property to specify the logical ID of the target\. If this property is not specified, then AWS SAM generates the logical ID of the target\.  
*Type*: [Target](sam-property-function-target.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[Targets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-targets)` property of an `AWS::Events::Rule` resource\. The AWS SAM version of this property only allows you to specify the logical ID of a single target\.

## Examples<a name="sam-property-function-eventbridgerule--examples"></a>

### EventBridgeRule<a name="sam-property-function-eventbridgerule--examples--eventbridgerule"></a>

The following is an example of an `EventBridgeRule` event source type\.

#### YAML<a name="sam-property-function-eventbridgerule--examples--eventbridgerule--yaml"></a>

```
EBRule:
  Type: EventBridgeRule
  Properties:
    Input: '{"Key": "Value"}'
    Pattern:
      detail:
        state:
          - terminated
    RetryPolicy:
      MaximumRetryAttempts: 5
      MaximumEventAgeInSeconds: 900
    DeadLetterConfig:
      Type: SQS
      QueueLogicalId: EBRuleDLQ
    Target:
      Id: MyTarget
    Enabled: false
```
