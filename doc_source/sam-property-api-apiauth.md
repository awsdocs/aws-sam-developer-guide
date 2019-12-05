# ApiAuth<a name="sam-property-api-apiauth"></a>

Configure authorization to control access to your API Gateway API\.

For more information and examples for configuring access using AWS SAM see [Controlling Access to API Gateway APIs](serverless-controlling-access-to-apis.md) in the AWS Serverless Application Model Developer Guide\.

## Syntax<a name="sam-property-api-apiauth-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-api-apiauth-syntax.yaml"></a>

```
  [AddDefaultAuthorizerToCorsPreflight](#sam-api-apiauth-adddefaultauthorizertocorspreflight): Boolean
  [ApiKeyRequired](#sam-api-apiauth-apikeyrequired): Boolean
  [Authorizers](#sam-api-apiauth-authorizers): [CognitoAuthorizer](sam-property-api-cognitoauthorizer.md) | [LambdaTokenAuthorizer](sam-property-api-lambdatokenauthorizer.md) | [LambdaRequestAuthorizer](sam-property-api-lambdarequestauthorizer.md)
  [DefaultAuthorizer](#sam-api-apiauth-defaultauthorizer): String
  [InvokeRole](#sam-api-apiauth-invokerole): String
  [ResourcePolicy](#sam-api-apiauth-resourcepolicy): [ResourcePolicyStatement](sam-property-api-resourcepolicystatement.md)
```

## Properties<a name="sam-property-api-apiauth-properties"></a>

 `AddDefaultAuthorizerToCorsPreflight`   <a name="sam-api-apiauth-adddefaultauthorizertocorspreflight"></a>
If the `DefaultAuthorizer` and `Cors` properties are set, then setting `AddDefaultAuthorizerToCorsPreflight` will cause the default authorizer to be added to the `Options` property in the OpenAPI section\.  
*Type*: Boolean  
*Required*: No  
*Default*: True  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `ApiKeyRequired`   <a name="sam-api-apiauth-apikeyrequired"></a>
If set to true then an API key is required for all API events\. For more information about API keys see [Create and Use Usage Plans with API Keys](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html) in the API Gateway Developer Guide\.  
*Type*: Boolean  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `Authorizers`   <a name="sam-api-apiauth-authorizers"></a>
The authorizer used to control access to your API Gateway API\.  
For more information, see [Controlling Access to API Gateway APIs](serverless-controlling-access-to-apis.md) in the AWS Serverless Application Model Developer Guide\.  
*Type*: [CognitoAuthorizer](sam-property-api-cognitoauthorizer.md) \| [LambdaTokenAuthorizer](sam-property-api-lambdatokenauthorizer.md) \| [LambdaRequestAuthorizer](sam-property-api-lambdarequestauthorizer.md)  
*Required*: No  
*Default*: None  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.  
*Additional Notes*: SAM adds the Authorizers to the OpenApi definition of an Api\.

 `DefaultAuthorizer`   <a name="sam-api-apiauth-defaultauthorizer"></a>
Specify a default authorizer for an API Gateway API, which will be used for authorizing API calls by default\.  
**Note**: If the Api EventSource for the function associated with this Api is configured to use IAM Permissions, then this property must be set to `AWS_IAM`, otherwise an error will result\.  
*Type*: String  
*Required*: No  
*Default*: None  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `InvokeRole`   <a name="sam-api-apiauth-invokerole"></a>
Sets integration credentials for all resources and methods to this value\.  
Supported values: CALLER\_CREDENTIALS, NONE, IAM Role Arn\.  
`CALLER_CREDENTIALS` maps to `arn:aws:iam::*:user/*`, which uses the caller credentials to invoke the endpoint\.  
*Type*: String  
*Required*: No  
*Default*: CALLER\_CREDENTIALS  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `ResourcePolicy`   <a name="sam-api-apiauth-resourcepolicy"></a>
Configure Resource Policy for all methods and paths on an API\.  
*Type*: [ResourcePolicyStatement](sam-property-api-resourcepolicystatement.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.  
*Additional Notes*: This setting can also be defined on individual `AWS::Serverless::Function` using the [ApiFunctionAuth](sam-property-function-apifunctionauth.md)\. This is required for APIs with `EndpointConfiguration: PRIVATE`\.

## Examples<a name="sam-property-api-apiauth--examples"></a>

### CognitoAuth<a name="sam-property-api-apiauth--examples--cognitoauth"></a>

Cognito Auth Example

#### YAML<a name="sam-property-api-apiauth--examples--cognitoauth--yaml"></a>

```
Auth:
  AddDefaultAuthorizerToCorsPreflight: false
  ApiKeyRequired: false
  Authorizers:
    MyCognitoAuth:
      AuthType: COGNITO_USER_POOLS
      UserPoolArn:
        Fn::GetAtt:
        - MyUserPool
        - Arn
  DefaultAuthorizer: MyCognitoAuth
  InvokeRole: CALLER_CREDENTIALS
  ResourcePolicy:
    CustomStatements:
    - Action: execute-api:Invoke
      Condition:
        IpAddress:
          aws:SourceIp: 1.2.3.4
      Effect: Allow
      Principal: '*'
      Resource: execute-api:/Prod/PUT/get
    IpRangeBlacklist:
    - 10.20.30.40
```