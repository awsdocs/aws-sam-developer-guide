# FunctionUrlConfig<a name="sam-property-function-functionurlconfig"></a>

Creates an AWS Lambda function URL with the specified configuration parameters\. A Lambda function URL is an HTTPS endpoint that you can use to invoke your function\.

By default, the function URL that you create uses the `$LATEST` version of your Lambda function\. If you specify an `AutoPublishAlias` for your Lambda function, the endpoint connects to the specified function alias\.

For more information, see [Lambda function URLs](https://docs.aws.amazon.com/lambda/latest/dg/lambda-urls.html) in the *AWS Lambda Developer Guide*\.

## Syntax<a name="sam-property-function-functionurlconfig-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-functionurlconfig-syntax.yaml"></a>

```
[AuthType](#sam-function-functionurlconfig-authtype): String
[Cors](#sam-function-functionurlconfig-cors): [Cors](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-url-cors.html)
[InvokeMode](#sam-function-functionurlconfig-invokemode): String
```

## Properties<a name="sam-property-function-functionurlconfig-properties"></a>

 `AuthType`   <a name="sam-function-functionurlconfig-authtype"></a>
The type of authorization for your function URL\. To use AWS Identity and Access Management \(IAM\) to authorize requests, set to `AWS_IAM`\. For open access, set to `NONE`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[AuthType](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-url.html#cfn-lambda-url-authtype)` property of an `AWS::Lambda::Url` resource\.

 `Cors`   <a name="sam-function-functionurlconfig-cors"></a>
The cross\-origin resource sharing \(CORS\) settings for your function URL\.  
*Type*: [Cors](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-url-cors.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Cors](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-url-cors.html)` property of an `AWS::Lambda::Url` resource\.

 `InvokeMode`  <a name="sam-function-functionurlconfig-invokemode"></a>
The mode that your function URL will be invoked\. To have your function return the response after invocation completes, set to `BUFFERED`\. To have your function stream the response, set to `RESPONSE_STREAM`\. The default value is `BUFFERED`\.  
*Valid values*: `BUFFERED` or `RESPONSE_STREAM`  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-url.html#cfn-lambda-url-invokemode](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-url.html#cfn-lambda-url-invokemode) property of an `AWS::Lambda::Url` resource\.

## Examples<a name="sam-property-function-functionurlconfig--examples"></a>

### Function URL<a name="sam-property-function-functionurlconfig--examples--function-url"></a>

The following example creates a Lambda function with a function URL\. The function URL uses IAM authorization\.

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
      InvokeMode: RESPONSE_STREAM

Outputs:
  MyFunctionUrlEndpoint:
      Description: "My Lambda Function URL Endpoint"
      Value:
        Fn::GetAtt: HelloWorldFunctionUrl.FunctionUrl
```