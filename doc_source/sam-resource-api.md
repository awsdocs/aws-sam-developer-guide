# AWS::Serverless::Api<a name="sam-resource-api"></a>

Creates a collection of Amazon API Gateway resources and methods that can be invoked through HTTPS endpoints\.

An [AWS::Serverless::Api](#sam-resource-api) resource need not be explicitly added to a AWS Serverless Application Definition template\. A resource of this type is implicitly created from the union of Api events defined on [AWS::Serverless::Function](sam-resource-function.md) resources defined in the template that do not refer to an [AWS::Serverless::Api](#sam-resource-api) resource\.

An [AWS::Serverless::Api](#sam-resource-api) resource should be used to define and document the API using OpenApi, which provides more ability to configure the underlying Amazon API Gateway resources\.

## Syntax<a name="sam-resource-api-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-resource-api-syntax.yaml"></a>

```
Type: AWS::Serverless::Api
Properties:
  [AccessLogSetting](#sam-api-accesslogsetting): [AccessLogSetting](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-accesslogsetting)
  [Auth](#sam-api-auth): [ApiAuth](sam-property-api-apiauth.md)
  [BinaryMediaTypes](#sam-api-binarymediatypes): List
  [CacheClusterEnabled](#sam-api-cacheclusterenabled): Boolean
  [CacheClusterSize](#sam-api-cacheclustersize): String
  [CanarySetting](#sam-api-canarysetting): [CanarySetting](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-canarysetting)
  [Cors](#sam-api-cors): String | [CorsConfiguration](sam-property-api-corsconfiguration.md)
  [DefinitionBody](#sam-api-definitionbody): String
  [DefinitionUri](#sam-api-definitionuri): String
  [EndpointConfiguration](#sam-api-endpointconfiguration): String
  [GatewayResponses](#sam-api-gatewayresponses): Map
  [MethodSettings](#sam-api-methodsettings): [MethodSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-methodsettings)
  [MinimumCompressionSize](#sam-api-minimumcompressionsize): Integer
  [Models](#sam-api-models): Map
  [OpenApiVersion](#sam-api-openapiversion): String
  [StageName](#sam-api-stagename): String
  [Tags](#sam-api-tags): Map
  [TracingEnabled](#sam-api-tracingenabled): Boolean
  [Variables](#sam-api-variables): Map
```

## Properties<a name="sam-resource-api-properties"></a>

 `AccessLogSetting`   <a name="sam-api-accesslogsetting"></a>
Configures Access Log Setting for a stage\.  
*Type*: [AccessLogSetting](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-accesslogsetting)  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[AccessLogSetting](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-accesslogsetting)` property of an `AWS::ApiGateway::Stage`\.

 `Auth`   <a name="sam-api-auth"></a>
Configure authorization to control access to your API Gateway API\.  
For more information about configuring access using AWS SAM see [Controlling Access to API Gateway APIs](serverless-controlling-access-to-apis.md) in the AWS Serverless Application Model Developer Guide\.  
*Type*: [ApiAuth](sam-property-api-apiauth.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `BinaryMediaTypes`   <a name="sam-api-binarymediatypes"></a>
List of MIME types that your API could return\. Use this to enable binary support for APIs\. Use \~1 instead of / in the mime types\.  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[BinaryMediaTypes](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-restapi.html#cfn-apigateway-restapi-binarymediatypes)` property of an `AWS::ApiGateway::RestApi`\. The list of BinaryMediaTypes is added to both the AWS CloudFormation resource and the OpenAPI document\.

 `CacheClusterEnabled`   <a name="sam-api-cacheclusterenabled"></a>
Indicates whether cache clustering is enabled for the stage\.  
*Type*: Boolean  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[CacheClusterEnabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-cacheclusterenabled)` property of an `AWS::ApiGateway::Stage`\.

 `CacheClusterSize`   <a name="sam-api-cacheclustersize"></a>
The stage's cache cluster size\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[CacheClusterSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-cacheclustersize)` property of an `AWS::ApiGateway::Stage`\.

 `CanarySetting`   <a name="sam-api-canarysetting"></a>
Configure a canary setting to a stage of a regular deployment\.  
*Type*: [CanarySetting](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-canarysetting)  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[CanarySetting](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-canarysetting)` property of an `AWS::ApiGateway::Stage`\.

 `Cors`   <a name="sam-api-cors"></a>
Manage Cross\-origin resource sharing \(CORS\) for all your API Gateway APIs\. Specify the domain to allow as a string or specify a dictionary with additional Cors configuration\. NOTE: Cors requires SAM to modify your OpenAPI definition\. So, it works only inline OpenApi defined with DefinitionBody\.  
For more information about CORS, see [Enable CORS for an API Gateway REST API Resource](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html) in the Amazon API Gateway Developer Guide\.\.  
*Type*: String \| [CorsConfiguration](sam-property-api-corsconfiguration.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `DefinitionBody`   <a name="sam-api-definitionbody"></a>
OpenAPI specification that describes your API\. If neither `DefinitionUri` nor `DefinitionBody` are specified, SAM will generate a `DefinitionBody` for you based on your template configuration\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[Body](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-restapi.html#cfn-apigateway-restapi-body)` property of an `AWS::ApiGateway::RestApi`\. If certain properties are provided, content may be inserted or modified into the DefinitionBody before being passed to CloudFormation\. Properties include `Auth`, `BinaryMediaTypes`, `Cors`, `GatewayResponses`, `Models`, and an `EventSource` of type Api on for a corresponding `AWS::Serverless::Function`\.

 `DefinitionUri`   <a name="sam-api-definitionuri"></a>
AWS S3 Uri, local file path, or location object of the the OpenAPI document defining the API\. The AWS S3 object this property references must be a valid OpenAPI file\. If neither `DefinitionUri` nor `DefinitionBody` are specified, SAM will generate a `DefinitionBody` for you based on your template configuration\.  
If a local file path is provided, the template must go through the workflow that includes the `sam deploy` or `sam package` command, in order for the definition to be transformed properly\.  
Intrinsic functions are not supported in external OpenApi files\. Use instead the `DefinitionBody` property with the [Include Transform](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/create-reusable-transform-function-snippets-and-add-to-your-template-with-aws-include-transform.html) to define OpenApi definition\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[BodyS3Location](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-restapi.html#cfn-apigateway-restapi-bodys3location)` property of an `AWS::ApiGateway::RestApi`\. The nested Amazon S3 properties are named differently\.

 `EndpointConfiguration`   <a name="sam-api-endpointconfiguration"></a>
Specify the type of endpoint for API endpoint\.  
Valid values are `REGIONAL`, `EDGE`, or `PRIVATE`\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[EndpointConfiguration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-restapi.html#cfn-apigateway-restapi-endpointconfiguration)` property of an `AWS::ApiGateway::RestApi`\. AWS SAM only accepts a single endpoint configuration string\.

 `GatewayResponses`   <a name="sam-api-gatewayresponses"></a>
Configures Gateway Reponses for an API\. Gateway Responses are responses returned by API Gateway, either directly or through the use of Lambda Authorizers\. For more information, see the documentation for the [Api Gateway OpenApi extension for Gateway Responses](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-gateway-responses.html)\.  
*Type*: Map  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `MethodSettings`   <a name="sam-api-methodsettings"></a>
Configures all settings for API stage including Logging, Metrics, CacheTTL, Throttling\.  
*Type*: [MethodSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-methodsettings)  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[MethodSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-methodsettings)` property of an `AWS::ApiGateway::Stage`\.

 `MinimumCompressionSize`   <a name="sam-api-minimumcompressionsize"></a>
Allow compression of response bodies based on client's Accept\-Encoding header\. Compression is triggered when response body size is greater than or equal to your configured threshold\. The maximum body size threshold is 10 MB \(10,485,760 Bytes\)\. \- The following compression types are supported: gzip, deflate, and identity\.  
*Type*: Integer  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[MinimumCompressionSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-restapi.html#cfn-apigateway-restapi-minimumcompressionsize)` property of an `AWS::ApiGateway::RestApi`\.

 `Models`   <a name="sam-api-models"></a>
The schemas to be used by your API methods\. These schemas can be described using JSON or YAML\. See the Examples section at the bottom of this page for example models\.  
*Type*: Map  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `OpenApiVersion`   <a name="sam-api-openapiversion"></a>
Version of OpenApi to use\. This can either be `2.0` for the Swagger specification, or one of the OpenApi 3\.0 versions, like `3.0.1`\. For more information about OpenAPI, see the [OpenAPI Specification](https://swagger.io/specification/)\.  
**Note**: Setting this property to any valid value will also remove the stage `Stage` that SAM creates\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `StageName`   <a name="sam-api-stagename"></a>
The name of the stage, which API Gateway uses as the first path segment in the invoke Uniform Resource Identifier \(URI\)\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is similar to the `[StageName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-stagename)` property of an `AWS::ApiGateway::Stage`\. It is required in SAM, but not required in API Gateway  
*Additional Notes*: The Implicit API has a stage name of "prod"

 `Tags`   <a name="sam-api-tags"></a>
A map \(string to string\) that specifies the tags to be added to this API Gateway stage\. Keys and values are limited to alphanumeric characters\. Keys can be 1 to 127 Unicode characters in length and cannot be prefixed with aws:\. Values can be 1 to 255 Unicode characters in length\.  
*Type*: Map  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[Tags](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-tags)` property of an `AWS::ApiGateway::Stage`\. The Tags property in SAM consists of Key:Value pairs; in CloudFormation it consists of a list of Tag objects\. When the stack is created, SAM will automatically add a `lambda:createdBy:SAM` tag to this API Gateway stage\.

 `TracingEnabled`   <a name="sam-api-tracingenabled"></a>
Indicates whether active tracing with X\-Ray is enabled for the stage\.  
*Type*: Boolean  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[TracingEnabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-tracingenabled)` property of an `AWS::ApiGateway::Stage`\.

 `Variables`   <a name="sam-api-variables"></a>
A map \(string to string\) that defines the stage variables, where the variable name is the key and the variable value is the value\. Variable names are limited to alphanumeric characters\. Values must match the following regular expression: `[A-Za-z0-9._~:/?#&=,-]+`\.  
*Type*: Map  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[Variables](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-stage.html#cfn-apigateway-stage-variables)` property of an `AWS::ApiGateway::Stage`\.

## Examples<a name="sam-resource-api--examples"></a>

### SimpleApiExample<a name="sam-resource-api--examples--simpleapiexample"></a>

A simple API definition

#### YAML<a name="sam-resource-api--examples--simpleapiexample--yaml"></a>

```
AWSTemplateFormatVersion: '2010-09-09'
Description: AWS SAM template with a simple API definition
Resources:
  ApiFunction:
    Properties:
      Events:
        ApiEvent:
          Properties:
            Method: get
            Path: /
            RestApiId:
              Ref: ApiGatewayApi
          Type: Api
      Handler: index.handler
      InlineCode: "def handler(event, context):\n    return {'body': 'Hello World!',\
        \ 'statusCode': 200}\n"
      Runtime: python3.7
    Type: AWS::Serverless::Function
  ApiGatewayApi:
    Properties:
      StageName: prod
    Type: AWS::Serverless::Api
Transform: AWS::Serverless-2016-10-31
```

### ApiCorsExample<a name="sam-resource-api--examples--apicorsexample"></a>

AWS SAM template with API defined in an external Swagger file along with Lambda integrations and CORS configurations\. See [GitHub](https://github.com/awslabs/serverless-application-model/tree/master/examples/2016-10-31/api_swagger_cors) for the full example\.

#### YAML<a name="sam-resource-api--examples--apicorsexample--yaml"></a>

```
Properties:
  Cors: '''www.example.com'''
  DefinitionBody:
    Fn::Transform:
      Name: AWS::Include
      Parameters:
        Location: s3://bucket/swagger.yaml
  StageName: Prod
Type: AWS::Serverless::Api
```

### ApiCognitoAuthExample<a name="sam-resource-api--examples--apicognitoauthexample"></a>

AWS SAM template with an API that uses AWS Cognito to authorize requests against the API\. See [GitHub](https://github.com/awslabs/serverless-application-model/tree/master/examples/2016-10-31/api_cognito_auth) for the full example\.

#### YAML<a name="sam-resource-api--examples--apicognitoauthexample--yaml"></a>

```
Properties:
  Auth:
    Authorizers:
      MyCognitoAuthorizer:
        UserPoolArn:
          Fn::GetAtt:
          - MyCognitoUserPool
          - Arn
    DefaultAuthorizer: MyCognitoAuthorizer
  Cors: '''*'''
  StageName: Prod
Type: AWS::Serverless::Api
```