# FunctionUrlConfig<a name="sam-property-function-functionurlconfig"></a>

Creates a function URL with the specified configuration parameters\. A function URL is an HTTPS endpoint that you can use to invoke your function\.

By default, the function URL uses the `$LATEST` version of your Lambda function\. If you specify an `AutoPublishAlias` for your Lambda function, the endpoint connects to the specified function alias\.

For more information, see [Function URLs](https://docs.aws.amazon.com/lambda/latest/dg/lambda-urls.html) in the *AWS Lambda Developer Guide*\.

## Syntax<a name="sam-property-function-functionurlconfig-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-functionurlconfig-syntax.yaml"></a>

```
  [AuthType](#sam-function-functionurlconfig-authtype): String
  [Cors](#sam-function-functionurlconfig-cors): Cors
```

## Properties<a name="sam-property-function-functionurlconfig-properties"></a>

 `AuthType`   <a name="sam-function-functionurlconfig-authtype"></a>
The type of authorization for your function URL\. Set to `AWS_IAM` to use IAM to authorize requests\. Set to `NONE` for open access\.  
For more information, see [Function URLs](https://docs.aws.amazon.com/lambda/latest/dg/urls-auth.html) in the *AWS Lambda Developer Guide*  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[AuthType](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-url.html#cfn-lambda-url-authorizationtype)` property of an `AWS::Lambda::FunctionUrl` resource\.

 `Cors`   <a name="sam-function-functionurlconfig-cors"></a>
The Cross\-Origin Resource Sharing \(CORS\) settings for your function URL\.  
*Type*: [Cors](sam-property-function-cors.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-functionurlconfig--examples"></a>

### Function URL<a name="sam-property-function-functionurlconfig--examples--function-url"></a>

The following example create a Lambda function with a function URL\. The function URL uses IAM authorization\.

#### YAML<a name="sam-property-function-functionurlconfig--examples--function-url--yaml"></a>

```
HelloWorldFunction:
  Type: AWS::Serverless::Function
  Properties:
    CodeUri: hello_world/
    Handler: index.handler
    Runtime: nodejs14.x
    FunctionUrlConfig:
      AuthType: AWS_IAM

Outputs:
  MyFunctionUrlEndpoint:
      Description: "My Lambda Function URL Endpoint"
      Value:
        Fn::GetAtt: HelloWorldFunctionUrl.FunctionUrl
```