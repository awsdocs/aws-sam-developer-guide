# EventSource<a name="sam-property-statemachine-statemachineeventsource"></a>

The object describing the source of events which trigger the state machine\. Each event consists of a type and a set of properties that depend on that type\. For more information about the properties of each event source, see the topic corresponding to that type\.

## Syntax<a name="sam-property-statemachine-statemachineeventsource-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-statemachine-statemachineeventsource-syntax.yaml"></a>

```
  [Properties](#sam-statemachine-statemachineeventsource-properties): [Schedule](sam-property-statemachine-schedule.md) | [CloudWatchEvent](sam-property-statemachine-cloudwatchevent.md) | [EventBridgeRule](sam-property-statemachine-eventbridgerule.md) | [Api](sam-property-statemachine-statemachineapi.md)
  [Type](#sam-statemachine-statemachineeventsource-type): String
```

## Properties<a name="sam-property-statemachine-statemachineeventsource-properties"></a>

 `Properties`   <a name="sam-statemachine-statemachineeventsource-properties"></a>
Object describing properties of this event mapping\. The set of properties must conform to the defined Type\.  
*Type*: [Schedule](sam-property-statemachine-schedule.md) \| [CloudWatchEvent](sam-property-statemachine-cloudwatchevent.md) \| [EventBridgeRule](sam-property-statemachine-eventbridgerule.md) \| [Api](sam-property-statemachine-statemachineapi.md)  
*Required*: Yes  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Type`   <a name="sam-statemachine-statemachineeventsource-type"></a>
The event type\.  
Supported values: `Api`, `Schedule`, `CloudWatchEvent`, `EventBridgeRule`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-statemachine-statemachineeventsource--examples"></a>

### API\-Event<a name="sam-property-statemachine-statemachineeventsource--examples--api-event"></a>

Example of using an API Event

#### YAML<a name="sam-property-statemachine-statemachineeventsource--examples--api-event--yaml"></a>

```
ApiEvent:
  Type: Api
  Properties:
    Method: get
    Path: /group/{user}
    RestApiId: 
      Ref: MyApi
```