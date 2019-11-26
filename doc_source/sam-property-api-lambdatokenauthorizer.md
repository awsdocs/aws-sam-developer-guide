# LambdaTokenAuthorizer<a name="sam-property-api-lambdatokenauthorizer"></a>

Configure a Lambda Authorizer to control access to your Api with a Lambda function\.

For more information and examples, see [Controlling Access to API Gateway APIs](serverless-controlling-access-to-apis.md) in the AWS Serverless Application Model Developer Guide\.

## Syntax<a name="sam-property-api-lambdatokenauthorizer-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-api-lambdatokenauthorizer-syntax.yaml"></a>

```
  [FunctionArn](#sam-api-lambdatokenauthorizer-functionarn): String
  [FunctionInvokeRole](#sam-api-lambdatokenauthorizer-functioninvokerole): String
  [FunctionPayloadType](#sam-api-lambdatokenauthorizer-functionpayloadtype): String
  [Identity](#sam-api-lambdatokenauthorizer-identity): [LambdaTokenAuthorizationIdentity](sam-property-api-lambdatokenauthorizationidentity.md)
```

## Properties<a name="sam-property-api-lambdatokenauthorizer-properties"></a>

 `FunctionArn`   <a name="sam-api-lambdatokenauthorizer-functionarn"></a>
Specify the function arn of the Lambda function which gives the authorization to Api  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `FunctionInvokeRole`   <a name="sam-api-lambdatokenauthorizer-functioninvokerole"></a>
Adds authorizer credentials to the OpenApi definition of the Lambda authorizer\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `FunctionPayloadType`   <a name="sam-api-lambdatokenauthorizer-functionpayloadtype"></a>
This property can be used to define the type of Lambda Authorizer for an Api\.  
Supported values: TOKEN and REQUEST  
*Type*: String  
*Required*: No  
*Default*: TOKEN  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `Identity`   <a name="sam-api-lambdatokenauthorizer-identity"></a>
This property can be used to specify an `IdentitySource` in an incoming request for an authorizer\.  
*Type*: [LambdaTokenAuthorizationIdentity](sam-property-api-lambdatokenauthorizationidentity.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-api-lambdatokenauthorizer--examples"></a>

### LambdaTokenAuth<a name="sam-property-api-lambdatokenauthorizer--examples--lambdatokenauth"></a>

#### YAML<a name="sam-property-api-lambdatokenauthorizer--examples--lambdatokenauth--yaml"></a>

```
Authorizers:
  MyLambdaTokenAuth:
    FunctionArn:
      Fn::GetAtt:
      - MyAuthFunction
      - Arn
    Identity:
      Header: MyCustomAuthHeader
      ReauthorizeEvery: 20
      ValidationExpression: mycustomauthexpression
```

### BasicLambdaTokenAuth<a name="sam-property-api-lambdatokenauthorizer--examples--basiclambdatokenauth"></a>

#### YAML<a name="sam-property-api-lambdatokenauthorizer--examples--basiclambdatokenauth--yaml"></a>

```
Authorizers:
  MyLambdaTokenAuth:
    FunctionArn:
      Fn::GetAtt:
      - MyAuthFunction
      - Arn
```