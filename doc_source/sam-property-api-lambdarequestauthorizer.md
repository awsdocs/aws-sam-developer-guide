# LambdaRequestAuthorizer<a name="sam-property-api-lambdarequestauthorizer"></a>

Configure a Lambda Authorizer to control access to your API with a Lambda function\.

For more information and examples, see [Controlling access to API Gateway APIs](serverless-controlling-access-to-apis.md) in the AWS Serverless Application Model Developer Guide\.

## Syntax<a name="sam-property-api-lambdarequestauthorizer-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-lambdarequestauthorizer-syntax.yaml"></a>

```
  [AuthorizationScopes](#sam-api-lambdarequestauthorizer-authorizationscopes): List
  [FunctionArn](#sam-api-lambdarequestauthorizer-functionarn): String
  [FunctionInvokeRole](#sam-api-lambdarequestauthorizer-functioninvokerole): String
  [FunctionPayloadType](#sam-api-lambdarequestauthorizer-functionpayloadtype): String
  [Identity](#sam-api-lambdarequestauthorizer-identity): LambdaRequestAuthorizationIdentity
```

## Properties<a name="sam-property-api-lambdarequestauthorizer-properties"></a>

 `AuthorizationScopes`   <a name="sam-api-lambdarequestauthorizer-authorizationscopes"></a>
List of authorization scopes for this authorizer\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `FunctionArn`   <a name="sam-api-lambdarequestauthorizer-functionarn"></a>
Specify the function arn of the Lambda function which provides authorization for the API\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `FunctionInvokeRole`   <a name="sam-api-lambdarequestauthorizer-functioninvokerole"></a>
Adds authorizer credentials to the OpenApi definition of the Lambda authorizer\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `FunctionPayloadType`   <a name="sam-api-lambdarequestauthorizer-functionpayloadtype"></a>
This property can be used to define the type of Lambda Authorizer for an API\.  
Supported values: `TOKEN` and `REQUEST`\.  
*Type*: String  
*Required*: No  
*Default*: `TOKEN`   
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Identity`   <a name="sam-api-lambdarequestauthorizer-identity"></a>
This property can be used to specify an `IdentitySource` in an incoming request for an authorizer  
*Type*: [LambdaRequestAuthorizationIdentity](sam-property-api-lambdarequestauthorizationidentity.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-api-lambdarequestauthorizer--examples"></a>

### LambdaRequestAuth<a name="sam-property-api-lambdarequestauthorizer--examples--lambdarequestauth"></a>

#### YAML<a name="sam-property-api-lambdarequestauthorizer--examples--lambdarequestauth--yaml"></a>

```
Authorizer:
  MyLambdaRequestAuth:
    FunctionPayloadType: REQUEST
    FunctionArn:
      Fn::GetAtt:
        - MyAuthFunction
        - Arn
    FunctionInvokeRole:
      Fn::GetAtt:
        - LambdaAuthInvokeRole
        - Arn
    Identity:
      Headers:
        - Authorization1
```