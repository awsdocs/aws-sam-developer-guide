# Target<a name="sam-property-function-target"></a>

Configures the AWS resource that EventBridge invokes when a rule is triggered\.

## Syntax<a name="sam-property-function-target-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-target-syntax.yaml"></a>

```
  [Id](#sam-function-target-id): String
```

## Properties<a name="sam-property-function-target-properties"></a>

 `Id`   <a name="sam-function-target-id"></a>
The logical ID of the target\.  
The value of `Id` can include alphanumeric characters, periods \(`.`\), hyphens \(`-`\), and underscores \(`_`\)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Id](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-events-rule-target.html#cfn-events-rule-target-id)` property of the `AWS::Events::Rule` `Target` data type\.

## Examples<a name="sam-property-function-target--examples"></a>

### Target<a name="sam-property-function-target--examples--target"></a>

Target

#### YAML<a name="sam-property-function-target--examples--target--yaml"></a>

```
EBRule:
  Type: EventBridgeRule
  Properties:
    Target:
      Id: MyTarget
```