# PrimaryKeyObject<a name="sam-property-simpletable-primarykeyobject"></a>

The object describing the properties of a primary key\.

## Syntax<a name="sam-property-simpletable-primarykeyobject-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-simpletable-primarykeyobject-syntax.yaml"></a>

```
  [Name](#sam-simpletable-primarykeyobject-name): String
  [Type](#sam-simpletable-primarykeyobject-type): String
```

## Properties<a name="sam-property-simpletable-primarykeyobject-properties"></a>

 `Name`   <a name="sam-simpletable-primarykeyobject-name"></a>
Attribute name of the primary key\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[AttributeName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-dynamodb-attributedef.html#cfn-dynamodb-attributedef-attributename)` property of the `AWS::DynamoDB::Table` `AttributeDefinition` data type\.  
*Additional Notes*: This property is also passed to the [AttributeName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-dynamodb-keyschema.html#aws-properties-dynamodb-keyschema-attributename) property of an `AWS::DynamoDB::Table KeySchema` data type\.

 `Type`   <a name="sam-simpletable-primarykeyobject-type"></a>
The data type for the primary key\.  
Supported values: `String`, `Number`, `Binary`\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[AttributeType](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-dynamodb-attributedef.html#cfn-dynamodb-attributedef-attributename-attributetype)` property of the `AWS::DynamoDB::Table` `AttributeDefinition` data type\.

## Examples<a name="sam-property-simpletable-primarykeyobject--examples"></a>

### PrimaryKey<a name="sam-property-simpletable-primarykeyobject--examples--primarykey"></a>

Primary key example\.

#### YAML<a name="sam-property-simpletable-primarykeyobject--examples--primarykey--yaml"></a>

```
Properties:
  PrimaryKey:
    Name: MyPrimaryKey
    Type: String
```