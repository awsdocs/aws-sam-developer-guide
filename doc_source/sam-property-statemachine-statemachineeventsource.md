# EventSource<a name="sam-property-statemachine-statemachineeventsource"></a>

The object describing the source of events which trigger the state machine\. Each event consists of a type and a set of properties that depend on that type\. For more information about the properties of each event source, see the subtopic corresponding to that type\.

## Syntax<a name="sam-property-statemachine-statemachineeventsource-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-statemachine-statemachineeventsource-syntax.yaml"></a>

```
  [Properties](#sam-statemachine-statemachineeventsource-properties): Schedule | CloudWatchEvent | EventBridgeRule | Api
  [Type](#sam-statemachine-statemachineeventsource-type): String
```

## Properties<a name="sam-property-statemachine-statemachineeventsource-properties"></a>

 `Properties`   <a name="sam-statemachine-statemachineeventsource-properties"></a>
An object describing the properties of this event mapping\. The set of properties must conform to the defined `Type`\.  
*Type*: [Schedule](sam-property-statemachine-schedule.md) \| [CloudWatchEvent](sam-property-statemachine-statemachinecloudwatchevent.md) \| [EventBridgeRule](sam-property-statemachine-eventbridgerule.md) \| [Api](sam-property-statemachine-statemachineapi.md)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Type`   <a name="sam-statemachine-statemachineeventsource-type"></a>
The event type\.  
Valid values: `Api`, `Schedule`, `CloudWatchEvent`, `EventBridgeRule`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-statemachine-statemachineeventsource--examples"></a>

### API<a name="sam-property-statemachine-statemachineeventsource--examples--api"></a>

The following is an example of an event of the `API` type\.

#### YAML<a name="sam-property-statemachine-statemachineeventsource--examples--api--yaml"></a>

```
ApiEvent:
  Type: Api
  Properties:
    Method: get
    Path: /group/{user}
    RestApiId: 
      Ref: MyApi
```