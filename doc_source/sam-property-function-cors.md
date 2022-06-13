# Cors<a name="sam-property-function-cors"></a>

The Cross\-Origin Resource Sharing \(CORS\) settings for your function URL\.

## Syntax<a name="sam-property-function-cors-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-cors-syntax.yaml"></a>

```
  [AllowCredentials](#sam-function-cors-allowcredentials): Boolean
  [AllowHeaders](#sam-function-cors-allowheaders): List
  [AllowMethods](#sam-function-cors-allowmethods): List
  [AllowOrigins](#sam-function-cors-alloworigins): List
  [ExposeHeaders](#sam-function-cors-exposeheaders): List
  [MaxAge](#sam-function-cors-maxage): Integer
```

## Properties<a name="sam-property-function-cors-properties"></a>

 `AllowCredentials`   <a name="sam-function-cors-allowcredentials"></a>
Whether you want to allow cookies or other credentials in requests to your function URL\. The default is `false`\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Cors](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-url-cors.html#cfn-lambda-url-cors-allowcredentials)` property of an `AWS::Lambda::Url` resource\.

 `AllowHeaders`   <a name="sam-function-cors-allowheaders"></a>
The HTTP headers that origins can include in requests to your function URL\. For example, `Date`, `Keep-Alive`, `X-Custom-Header`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Cors](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-url-cors.html#cfn-lambda-url-cors-allowheaders)` property of an `AWS::Lambda::Url` resource\.

 `AllowMethods`   <a name="sam-function-cors-allowmethods"></a>
The HTTP methods that are allowed when calling your function URL\. For example, GET, POST, DELETE, or the wildcard character \(\*\)\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Cors](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-url-cors.html#cfn-lambda-url-cors-methods)` property of an `AWS::Lambda::Url` resource\.

 `AllowOrigins`   <a name="sam-function-cors-alloworigins"></a>
The origins that can access your function URL\. You can list any number of specific origins, separated by a comma\. For example, `https://www.example.com`, `http://localhost:3000`\.  
You can grant access to all origins with the wildcard character \(`*`\)\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Cors](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-url-cors.html#cfn-lambda-url-cors-alloworigins)` property of an `AWS::Lambda::Url` resource\.

 `ExposeHeaders`   <a name="sam-function-cors-exposeheaders"></a>
The HTTP headers in your function response that you want to expose to origins that call your function URL\. For example, `Date`, `Keep-Alive`, `X-Custom-Header`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Cors](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-url-cors.html#cfn-lambda-url-cors-exposeheaders)` property of an `AWS::Lambda::Url` resource\.

 `MaxAge`   <a name="sam-function-cors-maxage"></a>
The maximum amount of time, in seconds, that browsers can cache results of a preflight request\. By default, this is set to 0, which means the browser will not cache results\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Cors](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-url-cors.html#cfn-lambda-url-cors-max-age)` property of an `AWS::Lambda::Url` resource\.

## Examples<a name="sam-property-function-cors--examples"></a>

### Function URL with CORS<a name="sam-property-function-cors--examples--function-url-with-cors"></a>

The following example creates a function URL with a CORS configuration\.

#### YAML<a name="sam-property-function-cors--examples--function-url-with-cors--yaml"></a>

```
HelloWorldFunction:
  Type: AWS::Serverless::Function
  Properties:
    CodeUri: hello_world/
    Handler: index.handler
    Runtime: nodejs14.x
    FunctionUrlConfig:
      AuthType: AWS_IAM
      Cors:
          AllowOrigins:
            - "https://example.com"
          AllowCredentials: false
          AllowMethods:
            - GET
            - POST
          AllowHeaders:
            - x-amzn-header
            - authorization
            - content-type
          ExposeHeaders:
            - date
            - content-type
          MaxAge: 30
```