# Api<a name="sam-property-function-api"></a>

The object describing an `Api` event source type\. If an [AWS::Serverless::Api](sam-resource-api.md) resource is defined, the path and method values must correspond to an operation in the OpenAPI definition of the API\.

If no [AWS::Serverless::Api](sam-resource-api.md) is defined, the function input and output are a representation of the HTTP request and HTTP response\.

For example, using the JavaScript API, the status code and body of the response can be controlled by returning an object with the keys statusCode and body\.

## Syntax<a name="sam-property-function-api-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-api-syntax.yaml"></a>

```
  [Auth](#sam-function-api-auth): ApiFunctionAuth
  [Method](#sam-function-api-method): String
  [Path](#sam-function-api-path): String
  [RequestModel](#sam-function-api-requestmodel): RequestModel
  [RequestParameters](#sam-function-api-requestparameters): String | RequestParameter
  [RestApiId](#sam-function-api-restapiid): String
```

## Properties<a name="sam-property-function-api-properties"></a>

 `Auth`   <a name="sam-function-api-auth"></a>
Auth configuration for this specific Api\+Path\+Method\.  
Useful for overriding the API's `DefaultAuthorizer` setting auth config on an individual path when no `DefaultAuthorizer` is specified or overriding the default `ApiKeyRequired` setting\.  
*Type*: [ApiFunctionAuth](sam-property-function-apifunctionauth.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Method`   <a name="sam-function-api-method"></a>
HTTP method for which this function is invoked\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Path`   <a name="sam-function-api-path"></a>
Uri path for which this function is invoked\. Must start with `/`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `RequestModel`   <a name="sam-function-api-requestmodel"></a>
Request model to use for this specific Api\+Path\+Method\. This should reference the name of a model specified in the `Models` section of an [AWS::Serverless::Api](sam-resource-api.md) resource\.  
*Type*: [RequestModel](sam-property-function-requestmodel.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `RequestParameters`   <a name="sam-function-api-requestparameters"></a>
Request parameters configuration for this specific Api\+Path\+Method\. All parameter names must start with `method.request` and must be limited to `method.request.header`, `method.request.querystring`, or `method.request.path`\.  
If a parameter is a string and not a Function Request Parameter Object, then `Required` and `Caching` will default to False\.  
*Type*: String \| [RequestParameter](sam-property-function-requestparameter.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `RestApiId`   <a name="sam-function-api-restapiid"></a>
Identifier of a RestApi resource, which must contain an operation with the given path and method\. Typically, this is set to reference an [AWS::Serverless::Api](sam-resource-api.md) resource defined in this template\.  
If you don't define this property, AWS SAM creates a default [AWS::Serverless::Api](sam-resource-api.md) resource using a generated `OpenApi` document\. That resource contains a union of all paths and methods defined by `Api` events in the same template that do not specify a `RestApiId`\.  
This cannot reference an [AWS::Serverless::Api](sam-resource-api.md) resource defined in another template\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-api--examples"></a>

### ApiEvent<a name="sam-property-function-api--examples--apievent"></a>

An example of Api Event

#### YAML<a name="sam-property-function-api--examples--apievent--yaml"></a>

```
Events:
  ApiEvent:
    Type: Api
    Properties:
      Path: /path
      Method: get
      RequestParameters:
        - method.request.header.Authorization
```