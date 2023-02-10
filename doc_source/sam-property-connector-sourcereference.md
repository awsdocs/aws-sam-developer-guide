# SourceReference<a name="sam-property-connector-sourcereference"></a>

A reference to a source resource that the [AWS::Serverless::Connector](sam-resource-connector.md) resource type uses\.

## Syntax<a name="sam-property-connector-sourcereference-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-connector-sourcereference-syntax.yaml"></a>

```
[Qualifier](#sam-connector-sourcereference-qualifier): String
```

## Properties<a name="sam-property-connector-sourcereference-properties"></a>

 `Qualifier`   <a name="sam-connector-sourcereference-qualifier"></a>
A qualifier for a resource that narrows its scope\. `Qualifier` replaces the `*` value at the end of a resource constraint ARN\.  
Qualifier definition varies per resource type\. For a list of supported source and destination resource types, see [AWS SAM connector reference](reference-sam-connector.md)\.
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-connector-sourcereference--examples"></a>

**The following example uses embedded connectors to define a source resource with a property other than `Id`:**

```
Transform: AWS::Serverless-2016-10-31
...
Resources:
  MyApi:
    Type: AWS::Serverless::Api
    Connectors:
      ApitoLambdaConn:
        Properties:
          SourceReference:
            Qualifier: Prod/GET/foobar
          Destination:
            Id: MyTable
          Permissions:
            - Read
            - Write
  MyTable:
    Type: AWS::DynamoDB::Table
    ...
```