# AWS::Serverless::HttpApi<a name="sam-resource-httpapi"></a>


|  | 
| --- |
| HTTP APIs are in beta for Amazon API Gateway and are subject to change\. | 

Creates an API Gateway HTTP API, which enables you to create RESTful APIs with lower latency and lower costs than REST APIs\. For more information about HTTP APIs see [HTTP API](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html) in the API Gateway Developer Guide\.

## Syntax<a name="sam-resource-httpapi-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-resource-httpapi-syntax.yaml"></a>

```
Type: AWS::Serverless::HttpApi
Properties:
  [Auth](#sam-httpapi-auth): [HttpApiAuth](sam-property-httpapi-httpapiauth.md)
  [DefinitionBody](#sam-httpapi-definitionbody): String
  [DefinitionUri](#sam-httpapi-definitionuri): String | [HttpApiDefinition](sam-property-httpapi-httpapidefinition.md)
  [StageName](#sam-httpapi-stagename): String
```

## Properties<a name="sam-resource-httpapi-properties"></a>

 `Auth`   <a name="sam-httpapi-auth"></a>
Configure authorization to control access to your API Gateway API\.  
For more information about configuring access see [JWT Authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html) in the API Gateway Developer Guide\.  
*Type*: [HttpApiAuth](sam-property-httpapi-httpapiauth.md)  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `DefinitionBody`   <a name="sam-httpapi-definitionbody"></a>
OpenAPI specification that describes your API\. If neither `DefinitionUri` nor `DefinitionBody` are specified, SAM will generate a `DefinitionBody` for you based on your template configuration\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is similar to the `[Body](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-api.html#cfn-apigatewayv2-api-body)` property of an `AWS::ApiGatewayV2::Api`\. If certain properties are provided, content may be inserted or modified into the DefinitionBody before being passed to CloudFormation\. Properties include `Auth` and an `EventSource` of type HttpApi on for a corresponding `AWS::Serverless::Function`\.

 `DefinitionUri`   <a name="sam-httpapi-definitionuri"></a>
AWS S3 Uri, local file path, or location object of the the OpenAPI document defining the API\. The AWS S3 object this property references must be a valid OpenAPI file\. If neither `DefinitionUri` nor `DefinitionBody` are specified, SAM will generate a `DefinitionBody` for you based on your template configuration\.  
If a local file path is provided, the template must go through the workflow that includes the `sam deploy` or `sam package` command, in order for the definition to be transformed properly\.  
Intrinsic functions are not supported in external OpenApi files referenced by `DefinitionUri`\. Use instead the `DefinitionBody` property with the [Include Transform](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/create-reusable-transform-function-snippets-and-add-to-your-template-with-aws-include-transform.html) to import an OpenApi definition into the template\.  
*Type*: String \| [HttpApiDefinition](sam-property-httpapi-httpapidefinition.md)  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is similar to the `[BodyS3Location](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-api.html#cfn-apigatewayv2-api-bodys3location)` property of an `AWS::ApiGatewayV2::Api`\. The nested Amazon S3 properties are named differently\.

 `StageName`   <a name="sam-httpapi-stagename"></a>
The name of the API stage\. If a name is not given, SAM will use the `$default` stage from Api Gateway\.  
*Type*: String  
*Required*: No  
*Default*: $default  
*AWS CloudFormation Compatibility*: This property is passed directly to the `[StageName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-stagename)` property of an `AWS::ApiGatewayV2::Stage`\.

## Return Values<a name="sam-resource-httpapi-return-values"></a>

### Ref<a name="sam-resource-httpapi-return-values-ref"></a>

When you pass the logical ID of this resource to the intrinsic Ref function, Ref returns the API ID of the underlying `AWS::ApiGatewayV2::Api` resource, such as a1bcdef2gh\.

For more information about using the Ref function, see [Ref](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)\. 

## Examples<a name="sam-resource-httpapi--examples"></a>

### Simple Http Api<a name="sam-resource-httpapi--examples--simple-http-api"></a>

Bare minimum needed to set up an HttpApi endpoint backed by a Lambda function\. This uses the default HTTP API that SAM creates\.

#### YAML<a name="sam-resource-httpapi--examples--simple-http-api--yaml"></a>

```
AWSTemplateFormatVersion: '2010-09-09'
Description: AWS SAM template with a simple API definition
Resources:
  ApiFunction:
    Type: AWS::Serverless::Function
    Properties:
      Events:
        ApiEvent:
          Type: HttpApi
      Handler: index.handler
      InlineCode: |
        def handler(event, context):
            return {'body': 'Hello World!', 'statusCode': 200}
      Runtime: python3.7
Transform: AWS::Serverless-2016-10-31
```

### Http Api with Auth<a name="sam-resource-httpapi--examples--http-api-with-auth"></a>

Example of how to set up authorization on API endpoints\.

#### YAML<a name="sam-resource-httpapi--examples--http-api-with-auth--yaml"></a>

```
Properties:
  Auth:
    DefaultAuthorizer: OAuth2
    Authorizers:
      OAuth2:
        AuthorizationScopes:
          - scope4
        JwtConfiguration:
          issuer: "https://www.example.com/v1/connect/oauth2"
          audience:
            - MyApi
        IdentitySource: "$request.querystring.param"
      OpenIdAuth:
        AuthorizationScopes:
          - scope1
          - scope2
        OpenIdConnectUrl: "https://www.example.com/v1/connect/oidc/.well-known/openid-configuration"
        JwtConfiguration:
          issuer: "https://www.example.com/v1/connect/oidc"
          audience:
            - MyApi
        IdentitySource: "$request.querystring.param"
```

### Http Api with OpenApi Document<a name="sam-resource-httpapi--examples--http-api-with-openapi-document"></a>

Shows how to add OpenApi to the document\.

Note that SAM will fill in any missing lambda integrations for HttpApi events that reference this API\. SAM will also add any missing paths that HttpApi events reference\.

#### YAML<a name="sam-resource-httpapi--examples--http-api-with-openapi-document--yaml"></a>

```
Properties:
  DefinitionBody:
    info:
      version: '1.0'
      title:
        Ref: AWS::StackName
    paths:
      "/":
        get:
          security:
          - OpenIdAuth:
            - scope1
            - scope2
          responses: {}
    openapi: 3.0.1
    securitySchemes:
      OpenIdAuth:
        type: openIdConnect
        x-amazon-apigateway-authorizer:
          identitySource: "$request.querystring.param"
          type: jwt
          jwtConfiguration:
            audience:
            - MyApi
            issuer: https://www.example.com/v1/connect/oidc
          openIdConnectUrl: https://www.example.com/v1/connect/oidc/.well-known/openid-configuration
```