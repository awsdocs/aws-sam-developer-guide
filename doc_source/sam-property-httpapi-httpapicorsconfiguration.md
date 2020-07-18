# HttpApiCorsConfiguration<a name="sam-property-httpapi-httpapicorsconfiguration"></a>

Manage cross\-origin resource sharing \(CORS\) for your HTTP APIs\. Specify the domain to allow as a string or specify a dictionary with additional Cors configuration\. NOTE: Cors requires SAM to modify your OpenAPI definition, so it only works with inline OpenApi defined in the `DefinitionBody` property\.

For more information about CORS, see [Configuring CORS for an HTTP API](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html) in the Amazon API Gateway Developer Guide\.

Note: If HttpApiCorsConfiguration is set both in OpenAPI and at the property level, AWS SAM merges them with the properties taking precedence\.

## Syntax<a name="sam-property-httpapi-httpapicorsconfiguration-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-httpapi-httpapicorsconfiguration-syntax.yaml"></a>

```
  [AllowCredentials](#sam-httpapi-httpapicorsconfiguration-allowcredentials): Boolean
  [AllowHeaders](#sam-httpapi-httpapicorsconfiguration-allowheaders): List
  [AllowMethods](#sam-httpapi-httpapicorsconfiguration-allowmethods): List
  [AllowOrigins](#sam-httpapi-httpapicorsconfiguration-alloworigins): List
  [ExposeHeaders](#sam-httpapi-httpapicorsconfiguration-exposeheaders): List
  [MaxAge](#sam-httpapi-httpapicorsconfiguration-maxage): Integer
```

## Properties<a name="sam-property-httpapi-httpapicorsconfiguration-properties"></a>

 `AllowCredentials`   <a name="sam-httpapi-httpapicorsconfiguration-allowcredentials"></a>
Specifies whether credentials are included in the CORS request\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AllowHeaders`   <a name="sam-httpapi-httpapicorsconfiguration-allowheaders"></a>
Represents a collection of allowed headers\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AllowMethods`   <a name="sam-httpapi-httpapicorsconfiguration-allowmethods"></a>
Represents a collection of allowed HTTP methods\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AllowOrigins`   <a name="sam-httpapi-httpapicorsconfiguration-alloworigins"></a>
Represents a collection of allowed origins\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ExposeHeaders`   <a name="sam-httpapi-httpapicorsconfiguration-exposeheaders"></a>
Represents a collection of exposed headers\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `MaxAge`   <a name="sam-httpapi-httpapicorsconfiguration-maxage"></a>
The number of seconds that the browser should cache preflight request results\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-httpapi-httpapicorsconfiguration--examples"></a>

### HttpApiCorsConfiguration<a name="sam-property-httpapi-httpapicorsconfiguration--examples--httpapicorsconfiguration"></a>

HTTP API Cors Configuration example\.

#### YAML<a name="sam-property-httpapi-httpapicorsconfiguration--examples--httpapicorsconfiguration--yaml"></a>

```
CorsConfiguration:
  AllowOrigins:
    - "https://example.com"
  AllowHeaders:
    - x-apigateway-header
  AllowMethods:
    - GET
  MaxAge: 600
  AllowCredentials: True
```