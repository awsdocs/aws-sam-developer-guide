# LayerContent<a name="sam-property-layerversion-layercontent"></a>

A ZIP archive that contains the contents of an [AWS Lambda layer](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html)\.

## Syntax<a name="sam-property-layerversion-layercontent-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-layerversion-layercontent-syntax.yaml"></a>

```
  [Bucket](#sam-layerversion-layercontent-bucket): String
  [Key](#sam-layerversion-layercontent-key): String
  [Version](#sam-layerversion-layercontent-version): String
```

## Properties<a name="sam-property-layerversion-layercontent-properties"></a>

 `Bucket`   <a name="sam-layerversion-layercontent-bucket"></a>
The Amazon S3 bucket of the layer archive\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[S3Bucket](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-layerversion-content.html#cfn-lambda-layerversion-content-s3bucket)` property of the `AWS::Lambda::LayerVersion` `Content` data type\.

 `Key`   <a name="sam-layerversion-layercontent-key"></a>
The Amazon S3 key of the layer archive\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[S3Key](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-layerversion-content.html#cfn-lambda-layerversion-content-s3key)` property of the `AWS::Lambda::LayerVersion` `Content` data type\.

 `Version`   <a name="sam-layerversion-layercontent-version"></a>
For versioned objects, the version of the layer archive object to use\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[S3ObjectVersion](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-layerversion-content.html#cfn-lambda-layerversion-content-s3objectversion)` property of the `AWS::Lambda::LayerVersion` `Content` data type\.

## Examples<a name="sam-property-layerversion-layercontent--examples"></a>

### LayerContent<a name="sam-property-layerversion-layercontent--examples--layercontent"></a>

Layer Content example

#### YAML<a name="sam-property-layerversion-layercontent--examples--layercontent--yaml"></a>

```
LayerContent:
  Bucket: mybucket-name
  Key: mykey-name
  Version: 121212
```