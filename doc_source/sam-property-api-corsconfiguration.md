# CorsConfiguration<a name="sam-property-api-corsconfiguration"></a>

Manage cross\-origin resource sharing \(CORS\) for your API Gateway APIs\. Specify the domain to allow as a string or specify a dictionary with additional Cors configuration\. NOTE: Cors requires SAM to modify your OpenAPI definition, so it only works with inline OpenApi defined in the `DefinitionBody` property\.

For more information about CORS, see [Enable CORS for an API Gateway REST API Resource](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html) in the Amazon API Gateway Developer Guide\.

## Syntax<a name="sam-property-api-corsconfiguration-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-api-corsconfiguration-syntax.yaml"></a>

```
  [AllowCredentials](#sam-api-corsconfiguration-allowcredentials): String
  [AllowHeaders](#sam-api-corsconfiguration-allowheaders): List
  [AllowMethods](#sam-api-corsconfiguration-allowmethods): List
  [AllowOrigin](#sam-api-corsconfiguration-alloworigin): List
  [MaxAge](#sam-api-corsconfiguration-maxage): String
```

## Properties<a name="sam-property-api-corsconfiguration-properties"></a>

 `AllowCredentials`   <a name="sam-api-corsconfiguration-allowcredentials"></a>
Boolean indicating whether request is allowed to contain credentials\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `AllowHeaders`   <a name="sam-api-corsconfiguration-allowheaders"></a>
Array of headers to allow\.  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `AllowMethods`   <a name="sam-api-corsconfiguration-allowmethods"></a>
Array containing the HTTP methods to allow\.  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `AllowOrigin`   <a name="sam-api-corsconfiguration-alloworigin"></a>
Array of origin to allow\.  
*Type*: List  
*Required*: Yes  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `MaxAge`   <a name="sam-api-corsconfiguration-maxage"></a>
String containing the number of seconds to cache CORS Preflight request\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-api-corsconfiguration--examples"></a>

### CorsConfiguration<a name="sam-property-api-corsconfiguration--examples--corsconfiguration"></a>

Cors Configuration example\.

#### YAML<a name="sam-property-api-corsconfiguration--examples--corsconfiguration--yaml"></a>

```
Cors:
  AllowCredentials: true
  AllowHeaders:
    - 'X-Forwarded-For'
  AllowMethods:
    - 'POST'
    - 'GET'
  AllowOrigin:
    - 'www.example.com'
  MaxAge: '"600"'
```
