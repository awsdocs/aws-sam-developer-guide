# LambdaAuthorizer<a name="sam-property-httpapi-lambdaauthorizer"></a>

Configure a Lambda authorizer to control access to your Amazon API Gateway HTTP API with an AWS Lambda function\.

For more information and examples, see [Working with AWS Lambda authorizers for HTTP APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-lambda-authorizer.html) in the *API Gateway Developer Guide*\.

## Syntax<a name="sam-property-httpapi-lambdaauthorizer-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-httpapi-lambdaauthorizer-syntax.yaml"></a>

```
  [AuthorizerPayloadFormatVersion](#sam-httpapi-lambdaauthorizer-authorizerpayloadformatversion): String
  [EnableSimpleResponses](#sam-httpapi-lambdaauthorizer-enablesimpleresponses): Boolean
  [FunctionArn](#sam-httpapi-lambdaauthorizer-functionarn): String
  [FunctionInvokeRole](#sam-httpapi-lambdaauthorizer-functioninvokerole): String
  [Identity](#sam-httpapi-lambdaauthorizer-identity): LambdaAuthorizationIdentity
```

## Properties<a name="sam-property-httpapi-lambdaauthorizer-properties"></a>

 `AuthorizerPayloadFormatVersion`   <a name="sam-httpapi-lambdaauthorizer-authorizerpayloadformatversion"></a>
Specifies the format of the payload sent to an HTTP API Lambda authorizer\. Required for HTTP API Lambda authorizers\.  
This is passed through to the `authorizerPayloadFormatVersion` section of an `x-amazon-apigateway-authorizer` in the `securitySchemes` section of an OpenAPI definition\.  
*Valid values*: `1.0` or `2.0`  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `EnableSimpleResponses`   <a name="sam-httpapi-lambdaauthorizer-enablesimpleresponses"></a>
Specifies whether a Lambda authorizer returns a response in a simple format\. By default, a Lambda authorizer must return an AWS Identity and Access Management \(IAM\) policy\. If enabled, the Lambda authorizer can return a boolean value instead of an IAM policy\.  
This is passed through to the `enableSimpleResponses` section of an `x-amazon-apigateway-authorizer` in the `securitySchemes` section of an OpenAPI definition\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `FunctionArn`   <a name="sam-httpapi-lambdaauthorizer-functionarn"></a>
The Amazon Resource Name \(ARN\) of the Lambda function that provides authorization for the API\.  
This is passed through to the `authorizerUri` section of an `x-amazon-apigateway-authorizer` in the `securitySchemes` section of an OpenAPI definition\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `FunctionInvokeRole`   <a name="sam-httpapi-lambdaauthorizer-functioninvokerole"></a>
The ARN of the IAM role that has the credentials required to invoke the authorizer\.  
This is passed through to the `authorizerCredentials` section of an `x-amazon-apigateway-authorizer` in the `securitySchemes` section of an OpenAPI definition\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Identity`   <a name="sam-httpapi-lambdaauthorizer-identity"></a>
Specifies an `IdentitySource` in an incoming request for an authorizer\.  
This is passed through to the `identitySource` section of an `x-amazon-apigateway-authorizer` in the `securitySchemes` section of an OpenAPI definition\.  
*Type*: [LambdaAuthorizationIdentity](sam-property-httpapi-lambdaauthorizationidentity.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-httpapi-lambdaauthorizer--examples"></a>

### LambdaAuthorizer<a name="sam-property-httpapi-lambdaauthorizer--examples--lambdaauthorizer"></a>

LambdaAuthorizer example

#### YAML<a name="sam-property-httpapi-lambdaauthorizer--examples--lambdaauthorizer--yaml"></a>

```
Auth:
  Authorizers:
    MyLambdaAuthorizer:
      AuthorizerPayloadFormatVersion: 2.0
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
          - Authorization
```
