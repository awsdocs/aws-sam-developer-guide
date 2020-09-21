# Api<a name="sam-property-statemachine-statemachineapi"></a>

The object describing an `Api` event source type\. If an [AWS::Serverless::Api](sam-resource-api.md) resource is defined, the path and method values must correspond to an operation in the OpenAPI definition of the API\.

## Syntax<a name="sam-property-statemachine-statemachineapi-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-statemachine-statemachineapi-syntax.yaml"></a>

```
  [Auth](#sam-statemachine-statemachineapi-auth): ApiStateMachineAuth
  [Method](#sam-statemachine-statemachineapi-method): String
  [Path](#sam-statemachine-statemachineapi-path): String
  [RestApiId](#sam-statemachine-statemachineapi-restapiid): String
```

## Properties<a name="sam-property-statemachine-statemachineapi-properties"></a>

 `Auth`   <a name="sam-statemachine-statemachineapi-auth"></a>
The authorization configuration for this API, path, and method\.  
Use this property to override the API's `DefaultAuthorizer` setting for an individual path, when no `DefaultAuthorizer` is specified, or to override the default `ApiKeyRequired` setting\.  
*Type*: [ApiStateMachineAuth](sam-property-statemachine-apistatemachineauth.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Method`   <a name="sam-statemachine-statemachineapi-method"></a>
The HTTP method for which this function is invoked\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Path`   <a name="sam-statemachine-statemachineapi-path"></a>
The URI path for which this function is invoked\. The value must start with `/`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `RestApiId`   <a name="sam-statemachine-statemachineapi-restapiid"></a>
The identifier of a `RestApi` resource, which must contain an operation with the given path and method\. Typically, this is set to reference an [AWS::Serverless::Api](sam-resource-api.md) resource that is defined in this template\.  
If you don't define this property, AWS SAM creates a default [AWS::Serverless::Api](sam-resource-api.md) resource using a generated `OpenApi` document\. That resource contains a union of all paths and methods defined by `Api` events in the same template that do not specify a `RestApiId`\.  
This property can't reference an [AWS::Serverless::Api](sam-resource-api.md) resource that is defined in another template\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-statemachine-statemachineapi--examples"></a>

### ApiEvent<a name="sam-property-statemachine-statemachineapi--examples--apievent"></a>

The following is an example of an event of the `Api` type\.

#### YAML<a name="sam-property-statemachine-statemachineapi--examples--apievent--yaml"></a>

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