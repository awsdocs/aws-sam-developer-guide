# HttpApiDefinition<a name="sam-property-httpapi-httpapidefinition"></a>

An OpenAPI document defining the API\.

## Syntax<a name="sam-property-httpapi-httpapidefinition-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-httpapi-httpapidefinition-syntax.yaml"></a>

```
  [Bucket](#sam-httpapi-httpapidefinition-bucket): String
  [Key](#sam-httpapi-httpapidefinition-key): String
  [Version](#sam-httpapi-httpapidefinition-version): String
```

## Properties<a name="sam-property-httpapi-httpapidefinition-properties"></a>

 `Bucket`   <a name="sam-httpapi-httpapidefinition-bucket"></a>
The name of the Amazon S3 bucket where the OpenAPI file is stored\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Bucket](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigatewayv2-api-bodys3location.html#cfn-apigatewayv2-api-bodys3location-bucket)` property of the `AWS::ApiGatewayV2::Api` `BodyS3Location` data type\.

 `Key`   <a name="sam-httpapi-httpapidefinition-key"></a>
The Amazon S3 key of the OpenAPI file\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Key](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigatewayv2-api-bodys3location.html#cfn-apigatewayv2-api-bodys3location-key)` property of the `AWS::ApiGatewayV2::Api` `BodyS3Location` data type\.

 `Version`   <a name="sam-httpapi-httpapidefinition-version"></a>
For versioned objects, the version of the OpenAPI file\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Version](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigatewayv2-api-bodys3location.html#cfn-apigatewayv2-api-bodys3location-version)` property of the `AWS::ApiGatewayV2::Api` `BodyS3Location` data type\.

## Examples<a name="sam-property-httpapi-httpapidefinition--examples"></a>

### Definition Uri example<a name="sam-property-httpapi-httpapidefinition--examples--definition-uri-example"></a>

API Definition example

#### YAML<a name="sam-property-httpapi-httpapidefinition--examples--definition-uri-example--yaml"></a>

```
DefinitionUri:
  Bucket: mybucket-name
  Key: mykey-name
  Version: 121212
```