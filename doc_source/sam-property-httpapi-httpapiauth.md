# HttpApiAuth<a name="sam-property-httpapi-httpapiauth"></a>

Configure authorization to control access to your Amazon API Gateway HTTP API\.

For more information about configuring access to HTTP APIs, see [Controlling and managing access to an HTTP API in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-access-control.html) in the API Gateway Developer Guide\.

## Syntax<a name="sam-property-httpapi-httpapiauth-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-httpapi-httpapiauth-syntax.yaml"></a>

```
  [Authorizers](#sam-httpapi-httpapiauth-authorizers): OAuth2Authorizer | LambdaAuthorizer
  [DefaultAuthorizer](#sam-httpapi-httpapiauth-defaultauthorizer): String
```

## Properties<a name="sam-property-httpapi-httpapiauth-properties"></a>

 `Authorizers`   <a name="sam-httpapi-httpapiauth-authorizers"></a>
The authorizer used to control access to your API Gateway API\.  
*Type*: [OAuth2Authorizer](sam-property-httpapi-oauth2authorizer.md) \| [LambdaAuthorizer](sam-property-httpapi-lambdaauthorizer.md)  
*Required*: No  
*Default*: None  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*Additional notes*: AWS SAM adds the authorizers to the OpenAPI definition\.

 `DefaultAuthorizer`   <a name="sam-httpapi-httpapiauth-defaultauthorizer"></a>
Specify the default authorizer to use for authorizing API calls to your API Gateway API\.  
*Type*: String  
*Required*: No  
*Default*: None  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-httpapi-httpapiauth--examples"></a>

### OAuth 2\.0 Authorizer<a name="sam-property-httpapi-httpapiauth--examples--oauth-2.0-authorizer"></a>

OAuth 2\.0 authorizer example

#### YAML<a name="sam-property-httpapi-httpapiauth--examples--oauth-2.0-authorizer--yaml"></a>

```
Auth:
  Authorizers:
    OAuth2Authorizer:
      AuthorizationScopes:
        - scope1
        - scope2
      JwtConfiguration:
        issuer: "https://www.example.com/v1/connect/oauth2"
        audience:
          - MyApi
      IdentitySource: "$request.querystring.param"
  DefaultAuthorizer: OAuth2Authorizer
```