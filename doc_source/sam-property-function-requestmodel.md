# RequestModel<a name="sam-property-function-requestmodel"></a>

Configure Request Model for a specific Api\+Path\+Method\.

## Syntax<a name="sam-property-function-requestmodel-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-requestmodel-syntax.yaml"></a>

```
  [Model](#sam-function-requestmodel-model): String
  [Required](#sam-function-requestmodel-required): Boolean
```

## Properties<a name="sam-property-function-requestmodel-properties"></a>

 `Model`   <a name="sam-function-requestmodel-model"></a>
Name of a model defined in the Models property of the [AWS::Serverless::Api](sam-resource-api.md)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Required`   <a name="sam-function-requestmodel-required"></a>
adds a `required` property in the parameters section of OpenApi definition for given API endpoint  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-requestmodel--examples"></a>

### Request Model<a name="sam-property-function-requestmodel--examples--request-model"></a>

Request Model Example

#### YAML<a name="sam-property-function-requestmodel--examples--request-model--yaml"></a>

```
RequestModel:
  Model: User
  Required: true
```