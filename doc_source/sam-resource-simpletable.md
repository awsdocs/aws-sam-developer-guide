# AWS::Serverless::SimpleTable<a name="sam-resource-simpletable"></a>

Creates a DynamoDB table with a single attribute primary key\. It is useful when data only needs to be accessed via a primary key\.

To use the more advanced functionality of DynamoDB, use an [http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-dynamodb-table.html](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-dynamodb-table.html) resource instead\.

## Syntax<a name="sam-resource-simpletable-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-resource-simpletable-syntax.yaml"></a>

```
Type: AWS::Serverless::SimpleTable
Properties:
  [PrimaryKey](#sam-simpletable-primarykey): PrimaryKeyObject
  [ProvisionedThroughput](#sam-simpletable-provisionedthroughput): [ProvisionedThroughput](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-dynamodb-provisionedthroughput.html)
  [SSESpecification](#sam-simpletable-ssespecification): [SSESpecification](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-dynamodb-table-ssespecification.html)
  [TableName](#sam-simpletable-tablename): String
  [Tags](#sam-simpletable-tags): Map
```

## Properties<a name="sam-resource-simpletable-properties"></a>

 `PrimaryKey`   <a name="sam-simpletable-primarykey"></a>
Attribute name and type to be used as the table's primary key\. If not provided, the primary key will be a `String` with a value of `id`\.  
**Note**: The value of this property cannot be modified after this resource is created\.  
*Type*: [PrimaryKeyObject](sam-property-simpletable-primarykeyobject.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ProvisionedThroughput`   <a name="sam-simpletable-provisionedthroughput"></a>
Read and write throughput provisioning information\.  
If `ProvisionedThroughput` is not specified `BillingMode` will be specified as `PAY_PER_REQUEST`\.  
*Type*: [ProvisionedThroughput](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-dynamodb-provisionedthroughput.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ProvisionedThroughput](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-dynamodb-provisionedthroughput.html)` property of an `AWS::DynamoDB::Table` resource\.

 `SSESpecification`   <a name="sam-simpletable-ssespecification"></a>
Specifies the settings to enable server\-side encryption\.  
*Type*: [SSESpecification](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-dynamodb-table-ssespecification.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[SSESpecification](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-dynamodb-table-ssespecification.html)` property of an `AWS::DynamoDB::Table` resource\.

 `TableName`   <a name="sam-simpletable-tablename"></a>
Name for the DynamoDB Table\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[TableName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-dynamodb-table.html#cfn-dynamodb-table-tablename)` property of an `AWS::DynamoDB::Table` resource\.

 `Tags`   <a name="sam-simpletable-tags"></a>
A map \(string to string\) that specifies the tags to be added to this SimpleTable\. Keys and values are limited to alphanumeric characters\. Keys can be 1 to 127 Unicode characters in length and cannot be prefixed with aws:\. Values can be 1 to 255 Unicode characters in length\.  
*Type*: Map  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[Tags](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-dynamodb-table.html#cfn-dynamodb-table-tags)` property of an `AWS::DynamoDB::Table` resource\. The Tags property in SAM consists of Key:Value pairs; in CloudFormation it consists of a list of Tag objects\.

## Return Values<a name="sam-resource-simpletable-return-values"></a>

### Ref<a name="sam-resource-simpletable-return-values-ref"></a>

When the logical ID of this resource is provided to the Ref intrinsic function, it returns the resource name of the underlying DynamoDB table\.

For more information about using the `Ref` function, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html) in the *AWS CloudFormation User Guide*\. 

## Examples<a name="sam-resource-simpletable--examples"></a>

### SimpleTableExample<a name="sam-resource-simpletable--examples--simpletableexample"></a>

Example of a SimpleTable

#### YAML<a name="sam-resource-simpletable--examples--simpletableexample--yaml"></a>

```
Properties:
  TableName: my-table
  Tags:
    Department: Engineering
    AppType: Serverless
```