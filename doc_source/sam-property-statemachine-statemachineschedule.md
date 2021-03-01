# Schedule<a name="sam-property-statemachine-statemachineschedule"></a>

The object describing a `Schedule` event source type, which sets your state machine as the target of an EventBridge rule that triggers on a schedule\. For more information, see [What Is Amazon EventBridge?](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html) in the *Amazon EventBridge User Guide*\.

AWS Serverless Application Model \(AWS SAM\) generates an [AWS::Events::Rule](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html) resource when this event type is set\.

## Syntax<a name="sam-property-statemachine-statemachineschedule-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-statemachine-statemachineschedule-syntax.yaml"></a>

```
  [DeadLetterConfig](#sam-statemachine-statemachineschedule-deadletterconfig): DeadLetterConfig
  [Description](#sam-statemachine-statemachineschedule-description): String
  [Enabled](#sam-statemachine-statemachineschedule-enabled): Boolean
  [Input](#sam-statemachine-statemachineschedule-input): String
  [Name](#sam-statemachine-statemachineschedule-name): String
  [RetryPolicy](#sam-statemachine-statemachineschedule-retrypolicy): [RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)
  [Schedule](#sam-statemachine-statemachineschedule-schedule): String
```

## Properties<a name="sam-property-statemachine-statemachineschedule-properties"></a>

 `DeadLetterConfig`   <a name="sam-statemachine-statemachineschedule-deadletterconfig"></a>
Configure the Amazon Simple Queue Service \(Amazon SQS\) queue where EventBridge sends events after a failed target invocation\. Invocation can fail, for example, when sending an event to a Lambda function that doesn't exist, or when EventBridge has insufficient permissions to invoke the Lambda function\. For more information, see [Event retry policy and using dead\-letter queues](https://docs.aws.amazon.com/eventbridge/latest/userguide/rule-dlq.html) in the *Amazon EventBridge User Guide*\.  
*Type*: [DeadLetterConfig](sam-property-statemachine-statemachinescheduledeadletterconfig.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[DeadLetterConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-deadletterconfig)` property of the `AWS::Events::Rule` `Target` data type\. The AWS SAM version of this property includes additional subproperties, in case you want AWS SAM to create the dead\-letter queue for you\.

 `Description`   <a name="sam-statemachine-statemachineschedule-description"></a>
A description of the rule\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Description](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-description)` property of an `AWS::Events::Rule` resource\.

 `Enabled`   <a name="sam-statemachine-statemachineschedule-enabled"></a>
Indicates whether the rule is enabled\.  
To disable the rule, set this property to `False`\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[State](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-state)` property of an `AWS::Events::Rule` resource\. If this property is set to `True` then AWS SAM passes `ENABLED`, otherwise it passes `DISABLED`\.

 `Input`   <a name="sam-statemachine-statemachineschedule-input"></a>
Valid JSON text passed to the target\. If you use this property, nothing from the event text itself is passed to the target\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Target](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-input)` property of an `AWS::Events::Rule Target` resource\.

 `Name`   <a name="sam-statemachine-statemachineschedule-name"></a>
The name of the rule\. If you don't specify a name, AWS CloudFormation generates a unique physical ID and uses that ID for the rule name\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Name](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-name)` property of an `AWS::Events::Rule` resource\.

 `RetryPolicy`   <a name="sam-statemachine-statemachineschedule-retrypolicy"></a>
A `RetryPolicy` object that includes information about the retry policy settings\. For more information, see [Event retry policy and using dead\-letter queues](https://docs.aws.amazon.com/eventbridge/latest/userguide/rule-dlq.html) in the *Amazon EventBridge User Guide*\.  
*Type*: [RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)` property of the `AWS::Events::Rule` `Target` data type\.

 `Schedule`   <a name="sam-statemachine-statemachineschedule-schedule"></a>
The scheduling expression that determines when and how often the rule runs\. For more information, see [Schedule Expressions for Rules](https://docs.aws.amazon.com/eventbridge/latest/userguide/scheduled-events.html)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ScheduleExpression](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-scheduleexpression)` property of an `AWS::Events::Rule` resource\.

## Examples<a name="sam-property-statemachine-statemachineschedule--examples"></a>

### CloudWatch Schedule Event<a name="sam-property-statemachine-statemachineschedule--examples--cloudwatch-schedule-event"></a>

CloudWatch Schedule Event Example

#### YAML<a name="sam-property-statemachine-statemachineschedule--examples--cloudwatch-schedule-event--yaml"></a>

```
CWSchedule:
  Type: Schedule
  Properties:
    Schedule: 'rate(1 minute)'
    Name: TestSchedule
    Description: test schedule
    Enabled: False
```