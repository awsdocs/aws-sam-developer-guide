# OAuth2Authorizer<a name="sam-property-httpapi-oauth2authorizer"></a>

Definition for an OAuth 2\.0 authorizer, also known to as a JSON Web Token \(JWT\) authorizer\.

For more information, see [Controlling access to HTTP APIs with JWT authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html) in the *API Gateway Developer Guide*\.

## Syntax<a name="sam-property-httpapi-oauth2authorizer-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-httpapi-oauth2authorizer-syntax.yaml"></a>

```
  [AuthorizationScopes](#sam-httpapi-oauth2authorizer-authorizationscopes): List
  [IdentitySource](#sam-httpapi-oauth2authorizer-identitysource): String
  [JwtConfiguration](#sam-httpapi-oauth2authorizer-jwtconfiguration): Map
```

## Properties<a name="sam-property-httpapi-oauth2authorizer-properties"></a>

 `AuthorizationScopes`   <a name="sam-httpapi-oauth2authorizer-authorizationscopes"></a>
List of authorization scopes for this authorizer\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `IdentitySource`   <a name="sam-httpapi-oauth2authorizer-identitysource"></a>
Identity source expression for this authorizer\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `JwtConfiguration`   <a name="sam-httpapi-oauth2authorizer-jwtconfiguration"></a>
JWT configuration for this authorizer\.  
This is passed through to the `jwtConfiguration` section of an `x-amazon-apigateway-authorizer` in the `securitySchemes` section of an OpenAPI definition\.  
Properties `issuer` and `audience` are case insensitive and can be used either lowercase as in OpenAPI or uppercase `Issuer` and `Audience` as in [ AWS::ApiGatewayV2::Authorizer](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigatewayv2-authorizer-jwtconfiguration.html)\. 
*Type*: Map  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-httpapi-oauth2authorizer--examples"></a>

### OAuth 2\.0 authorizer<a name="sam-property-httpapi-oauth2authorizer--examples--oauth-2.0-authorizer"></a>

OAuth 2\.0 authorizer Example

#### YAML<a name="sam-property-httpapi-oauth2authorizer--examples--oauth-2.0-authorizer--yaml"></a>

```
Auth:
  Authorizers:
    OAuth2Authorizer:
      AuthorizationScopes:
        - scope1
      JwtConfiguration:
        issuer: "https://www.example.com/v1/connect/oauth2"
        audience:
          - MyApi
      IdentitySource: "$request.querystring.param"
  DefaultAuthorizer: OAuth2Authorizer
```