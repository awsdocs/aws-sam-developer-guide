# OpenIdAuthorizer<a name="sam-property-httpapi-openidauthorizer"></a>


|  | 
| --- |
| HTTP APIs are in beta for Amazon API Gateway and are subject to change\. | 

Definition for an OpenIdConnect \(OIDC\) authorizer, which is built on top of the OAuth 2\.0 protocol\.

For more information about configuring access see [JWT Authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html) in the API Gateway Developer Guide\.

## Syntax<a name="sam-property-httpapi-openidauthorizer-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-httpapi-openidauthorizer-syntax.yaml"></a>

```
  [AuthorizationScopes](#sam-httpapi-openidauthorizer-authorizationscopes): List
  [IdentitySource](#sam-httpapi-openidauthorizer-identitysource): String
  [JwtConfiguration](#sam-httpapi-openidauthorizer-jwtconfiguration): Map
  [OpenIdConnectUrl](#sam-httpapi-openidauthorizer-openidconnecturl): String
```

## Properties<a name="sam-property-httpapi-openidauthorizer-properties"></a>

 `AuthorizationScopes`   <a name="sam-httpapi-openidauthorizer-authorizationscopes"></a>
List of authorization scopes for this authorizer\.  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `IdentitySource`   <a name="sam-httpapi-openidauthorizer-identitysource"></a>
Identity source expression for this authorizer\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `JwtConfiguration`   <a name="sam-httpapi-openidauthorizer-jwtconfiguration"></a>
JSON Web Token \(JWT\) configuration for this authorizer\.  
This is passed through to the `jwtConfiguration` section of a `x-amazon-apigateway-authorizer` in the `securitySchemes` section of an OpenApi document\.  
*Type*: Map  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `OpenIdConnectUrl`   <a name="sam-httpapi-openidauthorizer-openidconnecturl"></a>
URL to use to find the token issuer\. If the lookup fails using this URL, the authorizer will fall back to using the issuer in `JWTConfiguration`\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-httpapi-openidauthorizer--examples"></a>

### OpenId Authorizer<a name="sam-property-httpapi-openidauthorizer--examples--openid-authorizer"></a>

OpenId Authorizer Example

#### YAML<a name="sam-property-httpapi-openidauthorizer--examples--openid-authorizer--yaml"></a>

```
Auth:
  Authorizers:
    OpenIdAuthorizer:
      AuthorizationScopes:
      - scope1
      - scope2
      IdentitySource: $request.querystring.param
      JwtConfiguration:
        audience:
        - MyApi
        issuer: https://www.example.com/v1/connect/oidc
      OpenIdConnectUrl: https://www.example.com/v1/connect/oidc/.well-known/openid-configuration
```