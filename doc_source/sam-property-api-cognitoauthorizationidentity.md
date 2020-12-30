# CognitoAuthorizationIdentity<a name="sam-property-api-cognitoauthorizationidentity"></a>

This property can be used to specify an IdentitySource in an incoming request for an authorizer\. For more information about IdentitySource see the [ApiGateway Authorizer OpenApi extension](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-authorizer.html)\.

## Syntax<a name="sam-property-api-cognitoauthorizationidentity-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-cognitoauthorizationidentity-syntax.yaml"></a>

```
  [Header](#sam-api-cognitoauthorizationidentity-header): String
  [ReauthorizeEvery](#sam-api-cognitoauthorizationidentity-reauthorizeevery): Integer
  [ValidationExpression](#sam-api-cognitoauthorizationidentity-validationexpression): String
```

## Properties<a name="sam-property-api-cognitoauthorizationidentity-properties"></a>

 `Header`   <a name="sam-api-cognitoauthorizationidentity-header"></a>
Specify the header name for Authorization in the OpenApi definition\.  
*Type*: String  
*Required*: No  
*Default*: Authorization  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ReauthorizeEvery`   <a name="sam-api-cognitoauthorizationidentity-reauthorizeevery"></a>
The time\-to\-live \(TTL\) period, in seconds, that specifies how long API Gateway caches authorizer results\. If you specify a value greater than 0, API Gateway caches the authorizer responses\. By default, API Gateway sets this property to 300\. The maximum value is 3600, or 1 hour\.  
*Type*: Integer  
*Required*: No  
*Default*: 300  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ValidationExpression`   <a name="sam-api-cognitoauthorizationidentity-validationexpression"></a>
Specify a validation expression for validating the incoming Identity  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-api-cognitoauthorizationidentity--examples"></a>

### CognitoAuthIdentity<a name="sam-property-api-cognitoauthorizationidentity--examples--cognitoauthidentity"></a>

#### YAML<a name="sam-property-api-cognitoauthorizationidentity--examples--cognitoauthidentity--yaml"></a>

```
Identity:
  Header: MyCustomAuthHeader
  ValidationExpression: Bearer.*
  ReauthorizeEvery: 30
```