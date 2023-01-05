# AlexaSkill<a name="sam-property-function-alexaskill"></a>

The object describing an `AlexaSkill` event source type\.

## Syntax<a name="sam-property-function-alexaskill-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-alexaskill-syntax.yaml"></a>

```
  [SkillId](#sam-function-alexaskill-skillid): String
```

## Properties<a name="sam-property-function-alexaskill-properties"></a>

 `SkillId`   <a name="sam-function-alexaskill-skillid"></a>
The Alexa Skill ID for your Alexa Skill\. For more information about Skill ID see [Configure the trigger for a Lambda function](https://developer.amazon.com/docs/custom-skills/host-a-custom-skill-as-an-aws-lambda-function.html#configuring-the-alexa-skills-kit-trigger) in the Alexa Skills Kit documentation\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-alexaskill--examples"></a>

### AlexaSkillTrigger<a name="sam-property-function-alexaskill--examples--alexaskilltrigger"></a>

Alexa Skill Event Example

#### YAML<a name="sam-property-function-alexaskill--examples--alexaskilltrigger--yaml"></a>

```
AlexaSkillEvent:
  Type: AlexaSkill
```