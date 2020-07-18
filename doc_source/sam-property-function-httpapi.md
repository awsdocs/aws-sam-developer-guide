# HttpApi<a name="sam-property-function-httpapi"></a>

The object describing an event source with type HttpApi\.

If an OpenApi definition for the specified path and method exists on the API, SAM will add the Lambda integration and security section \(if applicable\) for you\.

If no OpenApi definition for the specified path and method exists on the API, SAM will create this definition for you\.

## Syntax<a name="sam-property-function-httpapi-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-httpapi-syntax.yaml"></a>

```
  [ApiId](#sam-function-httpapi-apiid): String
  [Auth](#sam-function-httpapi-auth): HttpApiFunctionAuth
  [Method](#sam-function-httpapi-method): String
  [Path](#sam-function-httpapi-path): String
  [PayloadFormatVersion](#sam-function-httpapi-payloadformatversion): String
  [RouteSettings](#sam-function-httpapi-routesettings): [RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)
  [TimeoutInMillis](#sam-function-httpapi-timeoutinmillis): Integer
```

## Properties<a name="sam-property-function-httpapi-properties"></a>

 `ApiId`   <a name="sam-function-httpapi-apiid"></a>
Identifier of an [AWS::Serverless::HttpApi](sam-resource-httpapi.md) resource defined in this template\.  
If not defined, a default [AWS::Serverless::HttpApi](sam-resource-httpapi.md) resource is created called `ServerlessHttpApi` using a generated OpenApi document containing a union of all paths and methods defined by Api events defined in this template that do not specify an `ApiId`\.  
This cannot reference an [AWS::Serverless::HttpApi](sam-resource-httpapi.md) resource defined in another template\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Auth`   <a name="sam-function-httpapi-auth"></a>
Auth configuration for this specific Api\+Path\+Method\.  
Useful for overriding the API's `DefaultAuthorizer` or setting auth config on an individual path when no `DefaultAuthorizer` is specified\.  
*Type*: [HttpApiFunctionAuth](sam-property-function-httpapifunctionauth.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Method`   <a name="sam-function-httpapi-method"></a>
HTTP method for which this function is invoked\.  
If no `Path` and `Method` are specified, SAM will create a default API path that routes any request that doesn't map to a different endpoint to this Lambda function\. Only one of these default paths can exist per API\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Path`   <a name="sam-function-httpapi-path"></a>
Uri path for which this function is invoked\. Must start with `/`\.  
If no `Path` and `Method` are specified, SAM will create a default API path that routes any request that doesn't map to a different endpoint to this Lambda function\. Only one of these default paths can exist per API\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `PayloadFormatVersion`   <a name="sam-function-httpapi-payloadformatversion"></a>
Specifies the format of the payload sent to an integration\.  
NOTE: PayloadFormatVersion requires SAM to modify your OpenAPI definition, so it only works with inline OpenApi defined in the `DefinitionBody` property\.  
*Type*: String  
*Required*: No  
*Default*: 2\.0  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `RouteSettings`   <a name="sam-function-httpapi-routesettings"></a>
The per\-route route settings for this HTTP API\. For more information about route settings, see [AWS::ApiGatewayV2::Stage RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigatewayv2-stage-routesettings.html) in the API Gateway Developer Guide\.  
Note: If RouteSettings are specified in both the HttpApi resource and event source, AWS SAM merges them with the event source properties taking precedence\.  
*Type*: [RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `TimeoutInMillis`   <a name="sam-function-httpapi-timeoutinmillis"></a>
Custom timeout between 50 and 29,000 milliseconds\.  
NOTE: TimeoutInMillis requires SAM to modify your OpenAPI definition, so it only works with inline OpenApi defined in the `DefinitionBody` property\.  
*Type*: Integer  
*Required*: No  
*Default*: 5000  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-httpapi--examples"></a>

### Default HttpApi Event<a name="sam-property-function-httpapi--examples--default-httpapi-event"></a>

HttpApi Event that uses the default path\. All unmapped paths and methods on this API will route to this endpoint\.

#### YAML<a name="sam-property-function-httpapi--examples--default-httpapi-event--yaml"></a>

```
Events:
  HttpApiEvent:
    Type: HttpApi
```

### HttpApi<a name="sam-property-function-httpapi--examples--httpapi"></a>

HttpApi Event that uses a specific path and method\.

#### YAML<a name="sam-property-function-httpapi--examples--httpapi--yaml"></a>

```
Events:
  HttpApiEvent:
    Type: HttpApi
    Properties:
      Path: /
      Method: GET
```

### HttpApi Authorization<a name="sam-property-function-httpapi--examples--httpapi-authorization"></a>

HttpApi Event that uses an Authorizer\.

#### YAML<a name="sam-property-function-httpapi--examples--httpapi-authorization--yaml"></a>

```
Events:
  HttpApiEvent:
    Type: HttpApi
    Properties:
      Path: /authenticated
      Method: GET
      Auth:
        Authorizer: OpenIdAuth
        AuthorizationScopes:
          - scope1
          - scope2
```