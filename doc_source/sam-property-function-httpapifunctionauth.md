# HttpApiFunctionAuth<a name="sam-property-function-httpapifunctionauth"></a>

Configures authorization at the event level\.

Configure Auth for a specific API \+ Path \+ Method

## Syntax<a name="sam-property-function-httpapifunctionauth-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-httpapifunctionauth-syntax.yaml"></a>

```
  [AuthorizationScopes](#sam-function-httpapifunctionauth-authorizationscopes): List
  [Authorizer](#sam-function-httpapifunctionauth-authorizer): String
```

## Properties<a name="sam-property-function-httpapifunctionauth-properties"></a>

 `AuthorizationScopes`   <a name="sam-function-httpapifunctionauth-authorizationscopes"></a>
The authorization scopes to apply to this API, path, and method\.  
Scopes listed here will override any scopes applied by the `DefaultAuthorizer` if one exists\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Authorizer`   <a name="sam-function-httpapifunctionauth-authorizer"></a>
The `Authorizer` for a specific Function\. To use IAM authorization, specify `AWS_IAM` and specify `true` for `EnableIamAuthorizer` in the `Globals` section of your template\.  
If you have specified a Global Authorizer on the API and want to make a specific Function public, override by setting `Authorizer` to `NONE`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-httpapifunctionauth--examples"></a>

### Function\-Auth<a name="sam-property-function-httpapifunctionauth--examples--function-auth"></a>

Specifing Authorization at Function level

#### YAML<a name="sam-property-function-httpapifunctionauth--examples--function-auth--yaml"></a>

```
Auth:
  Authorizer: OpenIdAuth
  AuthorizationScopes:
    - scope1
    - scope2
```

### IAM authorization<a name="sam-property-function-httpapifunctionauth--examples--iam-authorization"></a>

Specifies IAM authorization at the event level\. To use `AWS_IAM` authorization at the event level, you must also specify `true` for `EnableIamAuthorizer` in the `Globals` section of your template\. For more information, see [Globals section of the AWS SAM template](sam-specification-template-anatomy-globals.md)\.

#### YAML<a name="sam-property-function-httpapifunctionauth--examples--iam-authorization--yaml"></a>

```
Globals:
  HttpApi:
    Auth:
      EnableIamAuthorizer: true

Resources:
  HttpApiFunctionWithIamAuth:
    Type: AWS::Serverless::Function
    Properties:
      Events:
        ApiEvent:
          Type: HttpApi
          Properties:
            Path: /iam-auth
            Method: GET
            Auth:
              Authorizer: AWS_IAM
      Handler: index.handler
      InlineCode: |
        def handler(event, context):
          return {'body': 'HttpApiFunctionWithIamAuth', 'statusCode': 200}
      Runtime: python3.9
```