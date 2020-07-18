# CorsConfiguration<a name="sam-property-api-corsconfiguration"></a>

Manage cross\-origin resource sharing \(CORS\) for your API Gateway APIs\. Specify the domain to allow as a string or specify a dictionary with additional Cors configuration\. NOTE: Cors requires SAM to modify your OpenAPI definition, so it only works with inline OpenApi defined in the `DefinitionBody` property\.

For more information about CORS, see [Enable CORS for an API Gateway REST API Resource](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html) in the Amazon API Gateway Developer Guide\.

Note: If CorsConfiguration is set both in OpenAPI and at the property level, AWS SAM merges them, with the properties taking precedence\.

## Syntax<a name="sam-property-api-corsconfiguration-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-corsconfiguration-syntax.yaml"></a>

```
  [AllowCredentials](#sam-api-corsconfiguration-allowcredentials): Boolean
  [AllowHeaders](#sam-api-corsconfiguration-allowheaders): String
  [AllowMethods](#sam-api-corsconfiguration-allowmethods): String
  [AllowOrigin](#sam-api-corsconfiguration-alloworigin): String
  [MaxAge](#sam-api-corsconfiguration-maxage): String
```

## Properties<a name="sam-property-api-corsconfiguration-properties"></a>

 `AllowCredentials`   <a name="sam-api-corsconfiguration-allowcredentials"></a>
Boolean indicating whether request is allowed to contain credentials\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AllowHeaders`   <a name="sam-api-corsconfiguration-allowheaders"></a>
String of headers to allow\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AllowMethods`   <a name="sam-api-corsconfiguration-allowmethods"></a>
String containing the HTTP methods to allow\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AllowOrigin`   <a name="sam-api-corsconfiguration-alloworigin"></a>
String of origin to allow\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `MaxAge`   <a name="sam-api-corsconfiguration-maxage"></a>
String containing the number of seconds to cache CORS Preflight request\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-api-corsconfiguration--examples"></a>

### CorsConfiguration<a name="sam-property-api-corsconfiguration--examples--corsconfiguration"></a>

Cors Configuration example\. This is just a portion of an AWS SAM template file showing an AWS::Serverless::Api definition with Cors configured\.

#### YAML<a name="sam-property-api-corsconfiguration--examples--corsconfiguration--yaml"></a>

```
Resources:
  ApiGatewayApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: Prod
      Cors:
        AllowMethods: "'POST, GET'"
        AllowHeaders: "'X-Forwarded-For'"
        AllowOrigin: "'www.example.com'"
        MaxAge: "'600'"
        AllowCredentials: True
```