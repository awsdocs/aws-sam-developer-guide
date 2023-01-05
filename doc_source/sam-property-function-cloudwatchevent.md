# CloudWatchEvent<a name="sam-property-function-cloudwatchevent"></a>

The object describing a `CloudWatchEvent` event source type\.

AWS Serverless Application Model \(AWS SAM\) generates an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html) resource when this event type is set\.

**Important Note**: [EventBridgeRule](sam-property-function-eventbridgerule.md) is the preferred event source type to use, instead of `CloudWatchEvent`\. `EventBridgeRule` and `CloudWatchEvent` use the same underlying service, API, and AWS CloudFormation resources\. However, AWS SAM will add support for new features only to `EventBridgeRule`\.

## Syntax<a name="sam-property-function-cloudwatchevent-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-cloudwatchevent-syntax.yaml"></a>

```
  [Enabled](#sam-function-cloudwatchevent-enabled): Boolean
  [EventBusName](#sam-function-cloudwatchevent-eventbusname): String
  [Input](#sam-function-cloudwatchevent-input): String
  [InputPath](#sam-function-cloudwatchevent-inputpath): String
  [Pattern](#sam-function-cloudwatchevent-pattern): [EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)
  [State](#sam-function-cloudwatchevent-state): String
```

## Properties<a name="sam-property-function-cloudwatchevent-properties"></a>

 `Enabled`   <a name="sam-function-cloudwatchevent-enabled"></a>
Indicates whether the rule is enabled\.  
To disable the rule, set this property to `false`\.  
Specify either the `Enabled` or `State` property, but not both\.
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[State](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-state)` property of an `AWS::Events::Rule` resource\. If this property is set to `true` then AWS SAM passes `ENABLED`, otherwise it passes `DISABLED`\.

 `EventBusName`   <a name="sam-function-cloudwatchevent-eventbusname"></a>
The event bus to associate with this rule\. If you omit this property, AWS SAM uses the default event bus\.  
*Type*: String  
*Required*: No  
*Default*: Default event bus  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventBusName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventbusname)` property of an `AWS::Events::Rule` resource\.

 `Input`   <a name="sam-function-cloudwatchevent-input"></a>
Valid JSON text passed to the target\. If you use this property, nothing from the event text itself is passed to the target\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Input](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-input)` property of an `AWS::Events::Rule Target` resource\.

 `InputPath`   <a name="sam-function-cloudwatchevent-inputpath"></a>
When you don't want to pass the entire matched event to the target, use the `InputPath` property to describe which part of the event to pass\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[InputPath](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-inputpath)` property of an `AWS::Events::Rule Target` resource\.

 `Pattern`   <a name="sam-function-cloudwatchevent-pattern"></a>
Describes which events are routed to the specified target\. For more information, see [Events and Event Patterns in EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eventbridge-and-event-patterns.html) in the *Amazon EventBridge User Guide*\.  
*Type*: [EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)` property of an `AWS::Events::Rule` resource\.

 `State`   <a name="sam-function-cloudwatchevent-state"></a>
The state of the rule\.  
*Accepted values:* `DISABLED | ENABLED`  
Specify either the `Enabled` or `State` property, but not both\.
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[State](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-state)` property of an `AWS::Events::Rule` resource\.

## Examples<a name="sam-property-function-cloudwatchevent--examples"></a>

### CloudWatchEvent<a name="sam-property-function-cloudwatchevent--examples--cloudwatchevent"></a>

The following is an example of a `CloudWatchEvent` event source type\.

#### YAML<a name="sam-property-function-cloudwatchevent--examples--cloudwatchevent--yaml"></a>

```
CWEvent:
  Type: CloudWatchEvent
  Properties:
    Enabled: false
    Input: '{"Key": "Value"}'
    Pattern:
      detail:
        state:
          - running
```