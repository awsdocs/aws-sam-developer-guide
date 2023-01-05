# LambdaRequestAuthorizationIdentity<a name="sam-property-api-lambdarequestauthorizationidentity"></a>

This property can be used to specify an IdentitySource in an incoming request for an authorizer\. For more information about IdentitySource see the [ApiGateway Authorizer OpenApi extension](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-authorizer.html)\.

## Syntax<a name="sam-property-api-lambdarequestauthorizationidentity-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-lambdarequestauthorizationidentity-syntax.yaml"></a>

```
  [Context](#sam-api-lambdarequestauthorizationidentity-context): List
  [Headers](#sam-api-lambdarequestauthorizationidentity-headers): List
  [QueryStrings](#sam-api-lambdarequestauthorizationidentity-querystrings): List
  [ReauthorizeEvery](#sam-api-lambdarequestauthorizationidentity-reauthorizeevery): Integer
  [StageVariables](#sam-api-lambdarequestauthorizationidentity-stagevariables): List
```

## Properties<a name="sam-property-api-lambdarequestauthorizationidentity-properties"></a>

 `Context`   <a name="sam-api-lambdarequestauthorizationidentity-context"></a>
Converts the given context strings to the mapping expressions of format `context.contextString`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Headers`   <a name="sam-api-lambdarequestauthorizationidentity-headers"></a>
Converts the headers to comma\-separated string of mapping expressions of format `method.request.header.name`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `QueryStrings`   <a name="sam-api-lambdarequestauthorizationidentity-querystrings"></a>
Converts the given query strings to comma\-separated string of mapping expressions of format `method.request.querystring.queryString`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ReauthorizeEvery`   <a name="sam-api-lambdarequestauthorizationidentity-reauthorizeevery"></a>
The time\-to\-live \(TTL\) period, in seconds, that specifies how long API Gateway caches authorizer results\. If you specify a value greater than 0, API Gateway caches the authorizer responses\. By default, API Gateway sets this property to 300\. The maximum value is 3600, or 1 hour\.  
*Type*: Integer  
*Required*: No  
*Default*: 300  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `StageVariables`   <a name="sam-api-lambdarequestauthorizationidentity-stagevariables"></a>
Converts the given stage variables to comma\-separated string of mapping expressions of format `stageVariables.stageVariable`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-api-lambdarequestauthorizationidentity--examples"></a>

### LambdaRequestIdentity<a name="sam-property-api-lambdarequestauthorizationidentity--examples--lambdarequestidentity"></a>

#### YAML<a name="sam-property-api-lambdarequestauthorizationidentity--examples--lambdarequestidentity--yaml"></a>

```
Identity:
  QueryStrings:
    - auth
  Headers:
    - Authorization
  StageVariables:
    - VARIABLE
  Context:
    - authcontext
  ReauthorizeEvery: 100
```