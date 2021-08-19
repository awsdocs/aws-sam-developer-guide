# EventBridgeRule<a name="sam-property-statemachine-statemachineeventbridgerule"></a>

The object describing an `EventBridgeRule` event source type, which sets your state machine as the target for an Amazon EventBridge rule\. For more information, see [What Is Amazon EventBridge?](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html) in the *Amazon EventBridge User Guide*\.

AWS SAM generates an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html) resource when this event type is set\.

## Syntax<a name="sam-property-statemachine-statemachineeventbridgerule-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-statemachine-statemachineeventbridgerule-syntax.yaml"></a>

```
  [DeadLetterConfig](#sam-statemachine-statemachineeventbridgerule-deadletterconfig): DeadLetterConfig
  [EventBusName](#sam-statemachine-statemachineeventbridgerule-eventbusname): String
  [Input](#sam-statemachine-statemachineeventbridgerule-input): String
  [InputPath](#sam-statemachine-statemachineeventbridgerule-inputpath): String
  [Pattern](#sam-statemachine-statemachineeventbridgerule-pattern): [EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)
  [RetryPolicy](#sam-statemachine-statemachineeventbridgerule-retrypolicy): [RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)
```

## Properties<a name="sam-property-statemachine-statemachineeventbridgerule-properties"></a>

 `DeadLetterConfig`   <a name="sam-statemachine-statemachineeventbridgerule-deadletterconfig"></a>
Configure the Amazon Simple Queue Service \(Amazon SQS\) queue where EventBridge sends events after a failed target invocation\. Invocation can fail, for example, when sending an event to a Lambda function that doesn't exist, or when EventBridge has insufficient permissions to invoke the Lambda function\. For more information, see [Event retry policy and using dead\-letter queues](https://docs.aws.amazon.com/eventbridge/latest/userguide/rule-dlq.html) in the *Amazon EventBridge User Guide*\.  
*Type*: [DeadLetterConfig](sam-property-statemachine-statemachinedeadletterconfig.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[DeadLetterConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-deadletterconfig)` property of the `AWS::Events::Rule` `Target` data type\. The AWS SAM version of this property includes additional subproperties, in case you want AWS SAM to create the dead\-letter queue for you\.

 `EventBusName`   <a name="sam-statemachine-statemachineeventbridgerule-eventbusname"></a>
The event bus to associate with this rule\. If you omit this property, AWS SAM uses the default event bus\.  
*Type*: String  
*Required*: No  
*Default*: Default event bus  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventBusName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventbusname)` property of an `AWS::Events::Rule` resource\.

 `Input`   <a name="sam-statemachine-statemachineeventbridgerule-input"></a>
Valid JSON text passed to the target\. If you use this property, nothing from the event text itself is passed to the target\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Input](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-input)` property of an `AWS::Events::Rule Target` resource\.

 `InputPath`   <a name="sam-statemachine-statemachineeventbridgerule-inputpath"></a>
When you don't want to pass the entire matched event to the target, use the `InputPath` property to describe which part of the event to pass\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[InputPath](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-inputpath)` property of an `AWS::Events::Rule Target` resource\.

 `Pattern`   <a name="sam-statemachine-statemachineeventbridgerule-pattern"></a>
Describes which events are routed to the specified target\. For more information, see [Events and Event Patterns in EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eventbridge-and-event-patterns.html) in the *Amazon EventBridge User Guide*\.  
*Type*: [EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-rule.html#cfn-events-rule-eventpattern)` property of an `AWS::Events::Rule` resource\.

 `RetryPolicy`   <a name="sam-statemachine-statemachineeventbridgerule-retrypolicy"></a>
A `RetryPolicy` object that includes information about the retry policy settings\. For more information, see [Event retry policy and using dead\-letter queues](https://docs.aws.amazon.com/eventbridge/latest/userguide/rule-dlq.html) in the *Amazon EventBridge User Guide*\.  
*Type*: [RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-retrypolicy)` property of the `AWS::Events::Rule` `Target` data type\.

## Examples<a name="sam-property-statemachine-statemachineeventbridgerule--examples"></a>

### EventBridgeRule<a name="sam-property-statemachine-statemachineeventbridgerule--examples--eventbridgerule"></a>

The following is an example of an `EventBridgeRule` event source type\.

#### YAML<a name="sam-property-statemachine-statemachineeventbridgerule--examples--eventbridgerule--yaml"></a>

```
EBRule:
  Type: EventBridgeRule
  Properties:
    Input: '{"Key": "Value"}'
    Pattern:
      detail:
        state:
          - terminated
```