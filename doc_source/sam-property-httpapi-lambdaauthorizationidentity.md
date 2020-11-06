# LambdaAuthorizationIdentity<a name="sam-property-httpapi-lambdaauthorizationidentity"></a>

Use property can be used to specify an IdentitySource in an incoming request for a Lambda authorizer\. For more information about identity sources, see [Identity sources](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-lambda-authorizer.html#http-api-lambda-authorizer.identity-sources) in the API Gateway Developer Guide\.

## Syntax<a name="sam-property-httpapi-lambdaauthorizationidentity-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-httpapi-lambdaauthorizationidentity-syntax.yaml"></a>

```
  [Context](#sam-httpapi-lambdaauthorizationidentity-context): List
  [Headers](#sam-httpapi-lambdaauthorizationidentity-headers): List
  [QueryStrings](#sam-httpapi-lambdaauthorizationidentity-querystrings): List
  [ReauthorizeEvery](#sam-httpapi-lambdaauthorizationidentity-reauthorizeevery): Integer
  [StageVariables](#sam-httpapi-lambdaauthorizationidentity-stagevariables): List
```

## Properties<a name="sam-property-httpapi-lambdaauthorizationidentity-properties"></a>

 `Context`   <a name="sam-httpapi-lambdaauthorizationidentity-context"></a>
Converts the given context strings to a list of mapping expressions in the format `$context.contextString`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Headers`   <a name="sam-httpapi-lambdaauthorizationidentity-headers"></a>
Converts the headers to a list of mapping expressions in the format `$request.header.name`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `QueryStrings`   <a name="sam-httpapi-lambdaauthorizationidentity-querystrings"></a>
Converts the given query strings to a list of mapping expressions in the format `$request.querystring.queryString`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ReauthorizeEvery`   <a name="sam-httpapi-lambdaauthorizationidentity-reauthorizeevery"></a>
The time\-to\-live \(TTL\) period, in seconds, that specifies how long API Gateway caches authorizer results\. If you specify a value greater than 0, API Gateway caches the authorizer responses\. The maximum value is 3600, or 1 hour\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `StageVariables`   <a name="sam-httpapi-lambdaauthorizationidentity-stagevariables"></a>
Converts the given stage variables to a list of mapping expressions in the format `$stageVariables.stageVariable`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-httpapi-lambdaauthorizationidentity--examples"></a>

### LambdaRequestIdentity<a name="sam-property-httpapi-lambdaauthorizationidentity--examples--lambdarequestidentity"></a>

Lambda request identity example

#### YAML<a name="sam-property-httpapi-lambdaauthorizationidentity--examples--lambdarequestidentity--yaml"></a>

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