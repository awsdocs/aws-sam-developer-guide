# Schedule<a name="sam-property-function-schedule"></a>

The object describing a `Schedule` event source type\.

AWS SAM generates an [AWS::Events::Rule](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html) resource when this event type is set\.

## Syntax<a name="sam-property-function-schedule-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-schedule-syntax.yaml"></a>

```
  [Description](#sam-function-schedule-description): String
  [Enabled](#sam-function-schedule-enabled): Boolean
  [Input](#sam-function-schedule-input): String
  [Name](#sam-function-schedule-name): String
  [Schedule](#sam-function-schedule-schedule): String
```

## Properties<a name="sam-property-function-schedule-properties"></a>

 `Description`   <a name="sam-function-schedule-description"></a>
A description of the rule\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Description](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-description)` property of an `AWS::Events::Rule` resource\.

 `Enabled`   <a name="sam-function-schedule-enabled"></a>
Indicates whether the rule is enabled\.  
To disable the rule, set this property to `False`\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[State](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-state)` property of an `AWS::Events::Rule` resource\. If this property is set to `True` then AWS SAM passes `ENABLED`, otherwise it passes `DISABLED`\.

 `Input`   <a name="sam-function-schedule-input"></a>
Valid JSON text passed to the target\. If you use this property, nothing from the event text itself is passed to the target\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Target](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-input)` property of an `AWS::Events::Rule Target` resource\.

 `Name`   <a name="sam-function-schedule-name"></a>
The name of the rule\. If you don't specify a name, AWS CloudFormation generates a unique physical ID and uses that ID for the rule name\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Name](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-name)` property of an `AWS::Events::Rule` resource\.

 `Schedule`   <a name="sam-function-schedule-schedule"></a>
The scheduling expression that determines when and how often the rule runs\. For more information, see [Schedule Expressions for Rules](https://docs.aws.amazon.com/eventbridge/latest/userguide/scheduled-events.html)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ScheduleExpression](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-scheduleexpression)` property of an `AWS::Events::Rule` resource\.

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
    Enabled: False
```