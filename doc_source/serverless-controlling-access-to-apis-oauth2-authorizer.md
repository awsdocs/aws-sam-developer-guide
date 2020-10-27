# OAuth 2\.0/JWT authorizer example<a name="serverless-controlling-access-to-apis-oauth2-authorizer"></a>

You can control access to your APIs using JWTs as part of [OpenID Connect \(OIDC\)](https://openid.net/specs/openid-connect-core-1_0.html) and [OAuth 2\.0](https://oauth.net/2/) frameworks\. To do this, you use the [HttpApiAuth](sam-property-httpapi-httpapiauth.md) data type\.

The following is an example AWS SAM template section for an OAuth 2\.0/JWT authorizer:

```
Resources:
  MyApi:
    Type: AWS::Serverless::HttpApi
    Properties:
      Auth:
        Authorizers:
          MyOauth2Authorizer:
            AuthorizationScopes:
              - scope
            IdentitySource: $request.header.Authorization
            JwtConfiguration:
              audience:
                - audience1
                - audience2
              issuer: "https://www.example.com/v1/connect/oidc"
        DefaultAuthorizer: MyOauth2Authorizer
      StageName: Prod
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: ./src
      Events:
        GetRoot:
          Properties:
            ApiId: MyApi
            Method: get
            Path: /
            PayloadFormatVersion: "2.0"
          Type: HttpApi
      Handler: index.handler
      Runtime: nodejs12.x
```

For more information about OAuth 2\.0/JWT authorizers, see [Controlling access to HTTP APIs with JWT authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html) in the *API Gateway Developer Guide*\.