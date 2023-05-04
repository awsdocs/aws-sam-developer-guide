# Schedule<a name="sam-property-function-schedule"></a>

The object describing a `Schedule` event source type, which sets your serverless function as the target of an Amazon EventBridge rule that triggers on a schedule\. For more information, see [What Is Amazon EventBridge?](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html) in the *Amazon EventBridge User Guide*\.

AWS Serverless Application Model \(AWS SAM\) generates an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html) resource when this event type is set\.

**Note**  
EventBridge now offers a new scheduling capability, [Amazon EventBridge Scheduler](https://docs.aws.amazon.com/scheduler/latest/UserGuide/what-is-scheduler.html)\. Amazon EventBridge Scheduler is a serverless scheduler that allows you to create, run, and manage tasks from one central, managed service\. EventBridge Scheduler is highly customizable, and offers improved scalability over EventBridge scheduled rules, with a wider set of target API operations and AWS services\.  
We recommend that you use EventBridge Scheduler to invoke targets on a schedule\. To define this event source type in your AWS SAM templates, see [ScheduleV2](sam-property-function-schedulev2.md)\.

## Syntax<a name="sam-property-function-schedule-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-schedule-syntax.yaml"></a>

```
  [DeadLetterConfig](#sam-function-schedule-deadletterconfig): DeadLetterConfig
  [Description](#sam-function-schedule-description): String
  [Enabled](#sam-function-schedule-enabled): Boolean
  [Input](#sam-function-schedule-input): String
  [Name](#sam-function-schedule-name): String
  [RetryPolicy](#sam-function-schedule-retrypolicy): [RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)
  [Schedule](#sam-function-schedule-schedule): String
  [State](#sam-function-schedule-state): String
```

## Properties<a name="sam-property-function-schedule-properties"></a>

 `DeadLetterConfig`   <a name="sam-function-schedule-deadletterconfig"></a>
Configure the Amazon Simple Queue Service \(Amazon SQS\) queue where EventBridge sends events after a failed target invocation\. Invocation can fail, for example, when sending an event to a Lambda function that doesn't exist, or when EventBridge has insufficient permissions to invoke the Lambda function\. For more information, see [Event retry policy and using dead\-letter queues](https://docs.aws.amazon.com/eventbridge/latest/userguide/rule-dlq.html) in the *Amazon EventBridge User Guide*\.  
The [AWS::Serverless::Function](sam-resource-function.md) resource type has a similar data type, `DeadLetterQueue`, which handles failures that occur after successful invocation of the target Lambda function\. Examples of these types of failures include Lambda throttling, or errors returned by the Lambda target function\. For more information about the function `DeadLetterQueue` property, see [AWS Lambda function dead\-letter queues](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html#dlq) in the *AWS Lambda Developer Guide*\.
*Type*: [DeadLetterConfig](sam-property-function-scheduledeadletterconfig.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[DeadLetterConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-deadletterconfig)` property of the `AWS::Events::Rule` `Target` data type\. The AWS SAM version of this property includes additional subproperties, in case you want AWS SAM to create the dead\-letter queue for you\.

 `Description`   <a name="sam-function-schedule-description"></a>
A description of the rule\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Description](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-description)` property of an `AWS::Events::Rule` resource\.

 `Enabled`   <a name="sam-function-schedule-enabled"></a>
Indicates whether the rule is enabled\.  
To disable the rule, set this property to `false`\.  
Specify either the `Enabled` or `State` property, but not both\.
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[State](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-state)` property of an `AWS::Events::Rule` resource\. If this property is set to `true` then AWS SAM passes `ENABLED`, otherwise it passes `DISABLED`\.

 `Input`   <a name="sam-function-schedule-input"></a>
Valid JSON text passed to the target\. If you use this property, nothing from the event text itself is passed to the target\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Input](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-input)` property of an `AWS::Events::Rule Target` resource\.

 `Name`   <a name="sam-function-schedule-name"></a>
The name of the rule\. If you don't specify a name, AWS CloudFormation generates a unique physical ID and uses that ID for the rule name\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Name](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-name)` property of an `AWS::Events::Rule` resource\.

 `RetryPolicy`   <a name="sam-function-schedule-retrypolicy"></a>
A `RetryPolicy` object that includes information about the retry policy settings\. For more information, see [Event retry policy and using dead\-letter queues](https://docs.aws.amazon.com/eventbridge/latest/userguide/rule-dlq.html) in the *Amazon EventBridge User Guide*\.  
*Type*: [RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)` property of the `AWS::Events::Rule` `Target` data type\.

 `Schedule`   <a name="sam-function-schedule-schedule"></a>
The scheduling expression that determines when and how often the rule runs\. For more information, see [Schedule Expressions for Rules](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-create-rule-schedule.html)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ScheduleExpression](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-scheduleexpression)` property of an `AWS::Events::Rule` resource\.

 `State`   <a name="sam-function-schedule-state"></a>
The state of the rule\.  
*Accepted values:* `DISABLED | ENABLED`  
Specify either the `Enabled` or `State` property, but not both\.
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[State](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-state)` property of an `AWS::Events::Rule` resource\.

## Examples<a name="sam-property-function-schedule--examples"></a>

### CloudWatch Schedule Event<a name="sam-property-function-schedule--examples--cloudwatch-schedule-event"></a>

CloudWatch Schedule Event Example

#### YAML<a name="sam-property-function-schedule--examples--cloudwatch-schedule-event--yaml"></a>

```
CWSchedule:
  Type: Schedule
  Properties:
    Schedule: 'rate(1 minute)'
    Name: TestSchedule
    Description: test schedule
    Enabled: false
```