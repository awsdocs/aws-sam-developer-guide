# Target<a name="sam-property-statemachine-statemachinescheduletarget"></a>

Configures the AWS resource that EventBridge invokes when a rule is triggered\.

## Syntax<a name="sam-property-statemachine-statemachinescheduletarget-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-statemachine-statemachinescheduletarget-syntax.yaml"></a>

```
  [Id](#sam-statemachine-statemachinescheduletarget-id): String
```

## Properties<a name="sam-property-statemachine-statemachinescheduletarget-properties"></a>

 `Id`   <a name="sam-statemachine-statemachinescheduletarget-id"></a>
The logical ID of the target\.  
The value of `Id` can include alphanumeric characters, periods \(`.`\), hyphens \(`-`\), and underscores \(`_`\)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Id](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-id)` property of the `AWS::Events::Rule` `Target` data type\.

## Examples<a name="sam-property-statemachine-statemachinescheduletarget--examples"></a>

### Target<a name="sam-property-statemachine-statemachinescheduletarget--examples--target"></a>

#### YAML<a name="sam-property-statemachine-statemachinescheduletarget--examples--target--yaml"></a>

```
EBRule:
  Type: Schedule
  Properties:
    Target:
      Id: MyTarget
```