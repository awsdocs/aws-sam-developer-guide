# RequestParameter<a name="sam-property-function-requestparameter"></a>

Configure Request Parameter for a specific Api\+Path\+Method\.

Either `Required` or `Caching` property needs to be specified for request parameter

## Syntax<a name="sam-property-function-requestparameter-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-requestparameter-syntax.yaml"></a>

```
  [Caching](#sam-function-requestparameter-caching): Boolean
  [Required](#sam-function-requestparameter-required): Boolean
```

## Properties<a name="sam-property-function-requestparameter-properties"></a>

 `Caching`   <a name="sam-function-requestparameter-caching"></a>
Adds `cacheKeyParameters` section to the API Gateway OpenApi definition  
*Type*: Boolean  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Required`   <a name="sam-function-requestparameter-required"></a>
This field specifies whether a parameter is required  
*Type*: Boolean  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-requestparameter--examples"></a>

### Request Parameter<a name="sam-property-function-requestparameter--examples--request-parameter"></a>

Example of setting Request Parameters

#### YAML<a name="sam-property-function-requestparameter--examples--request-parameter--yaml"></a>

```
RequestParameters:
  - method.request.header.Authorization:
      Required: true
      Caching: true
```