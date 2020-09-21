# AWS::Serverless::HttpApi<a name="sam-resource-httpapi"></a>

Creates an API Gateway HTTP API, which enables you to create RESTful APIs with lower latency and lower costs than REST APIs\. For more information about HTTP APIs see [HTTP API](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html) in the API Gateway Developer Guide\.

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
  [DefinitionBody](#sam-httpapi-definitionbody): String
  [DefinitionUri](#sam-httpapi-definitionuri): String | HttpApiDefinition
  [Domain](#sam-httpapi-domain): HttpApiDomainConfiguration
  [FailOnWarnings](#sam-httpapi-failonwarnings): Boolean
  [RouteSettings](#sam-httpapi-routesettings): [RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)
  [StageName](#sam-httpapi-stagename): String
  [StageVariables](#sam-httpapi-stagevariables): [Json](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-stagevariables)
  [Tags](#sam-httpapi-tags): Map
```

## Properties<a name="sam-resource-httpapi-properties"></a>

 `AccessLogSettings`   <a name="sam-httpapi-accesslogsettings"></a>
Settings for logging access in a stage\.  
*Type*: [AccessLogSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-accesslogsettings)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[AccessLogSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-accesslogsettings)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `Auth`   <a name="sam-httpapi-auth"></a>
Configure authorization to control access to your API Gateway API\.  
For more information about configuring access see [JWT Authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html) in the API Gateway Developer Guide\.  
*Type*: [HttpApiAuth](sam-property-httpapi-httpapiauth.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `CorsConfiguration`   <a name="sam-httpapi-corsconfiguration"></a>
Manage Cross\-origin resource sharing \(CORS\) for all your HTTP APIs\. Specify the domain to allow as a string or specify a dictionary with additional Cors configuration\. NOTE: CORS requires AWS SAM to modify your OpenAPI definition\. So, it works only inline OpenApi defined with DefinitionBody\.  
For more information about CORS, see [Configuring CORS for an HTTP API](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html) in the Amazon API Gateway Developer Guide\.  
Note: If CorsConfiguration is set both in OpenAPI and at the property level, AWS SAM merges them with the properties taking precedence\.  
Note: If this property is set to `True` then all origins are allowed\.  
*Type*: String \| [HttpApiCorsConfiguration](sam-property-httpapi-httpapicorsconfiguration.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `DefaultRouteSettings`   <a name="sam-httpapi-defaultroutesettings"></a>
The default route settings for this HTTP API\. These settings apply to all routes, unless overridden by the `RouteSettings` property for certain routes\.  
*Type*: [RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `DefinitionBody`   <a name="sam-httpapi-definitionbody"></a>
OpenAPI specification that describes your API\. If neither `DefinitionUri` nor `DefinitionBody` are specified, SAM will generate a `DefinitionBody` for you based on your template configuration\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[Body](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-api.html#cfn-apigatewayv2-api-body)` property of an `AWS::ApiGatewayV2::Api` resource\. If certain properties are provided, content may be inserted or modified into the DefinitionBody before being passed to CloudFormation\. Properties include `Auth` and an `EventSource` of type HttpApi on for a corresponding `AWS::Serverless::Function`\.

 `DefinitionUri`   <a name="sam-httpapi-definitionuri"></a>
AWS S3 Uri, local file path, or location object of the the OpenAPI document defining the API\. The AWS S3 object this property references must be a valid OpenAPI file\. If neither `DefinitionUri` nor `DefinitionBody` are specified, SAM will generate a `DefinitionBody` for you based on your template configuration\.  
If a local file path is provided, the template must go through the workflow that includes the `sam deploy` or `sam package` command, in order for the definition to be transformed properly\.  
Intrinsic functions are not supported in external OpenApi files referenced by `DefinitionUri`\. Use instead the `DefinitionBody` property with the [Include Transform](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/create-reusable-transform-function-snippets-and-add-to-your-template-with-aws-include-transform.html) to import an OpenApi definition into the template\.  
*Type*: String \| [HttpApiDefinition](sam-property-httpapi-httpapidefinition.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[BodyS3Location](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-api.html#cfn-apigatewayv2-api-bodys3location)` property of an `AWS::ApiGatewayV2::Api` resource\. The nested Amazon S3 properties are named differently\.

 `Domain`   <a name="sam-httpapi-domain"></a>
Configures a custom domain for this API Gateway API\.  
*Type*: [HttpApiDomainConfiguration](sam-property-httpapi-httpapidomainconfiguration.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `FailOnWarnings`   <a name="sam-httpapi-failonwarnings"></a>
Specifies whether to rollback the API creation \(true\) or not \(false\) when a warning is encountered\. The default value is `false`\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[FailOnWarnings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-api.html#cfn-apigatewayv2-api-failonwarnings)` property of an `AWS::ApiGatewayV2::Api` resource\.

 `RouteSettings`   <a name="sam-httpapi-routesettings"></a>
The per\-route route settings for this HTTP API\. For more information about route settings, see [AWS::ApiGatewayV2::Stage RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigatewayv2-stage-routesettings.html) in the API Gateway Developer Guide\.  
*Type*: [RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RouteSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-routesettings)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `StageName`   <a name="sam-httpapi-stagename"></a>
The name of the API stage\. If a name is not given, SAM will use the `$default` stage from Api Gateway\.  
*Type*: String  
*Required*: No  
*Default*: $default  
*AWS CloudFormation compatibility*: This property is passed directly to the `[StageName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-stagename)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `StageVariables`   <a name="sam-httpapi-stagevariables"></a>
A map that defines the stage variables for a Stage\. Variable names can have alphanumeric and underscore characters, and the values must match \[A\-Za\-z0\-9\-\.\_\~:/?\#&=,\]\+\.  
*Type*: [Json](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-stagevariables)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[StageVariables](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-stage.html#cfn-apigatewayv2-stage-stagevariables)` property of an `AWS::ApiGatewayV2::Stage` resource\.

 `Tags`   <a name="sam-httpapi-tags"></a>
A map \(string to string\) that specifies the tags to be added to this API Gateway stage\. Keys and values are limited to alphanumeric characters\. Keys can be 1 to 127 Unicode characters in length and cannot be prefixed with aws:\. Values can be 1 to 255 Unicode characters in length\. NOTE: Tags requires AWS SAM to modify your OpenAPI definition\. So, it works only if inline OpenApi is defined with DefinitionBody\.  
*Type*: Map  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*Additional Notes*: Because Tags requires AWS SAM to modify your OpenAPI definition, they will only be added if the `DefinitionBody` property is specified—no tags will be added if the `DefinitionUri` property is provided\. AWS SAM automatically adds a `httpapi:createdBy:SAM` tag\. Tags will also be added to `AWS::ApiGatewayV2::Stage` and `AWS::ApiGatewayV2::DomainName` \(if `DomainName` is specified\)\.

## Return Values<a name="sam-resource-httpapi-return-values"></a>

### Ref<a name="sam-resource-httpapi-return-values-ref"></a>

When you pass the logical ID of this resource to the intrinsic `Ref` function, `Ref` returns the API ID of the underlying `AWS::ApiGatewayV2::Api` resource, such as a1bcdef2gh\.

For more information about using the `Ref` function, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html) in the *AWS CloudFormation User Guide*\. 

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
  FailOnWarnings: True
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
  FailOnWarnings: True
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

### Http Api with Configuration Settings<a name="sam-resource-httpapi--examples--http-api-with-configuration-settings"></a>

Shows how to add API and stage configurations to the template\.

#### YAML<a name="sam-resource-httpapi--examples--http-api-with-configuration-settings--yaml"></a>

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
      FailOnWarnings: True

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