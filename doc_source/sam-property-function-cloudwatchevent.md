# CloudWatchEvent<a name="sam-property-function-cloudwatchevent"></a>

The object describing an event source with type CloudWatchEvent

SAM generates [AWS::Events::Rule](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html) resource when this event type is set

## Syntax<a name="sam-property-function-cloudwatchevent-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-function-cloudwatchevent-syntax.yaml"></a>

```
  [EventBusName](#sam-function-cloudwatchevent-eventbusname): String
  [Input](#sam-function-cloudwatchevent-input): String
  [InputPath](#sam-function-cloudwatchevent-inputpath): String
  [Pattern](#sam-function-cloudwatchevent-pattern): [EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)
```

## Properties<a name="sam-property-function-cloudwatchevent-properties"></a>

 `EventBusName`   <a name="sam-function-cloudwatchevent-eventbusname"></a>
The event bus to associate with this rule\. If you omit this, the default event bus is used\.  
*Type*: String  
*Required*: No  
*Default*: default  
*CloudFormation Compatibility*: This property is passed directly to the `[EventBusName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventbusname)` property of an `AWS::Events::Rule`\.

 `Input`   <a name="sam-function-cloudwatchevent-input"></a>
Valid JSON text passed to the target\. If you use this property, nothing from the event text itself is passed to the target\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[Target](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-input)` property of an `AWS::Events::Rule Target`\.

 `InputPath`   <a name="sam-function-cloudwatchevent-inputpath"></a>
When you don't want to pass the entire matched event, InputPath describes which part of the event to pass to the target\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[Target](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-inputpath)` property of an `AWS::Events::Rule Target`\.

 `Pattern`   <a name="sam-function-cloudwatchevent-pattern"></a>
Describes which events are routed to the specified target\. For more information, see [Events and Event Patterns in EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eventbridge-and-event-patterns.html) in the Amazon EventBridge User Guide  
*Type*: [EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)  
*Required*: Yes  
*CloudFormation Compatibility*: This property is passed directly to the `[EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)` property of an `AWS::Events::Rule`\.

## Examples<a name="sam-property-function-cloudwatchevent--examples"></a>

### CloudWatchEvent<a name="sam-property-function-cloudwatchevent--examples--cloudwatchevent"></a>

CloudWatch Event Example

#### YAML<a name="sam-property-function-cloudwatchevent--examples--cloudwatchevent--yaml"></a>

```
CWEvent:
  Properties:
    Input: '{"Key": "Value"}'
    Pattern:
      detail:
        state:
        - terminated
  Type: CloudWatchEvent
```