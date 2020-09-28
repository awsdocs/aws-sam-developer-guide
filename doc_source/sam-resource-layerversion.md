# AWS::Serverless::LayerVersion<a name="sam-resource-layerversion"></a>

Creates a Lambda LayerVersion that contains library or runtime code needed by a Lambda Function\.

The [AWS::Serverless::LayerVersion](#sam-resource-layerversion) resource also supports the `Metadata` resource attribute, so you can instruct AWS SAM to build layers included in your application\. For more information about building layers, see [Building layers](building-layers.md)\.

**Important Note**: Since the release of the [UpdateReplacePolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-updatereplacepolicy.html) resource attribute in AWS CloudFormation, [AWS::Lambda::LayerVersion](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-layerversion.html) \(recommended\) offers the same benefits as [AWS::Serverless::LayerVersion](#sam-resource-layerversion)\.

When a Serverless LayerVersion is transformed, SAM also transforms the logical id of the resource so that old LayerVersions are not automatically deleted by CloudFormation when the resource is updated\.

## Syntax<a name="sam-resource-layerversion-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-resource-layerversion-syntax.yaml"></a>

```
Type: AWS::Serverless::LayerVersion
Properties:
  [CompatibleRuntimes](#sam-layerversion-compatibleruntimes): List
  [ContentUri](#sam-layerversion-contenturi): String | LayerContent
  [Description](#sam-layerversion-description): String
  [LayerName](#sam-layerversion-layername): String
  [LicenseInfo](#sam-layerversion-licenseinfo): String
  [RetentionPolicy](#sam-layerversion-retentionpolicy): String
```

## Properties<a name="sam-resource-layerversion-properties"></a>

 `CompatibleRuntimes`   <a name="sam-layerversion-compatibleruntimes"></a>
List of runtimes compatible with this LayerVersion\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[CompatibleRuntimes](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-layerversion.html#cfn-lambda-layerversion-compatibleruntimes)` property of an `AWS::Lambda::LayerVersion` resource\.

 `ContentUri`   <a name="sam-layerversion-contenturi"></a>
AWS S3 Uri, local file path, or LayerContent object of the layer code\.  
If an AWS S3 Uri or LayerContent object is provided, The AWS S3 object referenced must be a valid ZIP archive that contains the contents of an [AWS Lambda layer](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html)\.  
If a local file path is provided, the template must go through the workflow that includes the `sam deploy` or `sam package` command, in order for the content to be transformed properly\.  
*Type*: String \| [LayerContent](sam-property-layerversion-layercontent.md)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is similar to the `[Content](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-layerversion.html#cfn-lambda-layerversion-content)` property of an `AWS::Lambda::LayerVersion` resource\. The nested Amazon S3 properties are named differently\.

 `Description`   <a name="sam-layerversion-description"></a>
Description of this layer\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Description](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-layerversion.html#cfn-lambda-layerversion-description)` property of an `AWS::Lambda::LayerVersion` resource\.

 `LayerName`   <a name="sam-layerversion-layername"></a>
The name or Amazon Resource Name \(ARN\) of the layer\.  
*Type*: String  
*Required*: No  
*Default*: Resource logical id  
*AWS CloudFormation compatibility*: This property is similar to the `[LayerName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-layerversion.html#cfn-lambda-layerversion-layername)` property of an `AWS::Lambda::LayerVersion` resource\. If you don't specify a name, the logical id of the resource will be used as the name\.

 `LicenseInfo`   <a name="sam-layerversion-licenseinfo"></a>
Information about the license for this LayerVersion\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[LicenseInfo](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-layerversion.html#cfn-lambda-layerversion-licenseinfo)` property of an `AWS::Lambda::LayerVersion` resource\.

 `RetentionPolicy`   <a name="sam-layerversion-retentionpolicy"></a>
Specifies whether old versions of your LayerVersion are retained or deleted after an update\.  
Supported values: `Retain` and `Delete`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*Additional Notes*: When you specify `Retain`, AWS SAM adds a [Resource Attribute](http://mhirayam.aka.corp.amazon.com/docs-preview/sam-gh-migration/serverless-application-model/latest/developerguide/sam-specification-resource-attributes.html) of `DeletionPolicy: Retain` to the transformed `AWS::Lambda::LayerVersion` resource\.

## Return Values<a name="sam-resource-layerversion-return-values"></a>

### Ref<a name="sam-resource-layerversion-return-values-ref"></a>

When the logical ID of this resource is provided to the `Ref` intrinsic function, it returns the resource ARN of the underlying Lambda LayerVersion\.

For more information about using the `Ref` function, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html) in the *AWS CloudFormation User Guide*\. 

## Examples<a name="sam-resource-layerversion--examples"></a>

### LayerVersionExample<a name="sam-resource-layerversion--examples--layerversionexample"></a>

Example of a LayerVersion

#### YAML<a name="sam-resource-layerversion--examples--layerversionexample--yaml"></a>

```
Properties:
  LayerName: MyLayer
  Description: Layer description
  ContentUri: 's3://my-bucket/my-layer.zip'
  CompatibleRuntimes:
    - nodejs10.x
    - nodejs12.x
  LicenseInfo: 'Available under the MIT-0 license.'
  RetentionPolicy: Retain
```