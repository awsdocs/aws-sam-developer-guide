# ApiDefinition<a name="sam-property-api-apidefinition"></a>

An OpenAPI document defining the API\.

## Syntax<a name="sam-property-api-apidefinition-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-apidefinition-syntax.yaml"></a>

```
  [Bucket](#sam-api-apidefinition-bucket): String
  [Key](#sam-api-apidefinition-key): String
  [Version](#sam-api-apidefinition-version): String
```

## Properties<a name="sam-property-api-apidefinition-properties"></a>

 `Bucket`   <a name="sam-api-apidefinition-bucket"></a>
The name of the Amazon S3 bucket where the OpenAPI file is stored\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Bucket](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigateway-restapi-s3location.html#cfn-apigateway-restapi-s3location-bucket)` property of the `AWS::ApiGateway::RestApi` `S3Location` data type\.

 `Key`   <a name="sam-api-apidefinition-key"></a>
The Amazon S3 key of the OpenAPI file\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Key](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigateway-restapi-s3location.html#cfn-apigateway-restapi-s3location-key)` property of the `AWS::ApiGateway::RestApi` `S3Location` data type\.

 `Version`   <a name="sam-api-apidefinition-version"></a>
For versioned objects, the version of the OpenAPI file\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Version](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigateway-restapi-s3location.html#cfn-apigateway-restapi-s3location-version)` property of the `AWS::ApiGateway::RestApi` `S3Location` data type\.

## Examples<a name="sam-property-api-apidefinition--examples"></a>

### Definition Uri example<a name="sam-property-api-apidefinition--examples--definition-uri-example"></a>

API Definition example

#### YAML<a name="sam-property-api-apidefinition--examples--definition-uri-example--yaml"></a>

```
DefinitionUri:
  Bucket: mybucket-name
  Key: mykey-name
  Version: 121212
```