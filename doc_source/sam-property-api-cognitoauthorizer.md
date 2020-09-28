# CognitoAuthorizer<a name="sam-property-api-cognitoauthorizer"></a>

Define a Amazon Cognito User Pool authorizer\.

For more information and examples, see [Controlling access to API Gateway APIs](serverless-controlling-access-to-apis.md) in the AWS Serverless Application Model Developer Guide\.

## Syntax<a name="sam-property-api-cognitoauthorizer-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-cognitoauthorizer-syntax.yaml"></a>

```
  [AuthorizationScopes](#sam-api-cognitoauthorizer-authorizationscopes): List
  [Identity](#sam-api-cognitoauthorizer-identity): CognitoAuthorizationIdentity
  [UserPoolArn](#sam-api-cognitoauthorizer-userpoolarn): String
```

## Properties<a name="sam-property-api-cognitoauthorizer-properties"></a>

 `AuthorizationScopes`   <a name="sam-api-cognitoauthorizer-authorizationscopes"></a>
List of authorization scopes for this authorizer\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Identity`   <a name="sam-api-cognitoauthorizer-identity"></a>
This property can be used to specify an `IdentitySource` in an incoming request for an authorizer  
*Type*: [CognitoAuthorizationIdentity](sam-property-api-cognitoauthorizationidentity.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `UserPoolArn`   <a name="sam-api-cognitoauthorizer-userpoolarn"></a>
Can refer to a user pool/specify a userpool arn to which you want to add this cognito authorizer  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-api-cognitoauthorizer--examples"></a>

### CognitoAuth<a name="sam-property-api-cognitoauthorizer--examples--cognitoauth"></a>

Cognito Auth Example

#### YAML<a name="sam-property-api-cognitoauthorizer--examples--cognitoauth--yaml"></a>

```
Auth:
  Authorizers:
    MyCognitoAuth:
      AuthorizationScopes:
        - scope1
        - scope2
      UserPoolArn:
        Fn::GetAtt:
          - MyCognitoUserPool
          - Arn
      Identity:
        Header: MyAuthorizationHeader
        ValidationExpression: myauthvalidationexpression
```