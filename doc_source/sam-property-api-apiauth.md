# ApiAuth<a name="sam-property-api-apiauth"></a>

Configure authorization to control access to your API Gateway API\.

For more information and examples for configuring access using AWS SAM see [Controlling access to API Gateway APIs](serverless-controlling-access-to-apis.md) in the AWS Serverless Application Model Developer Guide\.

## Syntax<a name="sam-property-api-apiauth-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-apiauth-syntax.yaml"></a>

```
  [AddDefaultAuthorizerToCorsPreflight](#sam-api-apiauth-adddefaultauthorizertocorspreflight): Boolean
  [ApiKeyRequired](#sam-api-apiauth-apikeyrequired): Boolean
  [Authorizers](#sam-api-apiauth-authorizers): CognitoAuthorizer | LambdaTokenAuthorizer | LambdaRequestAuthorizer
  [DefaultAuthorizer](#sam-api-apiauth-defaultauthorizer): String
  [InvokeRole](#sam-api-apiauth-invokerole): String
  [ResourcePolicy](#sam-api-apiauth-resourcepolicy): ResourcePolicyStatement
  [UsagePlan](#sam-api-apiauth-usageplan): ApiUsagePlan
```

## Properties<a name="sam-property-api-apiauth-properties"></a>

 `AddDefaultAuthorizerToCorsPreflight`   <a name="sam-api-apiauth-adddefaultauthorizertocorspreflight"></a>
If the `DefaultAuthorizer` and `Cors` properties are set, then setting `AddDefaultAuthorizerToCorsPreflight` will cause the default authorizer to be added to the `Options` property in the OpenAPI section\.  
*Type*: Boolean  
*Required*: No  
*Default*: True  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ApiKeyRequired`   <a name="sam-api-apiauth-apikeyrequired"></a>
If set to true then an API key is required for all API events\. For more information about API keys see [Create and Use Usage Plans with API Keys](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html) in the API Gateway Developer Guide\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Authorizers`   <a name="sam-api-apiauth-authorizers"></a>
The authorizer used to control access to your API Gateway API\.  
For more information, see [Controlling access to API Gateway APIs](serverless-controlling-access-to-apis.md) in the AWS Serverless Application Model Developer Guide\.  
*Type*: [CognitoAuthorizer](sam-property-api-cognitoauthorizer.md) \| [LambdaTokenAuthorizer](sam-property-api-lambdatokenauthorizer.md) \| [LambdaRequestAuthorizer](sam-property-api-lambdarequestauthorizer.md)  
*Required*: No  
*Default*: None  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*Additional Notes*: SAM adds the Authorizers to the OpenApi definition of an Api\.

 `DefaultAuthorizer`   <a name="sam-api-apiauth-defaultauthorizer"></a>
Specify a default authorizer for an API Gateway API, which will be used for authorizing API calls by default\.  
**Note**: If the Api EventSource for the function associated with this API is configured to use IAM Permissions, then this property must be set to `AWS_IAM`, otherwise an error will result\.  
*Type*: String  
*Required*: No  
*Default*: None  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `InvokeRole`   <a name="sam-api-apiauth-invokerole"></a>
Sets integration credentials for all resources and methods to this value\.  
Supported values: `CALLER_CREDENTIALS`, `NONE`, IAM Role Arn\.  
`CALLER_CREDENTIALS` maps to `arn:aws:iam::*:user/*`, which uses the caller credentials to invoke the endpoint\.  
*Type*: String  
*Required*: No  
*Default*: `CALLER_CREDENTIALS`   
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ResourcePolicy`   <a name="sam-api-apiauth-resourcepolicy"></a>
Configure Resource Policy for all methods and paths on an API\.  
*Type*: [ResourcePolicyStatement](sam-property-api-resourcepolicystatement.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*Additional Notes*: This setting can also be defined on individual `AWS::Serverless::Function` using the [ApiFunctionAuth](sam-property-function-apifunctionauth.md)\. This is required for APIs with `EndpointConfiguration: PRIVATE`\.

 `UsagePlan`   <a name="sam-api-apiauth-usageplan"></a>
Configures a usage plan associated with this API\. For more information about usage plans see [Create and Use Usage Plans with API Keys](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html) in the API Gateway Developer Guide\.  
This AWS SAM property generates three additional AWS CloudFormation resources when this property is set: an [AWS::ApiGateway::UsagePlan](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html), an [AWS::ApiGateway::UsagePlanKey](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplankey.html), and an [AWS::ApiGateway::ApiKey](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-apikey.html)\. For information about this scenario, see [UsagePlan property is specified](sam-specification-generated-resources-api.md#sam-specification-generated-resources-api-usage-plan)\. For general information about generated AWS CloudFormation resources, see [Generated AWS CloudFormation resources](sam-specification-generated-resources.md)\.  
*Type*: [ApiUsagePlan](sam-property-api-apiusageplan.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-api-apiauth--examples"></a>

### CognitoAuth<a name="sam-property-api-apiauth--examples--cognitoauth"></a>

Cognito Auth Example

#### YAML<a name="sam-property-api-apiauth--examples--cognitoauth--yaml"></a>

```
Auth:
  Authorizers:
    MyCognitoAuth:
     UserPoolArn:
       Fn::GetAtt:
         - MyUserPool
         - Arn
     AuthType: "COGNITO_USER_POOLS"
  DefaultAuthorizer: MyCognitoAuth
  InvokeRole: CALLER_CREDENTIALS
  AddDefaultAuthorizerToCorsPreflight: false
  ApiKeyRequired: false
  ResourcePolicy:
    CustomStatements: [{
      "Effect": "Allow",
      "Principal": "*",
      "Action": "execute-api:Invoke",
      "Resource": "execute-api:/Prod/GET/pets",
      "Condition": {
          "IpAddress": {
              "aws:SourceIp": "1.2.3.4"
          }
        }
    }]
    IpRangeBlacklist:
      - "10.20.30.40"
```