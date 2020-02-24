# HttpApi<a name="sam-property-function-httpapi"></a>


|  | 
| --- |
| HTTP APIs are in beta for Amazon API Gateway and are subject to change\. | 

The object describing an event source with type HttpApi\.

If an OpenApi definition for the specified path and method exists on the API, SAM will add the Lambda integration and security section \(if applicable\) for you\.

If no OpenApi definition for the specified path and method exists on the API, SAM will create this definition for you\.

## Syntax<a name="sam-property-function-httpapi-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-function-httpapi-syntax.yaml"></a>

```
  [ApiId](#sam-function-httpapi-apiid): String
  [Auth](#sam-function-httpapi-auth): [HttpApiFunctionAuth](sam-property-function-httpapifunctionauth.md)
  [Method](#sam-function-httpapi-method): String
  [Path](#sam-function-httpapi-path): String
```

## Properties<a name="sam-property-function-httpapi-properties"></a>

 `ApiId`   <a name="sam-function-httpapi-apiid"></a>
Identifier of an [AWS::Serverless::HttpApi](sam-resource-httpapi.md) resource defined in this template\.  
If not defined, a default [AWS::Serverless::HttpApi](sam-resource-httpapi.md) resource is created called `ServerlessHttpApi` using a generated OpenApi document containing a union of all paths and methods defined by Api events defined in this template that do not specify an `ApiId`\.  
This cannot reference an [AWS::Serverless::HttpApi](sam-resource-httpapi.md) resource defined in another template\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Auth`   <a name="sam-function-httpapi-auth"></a>
Auth configuration for this specific Api\+Path\+Method\.  
Useful for overriding the API's `DefaultAuthorizer` or setting auth config on an individual path when no `DefaultAuthorizer` is specified\.  
*Type*: [HttpApiFunctionAuth](sam-property-function-httpapifunctionauth.md)  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Method`   <a name="sam-function-httpapi-method"></a>
HTTP method for which this function is invoked\.  
If no `Path` and `Method` are specified, SAM will create a default API path that routes any request that doesn't map to a different endpoint to this Lambda function\. Only one of these default paths can exist per API\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Path`   <a name="sam-function-httpapi-path"></a>
Uri path for which this function is invoked\. Must start with `/`\.  
If no `Path` and `Method` are specified, SAM will create a default API path that routes any request that doesn't map to a different endpoint to this Lambda function\. Only one of these default paths can exist per API\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

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