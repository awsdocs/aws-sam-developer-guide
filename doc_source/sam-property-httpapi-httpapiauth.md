# HttpApiAuth<a name="sam-property-httpapi-httpapiauth"></a>

Configure authorization to control access to your API Gateway API\.

For more information about configuring access see [JWT Authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html) in the API Gateway Developer Guide\.

## Syntax<a name="sam-property-httpapi-httpapiauth-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-httpapi-httpapiauth-syntax.yaml"></a>

```
  [Authorizers](#sam-httpapi-httpapiauth-authorizers): OAuth2Authorizer
  [DefaultAuthorizer](#sam-httpapi-httpapiauth-defaultauthorizer): String
```

## Properties<a name="sam-property-httpapi-httpapiauth-properties"></a>

 `Authorizers`   <a name="sam-httpapi-httpapiauth-authorizers"></a>
The authorizer used to control access to your API Gateway API\.  
*Type*: [OAuth2Authorizer](sam-property-httpapi-oauth2authorizer.md)  
*Required*: No  
*Default*: None  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*Additional Notes*: SAM adds the Authorizers to the OpenApi definition of an Api\.

 `DefaultAuthorizer`   <a name="sam-httpapi-httpapiauth-defaultauthorizer"></a>
Specify a default authorizer for an API Gateway API, which will be used for authorizing API calls by default\.  
*Type*: String  
*Required*: No  
*Default*: None  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-httpapi-httpapiauth--examples"></a>

### OAuth2 Authorizer<a name="sam-property-httpapi-httpapiauth--examples--oauth2-authorizer"></a>

OAuth2 Authorizer Example

#### YAML<a name="sam-property-httpapi-httpapiauth--examples--oauth2-authorizer--yaml"></a>

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