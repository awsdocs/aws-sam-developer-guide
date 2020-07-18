# CloudWatchEvent<a name="sam-property-statemachine-statemachinecloudwatchevent"></a>

The object describing a `CloudWatchEvent` event source type\.

AWS Serverless Application Model \(AWS SAM\) generates an [AWS::Events::Rule](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html) resource when this event type is set\.

**Important Note**: [EventBridgeRule](sam-property-statemachine-eventbridgerule.md) is the preferred event source type to use, instead of `CloudWatchEvent`\. `EventBridgeRule` and `CloudWatchEvent` use the same underlying service, API, and AWS CloudFormation resources\. However, AWS SAM will add support for new features only to `EventBridgeRule`\.

## Syntax<a name="sam-property-statemachine-statemachinecloudwatchevent-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-statemachine-statemachinecloudwatchevent-syntax.yaml"></a>

```
  [EventBusName](#sam-statemachine-statemachinecloudwatchevent-eventbusname): String
  [Input](#sam-statemachine-statemachinecloudwatchevent-input): String
  [InputPath](#sam-statemachine-statemachinecloudwatchevent-inputpath): String
  [Pattern](#sam-statemachine-statemachinecloudwatchevent-pattern): [EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)
```

## Properties<a name="sam-property-statemachine-statemachinecloudwatchevent-properties"></a>

 `EventBusName`   <a name="sam-statemachine-statemachinecloudwatchevent-eventbusname"></a>
The event bus to associate with this rule\. If you omit this property, AWS SAM uses the default event bus\.  
*Type*: String  
*Required*: No  
*Default*: Default event bus  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventBusName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventbusname)` property of an `AWS::Events::Rule` resource\.

 `Input`   <a name="sam-statemachine-statemachinecloudwatchevent-input"></a>
Valid JSON text passed to the target\. If you use this property, nothing from the event text itself is passed to the target\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Input](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-input)` property of an `AWS::Events::Rule Target` resource\.

 `InputPath`   <a name="sam-statemachine-statemachinecloudwatchevent-inputpath"></a>
When you don't want to pass the entire matched event to the target, use the `InputPath` property to describe which part of the event to pass\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[InputPath](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-inputpath)` property of an `AWS::Events::Rule Target` resource\.

 `Pattern`   <a name="sam-statemachine-statemachinecloudwatchevent-pattern"></a>
Describes which events are routed to the specified target\. For more information, see [Events and Event Patterns in EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eventbridge-and-event-patterns.html) in the Amazon EventBridge User Guide  
*Type*: [EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)` property of an `AWS::Events::Rule` resource\.

## Examples<a name="sam-property-statemachine-statemachinecloudwatchevent--examples"></a>

### CloudWatchEvent<a name="sam-property-statemachine-statemachinecloudwatchevent--examples--cloudwatchevent"></a>

The following is an example of a `CloudWatchEvent` event source type\.

#### YAML<a name="sam-property-statemachine-statemachinecloudwatchevent--examples--cloudwatchevent--yaml"></a>

```
CWEvent:
  Type: CloudWatchEvent
  Properties:
    Input: '{"Key": "Value"}'
    Pattern:
      detail:
        state:
          - terminated
```