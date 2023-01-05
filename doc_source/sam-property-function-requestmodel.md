# RequestModel<a name="sam-property-function-requestmodel"></a>

Configures a Request Model for a specific Api\+Path\+Method\.

## Syntax<a name="sam-property-function-requestmodel-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-requestmodel-syntax.yaml"></a>

```
  [Model](#sam-function-requestmodel-model): String
  [Required](#sam-function-requestmodel-required): Boolean
  [ValidateBody](#sam-function-requestmodel-validatebody): Boolean
  [ValidateParameters](#sam-function-requestmodel-validateparameters): Boolean
```

## Properties<a name="sam-property-function-requestmodel-properties"></a>

 `Model`   <a name="sam-function-requestmodel-model"></a>
Name of a model defined in the Models property of the [AWS::Serverless::Api](sam-resource-api.md)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Required`   <a name="sam-function-requestmodel-required"></a>
Adds a `required` property in the parameters section of the OpenApi definition for the given API endpoint\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ValidateBody`   <a name="sam-function-requestmodel-validatebody"></a>
Specifies whether API Gateway uses the `Model` to validate the request body\. For more information, see [Enable request validation in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-method-request-validation.html) in the *API Gateway Developer Guide*\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ValidateParameters`   <a name="sam-function-requestmodel-validateparameters"></a>
Specifies whether API Gateway uses the `Model` to validate request path parameters, query strings, and headers\. For more information, see [Enable request validation in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-method-request-validation.html) in the *API Gateway Developer Guide*\.  
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
  ValidateBody: true
  ValidateParameters: true
```