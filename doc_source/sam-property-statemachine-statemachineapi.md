# Api<a name="sam-property-statemachine-statemachineapi"></a>

The object describing an event source with type Api\. If an [AWS::Serverless::Api](sam-resource-api.md) resource is defined, the path and method values must correspond to an operation in the OpenApi definition of the API\.

## Syntax<a name="sam-property-statemachine-statemachineapi-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-statemachine-statemachineapi-syntax.yaml"></a>

```
  [Auth](#sam-statemachine-statemachineapi-auth): [ApiStateMachineAuth](sam-property-statemachine-apistatemachineauth.md)
  [Method](#sam-statemachine-statemachineapi-method): String
  [Path](#sam-statemachine-statemachineapi-path): String
  [RestApiId](#sam-statemachine-statemachineapi-restapiid): String
```

## Properties<a name="sam-property-statemachine-statemachineapi-properties"></a>

 `Auth`   <a name="sam-statemachine-statemachineapi-auth"></a>
Auth configuration for this specific Api\+Path\+Method\.  
Useful for overriding the API's `DefaultAuthorizer` setting auth config on an individual path when no `DefaultAuthorizer` is specified or overriding the default `ApiKeyRequired` setting\.  
*Type*: [ApiStateMachineAuth](sam-property-statemachine-apistatemachineauth.md)  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Method`   <a name="sam-statemachine-statemachineapi-method"></a>
HTTP method for which this function is invoked\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Path`   <a name="sam-statemachine-statemachineapi-path"></a>
Uri path for which this function is invoked\. Must start with `/`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `RestApiId`   <a name="sam-statemachine-statemachineapi-restapiid"></a>
Identifier of a RestApi resource, which must contain an operation with the given path and method\. Typically, this is set to reference an [AWS::Serverless::Api](sam-resource-api.md) resource defined in this template\.  
If not defined, a default [AWS::Serverless::Api](sam-resource-api.md) resource is created using a generated OpenApi document containing a union of all paths and methods defined by Api events defined in this template that do not specify a `RestApiId`\.  
This cannot reference an [AWS::Serverless::Api](sam-resource-api.md) resource defined in another template\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-statemachine-statemachineapi--examples"></a>

### ApiEvent<a name="sam-property-statemachine-statemachineapi--examples--apievent"></a>

An example of Api Event

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