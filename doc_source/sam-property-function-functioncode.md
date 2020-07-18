# FunctionCode<a name="sam-property-function-functioncode"></a>

The [deployment package](https://docs.aws.amazon.com/lambda/latest/dg/deployment-package-v2.html) for a Lambda function\.

## Syntax<a name="sam-property-function-functioncode-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-functioncode-syntax.yaml"></a>

```
  [Bucket](#sam-function-functioncode-bucket): String
  [Key](#sam-function-functioncode-key): String
  [Version](#sam-function-functioncode-version): String
```

## Properties<a name="sam-property-function-functioncode-properties"></a>

 `Bucket`   <a name="sam-function-functioncode-bucket"></a>
An Amazon S3 bucket in the same AWS Region as your function\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[S3Bucket](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-code.html#cfn-lambda-function-code-s3bucket)` property of the `AWS::Lambda::Function` `Code` data type\.

 `Key`   <a name="sam-function-functioncode-key"></a>
The Amazon S3 key of the deployment package\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[S3Key](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-code.html#cfn-lambda-function-code-s3key)` property of the `AWS::Lambda::Function` `Code` data type\.

 `Version`   <a name="sam-function-functioncode-version"></a>
For versioned objects, the version of the deployment package object to use\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[S3ObjectVersion](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-code.html#cfn-lambda-function-code-s3objectversion)` property of the `AWS::Lambda::Function` `Code` data type\.

## Examples<a name="sam-property-function-functioncode--examples"></a>

### FunctionCode<a name="sam-property-function-functioncode--examples--functioncode"></a>

Function Code example

#### YAML<a name="sam-property-function-functioncode--examples--functioncode--yaml"></a>

```
FunctionCode:
  Bucket: mybucket-name
  Key: mykey-name
  Version: 121212
```