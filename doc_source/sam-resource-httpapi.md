# AWS::Serverless::HttpApi<a name="sam-resource-httpapi"></a>

Creates an Amazon API Gateway HTTP API, which enables you to create RESTful APIs with lower latency and lower costs than REST APIs\. For more information, see [Working with HTTP APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html) in the *API Gateway Developer Guide*\.

We recommend that you use AWS CloudFormation hooks or IAM policies to verify that API Gateway resources have authorizers attached to them to control access to them\.

For more information about using AWS CloudFormation hooks, see [Registering hooks](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/registering-hook-python.html) in the *AWS CloudFormation CLI user guide* and the [apigw\-enforce\-authorizer](https://github.com/aws-cloudformation/aws-cloudformation-samples/tree/main/hooks/python-hooks/apigw-enforce-authorizer/) GitHub repository\.

For more information about using IAM policies, see [Require that API routes have authorization](https://docs.aws.amazon.com/apigateway/latest/developerguide/security_iam_id-based-policy-examples.html#security_iam_id-based-policy-examples-require-authorization) in the *API Gateway Developer Guide*\.

## Syntax<a name="sam-resource-httpapi-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-resource-httpapi-syntax.yaml"></a>

```
Type: AWS::Serverless::HttpApi
Properties:
  [AccessLogSettings](#sam-httpapi-accesslogsettings): [AccessLogSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-accesslogsettings)
  [Auth](#sam-httpapi-auth): HttpApiAuth
  [CorsConfiguration](#sam-httpapi-corsconfiguration): String | HttpApiCorsConfiguration
  [DefaultRouteSettings](#sam-httpapi-defaultroutesettings): [RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)
  [DefinitionBody](#sam-httpapi-definitionbody): JSON
  [DefinitionUri](#sam-httpapi-definitionuri): String | HttpApiDefinition
  [Description](#sam-httpapi-description): String
  [DisableExecuteApiEndpoint](#sam-httpapi-disableexecuteapiendpoint): Boolean
  [Domain](#sam-httpapi-domain): HttpApiDomainConfiguration
  [FailOnWarnings](#sam-httpapi-failonwarnings): Boolean
  [RouteSettings](#sam-httpapi-routesettings): [RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)
  [StageName](#sam-httpapi-stagename): String
  [StageVariables](#sam-httpapi-stagevariables): [Json](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-stagevariables)
  [Tags](#sam-httpapi-tags): Map
```

## Properties<a name="sam-resource-httpapi-properties"></a>

 `AccessLogSettings`   <a name="sam-httpapi-accesslogsettings"></a>
The settings for access logging in a stage\.  
*Type*: [AccessLogSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-accesslogsettings)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[AccessLogSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-accesslogsettings)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `Auth`   <a name="sam-httpapi-auth"></a>
Configures authorization for controlling access to your API Gateway HTTP API\.  
For more information, see [Controlling access to HTTP APIs with JWT authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html) in the *API Gateway Developer Guide*\.  
*Type*: [HttpApiAuth](sam-property-httpapi-httpapiauth.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `CorsConfiguration`   <a name="sam-httpapi-corsconfiguration"></a>
Manages cross\-origin resource sharing \(CORS\) for all your API Gateway HTTP APIs\. Specify the domain to allow as a string, or specify an `HttpApiCorsConfiguration` object\. Note that CORS requires AWS SAM to modify your OpenAPI definition, so CORS works only if the `DefinitionBody` property is specified\.  
For more information, see [Configuring CORS for an HTTP API](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html) in the *API Gateway Developer Guide*\.  
If `CorsConfiguration` is set both in an OpenAPI definition and at the property level, then AWS SAM merges both configuration sources with the properties taking precedence\. If this property is set to `true`, then all origins are allowed\.
*Type*: String \| [HttpApiCorsConfiguration](sam-property-httpapi-httpapicorsconfiguration.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `DefaultRouteSettings`   <a name="sam-httpapi-defaultroutesettings"></a>
The default route settings for this HTTP API\. These settings apply to all routes unless overridden by the `RouteSettings` property for certain routes\.  
*Type*: [RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `DefinitionBody`   <a name="sam-httpapi-definitionbody"></a>
The OpenAPI definition that describes your HTTP API\. If you don't specify a `DefinitionUri` or a `DefinitionBody`, AWS SAM generates a `DefinitionBody` for you based on your template configuration\.  
*Type*: JSON  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[Body](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-api.html#cfn-apigatewayv2-api-body)` property of an `AWS::ApiGatewayV2::Api` resource\. If certain properties are provided, AWS SAM may insert content into or modify the `DefinitionBody` before it is passed to AWS CloudFormation\. Properties include `Auth` and an `EventSource` of type HttpApi for a corresponding `AWS::Serverless::Function` resource\.

 `DefinitionUri`   <a name="sam-httpapi-definitionuri"></a>
The Amazon Simple Storage Service \(Amazon S3\) URI, local file path, or location object of the the OpenAPI definition that defines the HTTP API\. The Amazon S3 object that this property references must be a valid OpenAPI definition file\. If you don't specify a `DefinitionUri` or a `DefinitionBody` are specified, AWS SAM generates a `DefinitionBody` for you based on your template configuration\.  
If you provide a local file path, the template must go through the workflow that includes the `sam deploy` or `sam package` command for the definition to be transformed properly\.  
Intrinsic functions are not supported in external OpenApi definition files that you reference with `DefinitionUri`\. To import an OpenApi definition into the template, use the `DefinitionBody` property with the [Include transform](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/create-reusable-transform-function-snippets-and-add-to-your-template-with-aws-include-transform.html)\.  
*Type*: String \| [HttpApiDefinition](sam-property-httpapi-httpapidefinition.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[BodyS3Location](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-api.html#cfn-apigatewayv2-api-bodys3location)` property of an `AWS::ApiGatewayV2::Api` resource\. The nested Amazon S3 properties are named differently\.

 `Description`   <a name="sam-httpapi-description"></a>
A description of the HttpApi resource\.  
This property requires AWS SAM to modify the HttpApi resource's OpenAPI definition, to set the `description` field\. The following two scenarios result in an error: 1\) The `DefinitionBody` property is specified with the `description` field set in the OpenAPI definition \(since this is a conflict that AWS SAM won't resolve\), or 2\) The `DefinitionUri` property is specified \(since AWS SAM won't modify an OpenAPI definition that it retrieves from Amazon S3\)\.
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `DisableExecuteApiEndpoint`   <a name="sam-httpapi-disableexecuteapiendpoint"></a>
Specifies whether clients can invoke your HTTP API by using the default `execute-api` endpoint `https://{api_id}.execute-api.{region}.amazonaws.com`\. By default, clients can invoke your API with the default endpoint\. To require that clients only use a custom domain name to invoke your API, disable the default endpoint\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[DisableExecuteApiEndpoint](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-api.html#cfn-apigatewayv2-api-disableexecuteapiendpoint)` property of an `AWS::ApiGatewayV2::Api` resource\.

 `Domain`   <a name="sam-httpapi-domain"></a>
Configures a custom domain for this API Gateway HTTP API\.  
*Type*: [HttpApiDomainConfiguration](sam-property-httpapi-httpapidomainconfiguration.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `FailOnWarnings`   <a name="sam-httpapi-failonwarnings"></a>
Specifies whether to roll back the HTTP API creation \(`true`\) or not \(`false`\) when a warning is encountered\. The default value is `false`\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[FailOnWarnings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-api.html#cfn-apigatewayv2-api-failonwarnings)` property of an `AWS::ApiGatewayV2::Api` resource\.

 `RouteSettings`   <a name="sam-httpapi-routesettings"></a>
The route settings, per route, for this HTTP API\. For more information, see [Working with routes for HTTP APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-develop-routes.html) in the *API Gateway Developer Guide*\.  
*Type*: [RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `StageName`   <a name="sam-httpapi-stagename"></a>
The name of the API stage\. If no name is specified, AWS SAM uses the `$default` stage from API Gateway\.  
*Type*: String  
*Required*: No  
*Default*: $default  
*AWS CloudFormation compatibility*: This property is passed directly to the `[StageName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-stagename)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `StageVariables`   <a name="sam-httpapi-stagevariables"></a>
A map that defines the stage variables\. Variable names can have alphanumeric and underscore characters\. The values must match \[A\-Za\-z0\-9\-\.\_\~:/?\#&=,\]\+\.  
*Type*: [Json](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-stagevariables)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[StageVariables](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-stagevariables)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `Tags`   <a name="sam-httpapi-tags"></a>
A map \(string to string\) that specifies the tags to add to this API Gateway stage\. Keys can be 1 to 128 Unicode characters in length and cannot include the prefix `aws:`\. You can use any of the following characters: the set of Unicode letters, digits, whitespace, `_`, `.`, `/`, `=`, `+`, and `-`\. Values can be 1 to 256 Unicode characters in length\.  
*Type*: Map  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*Additional notes*: The `Tags` property requires AWS SAM to modify your OpenAPI definition, so tags are added only if the `DefinitionBody` property is specified—no tags are added if the `DefinitionUri` property is specified\. AWS SAM automatically adds an `httpapi:createdBy:SAM` tag\. Tags are also added to the `AWS::ApiGatewayV2::Stage` resource and the `AWS::ApiGatewayV2::DomainName` resource \(if `DomainName` is specified\)\.

## Return Values<a name="sam-resource-httpapi-return-values"></a>

### Ref<a name="sam-resource-httpapi-return-values-ref"></a>

When you pass the logical ID of this resource to the intrinsic `Ref` function, `Ref` returns the API ID of the underlying `AWS::ApiGatewayV2::Api` resource, for example, `a1bcdef2gh`\.

For more information about using the `Ref` function, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html) in the *AWS CloudFormation User Guide*\. 

## Examples<a name="sam-resource-httpapi--examples"></a>

### Simple HttpApi<a name="sam-resource-httpapi--examples--simple-httpapi"></a>

The following example shows the minimum needed to set up an HTTP API endpoint backed by an Lambda function\. This example uses the default HTTP API that AWS SAM creates\.

#### YAML<a name="sam-resource-httpapi--examples--simple-httpapi--yaml"></a>

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

### HttpApi with Auth<a name="sam-resource-httpapi--examples--httpapi-with-auth"></a>

The following example shows how to set up authorization on HTTP API endpoints\.

#### YAML<a name="sam-resource-httpapi--examples--httpapi-with-auth--yaml"></a>

```
Properties:
  FailOnWarnings: true
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
```

### HttpApi with OpenAPI definition<a name="sam-resource-httpapi--examples--httpapi-with-openapi-definition"></a>

The following example shows how to add an OpenAPI definition to the template\.

Note that AWS SAM fills in any missing Lambda integrations for HttpApi events that reference this HTTP API\. AWS SAM also also adds any missing paths that HttpApi events reference\.

#### YAML<a name="sam-resource-httpapi--examples--httpapi-with-openapi-definition--yaml"></a>

```
Properties:
  FailOnWarnings: true
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

### HttpApi with configuration settings<a name="sam-resource-httpapi--examples--httpapi-with-configuration-settings"></a>

The following example shows how to add HTTP API and stage configurations to the template\.

#### YAML<a name="sam-resource-httpapi--examples--httpapi-with-configuration-settings--yaml"></a>

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Parameters:
  StageName:
    Type: String
    Default: Prod
    
Resources:
  HttpApiFunction:
    Type: AWS::Serverless::Function
    Properties:
      InlineCode: |
          def handler(event, context):
              import json
              return {
                  "statusCode": 200,
                  "body": json.dumps(event),
              }
      Handler: index.handler
      Runtime: python3.7
      Events:
        ExplicitApi: # warning: creates a public endpoint
          Type: HttpApi
          Properties:
            ApiId: !Ref HttpApi
            Method: GET
            Path: /path
            TimeoutInMillis: 15000
            PayloadFormatVersion: "2.0"
            RouteSettings:
              ThrottlingBurstLimit: 600

  HttpApi:
    Type: AWS::Serverless::HttpApi
    Properties:
      StageName: !Ref StageName
      Tags:
        Tag: Value
      AccessLogSettings:
        DestinationArn: !GetAtt AccessLogs.Arn
        Format: $context.requestId
      DefaultRouteSettings:
        ThrottlingBurstLimit: 200
      RouteSettings:
        "GET /path":
          ThrottlingBurstLimit: 500 # overridden in HttpApi Event
      StageVariables:
        StageVar: Value
      FailOnWarnings: true

  AccessLogs:
    Type: AWS::Logs::LogGroup

Outputs:
  HttpApiUrl:
    Description: URL of your API endpoint
    Value:
      Fn::Sub: 'https://${HttpApi}.execute-api.${AWS::Region}.${AWS::URLSuffix}/${StageName}/'
  HttpApiId:
    Description: Api id of HttpApi
    Value:
      Ref: HttpApi
```