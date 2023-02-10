# Managing resource permissions with AWS SAM connectors<a name="managing-permissions-connectors"></a>

**Topics**
+ [What are AWS SAM connectors?](#what-are-connectors)
+ [Example of connectors](#what-are-connectors-example)
+ [Supported connections between source and destination resources](#supported-connector-resources)
+ [Using connectors](#connector-usage)
+ [How connectors work](#connectors-work)
+ [Benefits of AWS SAM connectors](#connector-benefits)
+ [Learn more](#connector-learn-more)
+ [Provide feedback](#connector-feedback)

## What are AWS SAM connectors?<a name="what-are-connectors"></a>

Connectors are an AWS Serverless Application Model \(AWS SAM\) abstract resource type, identified as `AWS::Serverless::Connector`, that provides simple and well\-scoped permissions between your serverless application resources\. Use the `Connectors` resource attribute by embedding it within a **source** resource\. Then, define your **destination** resource and describe how data or events should flow between those resources\. AWS SAM then composes the access policies necessary to facilitate the required interactions\.

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  <source-resource-logical-id>:
    Type: <resource-type>
    ...
    Connectors:
      <connector-name>:
        Properties:
          Destination:
            <properties-that-identify-destination-resource>
          Permissions:
            <permission-types-to-provision>
  ...
```

## Example of connectors<a name="what-are-connectors-example"></a>

In this example, we use connectors to write data from an AWS Lambda function to an Amazon DynamoDB table\.

![\[A diagram of a Lambda function writing data to a DynamoDB table using AWS SAM connectors.\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/images/managing-connectors-example.png)

```
Transform: AWS::Serverless-2016-10-31
Resources:
  MyTable:
    Type: AWS::Serverless::SimpleTable
  MyFunction:
    Type: AWS::Serverless::Function
    Connectors:
      MyConn:
        Properties:
          Destination:
            Id: MyTable
          Permissions:
            - Write
    Properties:
      Runtime: nodejs16.x
      Handler: index.handler
      InlineCode: |
        const AWS = require("aws-sdk");
        const docClient = new AWS.DynamoDB.DocumentClient();
        exports.handler = async (event, context) => {
          await docClient.put({
            TableName: process.env.TABLE_NAME,
            Item: {
              id: context.awsRequestId,
              event: JSON.stringify(event) 
            }
          }).promise();
        }
      Environment:
        Variables:
          TABLE_NAME: !Ref MyTable
```

The `Connectors` resource attribute is embedded within the Lambda function source resource\. The DynamoDB table is defined as the destination resource using the `Id` property\. Connectors will provision `Write` permissions between these two resources\.

When you deploy your AWS SAM template to AWS CloudFormation, AWS SAM will automatically compose the necessary access policies required for this connection to work\.

## Supported connections between source and destination resources<a name="supported-connector-resources"></a>

Connectors support `Read` and `Write` data and event permission types between a select combination of source and destination resource connections\. For example, connectors support a `Write` connection between an `AWS::ApiGateway::RestApi` source resource and an `AWS::Lambda::Function` destination resource\.

Source and destination resources can be defined by using a combination of supported properties\. Property requirements will depend on the connection you are making and where the resources are defined\.

**Note**  
Connectors can provision permissions between supported serverless and non\-serverless resource types\.

For a list of supported resource connections and their property requirements, see [Supported source and destination resource types for connectors](reference-sam-connector.md#supported-connector-resource-types)\.

## Using connectors<a name="connector-usage"></a>

### Defining Read and Write permissions<a name="connector-usage-define"></a>

`Read` and `Write` permissions can be provisioned within a single connector:

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  MyFunction:
    Type: AWS::Lambda::Function
    Connectors:
      MyTableConn:
        Properties:
          Destination:
            Id: MyTable
          Permissions:
            - Read
            - Write
  MyTable:
    Type: AWS::DynamoDB::Table
```

### Defining resources by using other supported properties<a name="connector-usage-other-properties"></a>

For both source and destination resources, when defined within the same template, use the `Id` property\. Optionally, a `Qualifier` can be added to narrow the scope of your defined resource\. When the resource is not within the same template, use a combination of supported properties\.
+ For a list of supported property combinations for source and destination resources, see [Supported source and destination resource types for connectors](reference-sam-connector.md#supported-connector-resource-types)\.
+ For a description of properties that you can use with connectors, see [AWS::Serverless::Connector](sam-resource-connector.md)\.

When you define a source resource with a property other than `Id`, use the `SourceReference` property\.

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  <source-resource-logical-id>:
    Type: <resource-type>
    ...
    Connectors:
      <connector-name>:
        Properties:
          SourceReference:
            Qualifier: <optional-qualifier>
            <other-supported-properties>
          Destination:
            <properties-that-identify-destination-resource>
          Permissions:
            <permission-types-to-provision>
```

Here's an example, using a `Qualifier` to narrow the scope of an Amazon API Gateway resource:

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  MyApi:
    Type: AWS::Serverless::Api
    Connectors:
      ApiToLambdaConn:
        Properties:
          SourceReference:
            Qualifier: Prod/GET/foobar
          Destination:
            Id: MyFunction
          Permissions:
            - Write           
  ...
```

Here's an example, using a supported combination of `Arn` and `Type` to define a destination resource from another template:

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Connectors:
      TableConn:
        Properties:
          Destination:
            Type: AWS::DynamoDB::Table
            Arn: !GetAtt MyTable.Arn
  ...
```

### Defining resource attributes with connectors<a name="connector-usage-resource-attributes"></a>

Resource attributes can be defined for resources to specify additional behaviors and relationships\. To learn more about resource attributes, see [Resource attribute reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-product-attribute-reference.html) in the *AWS CloudFormation User Guide*\.

You can add resource attributes to your embedded connector by defining them on the same level as your connector properties\. When your AWS SAM template is transformed at deployment, attributes will pass through to the generated resources\.

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Connectors:
      MyConn:
        DeletionPolicy: Retain
        DependsOn: AnotherFunction
        Properties:
          ...
```

## How connectors work<a name="connectors-work"></a>

**Note**  
This section explains how connectors provision the necessary resources behind the scenes\. This happens for you automatically when using connectors\.

First, the embedded `Connectors` resource attribute is transformed into an `AWS::Serverless::Connector` resource type\.

```
Transform: AWS::Serverless-2016-10-31
Resources:
  ...
  MyConnector:
    Type: AWS::Serverless::Connector
    Properties:
      Source:
        Id: MyFunction
      Destination:
        Id: MyTable
      Permissions:
        - Write
  ...
```

**Note**  
You can also define connectors in your AWS SAM template by using this syntax\. This is recommended when your source resource is defined on a separate template from your connector\.

Next, the necessary access policies for this connection are automatically composed\. For more information about the resources generated by connectors, see [AWS CloudFormation resources generated when you specify AWS::Serverless::Connector](sam-specification-generated-resources-connector.md)\.

## Benefits of AWS SAM connectors<a name="connector-benefits"></a>

By automatically composing the appropriate access policies between resources, connectors provide you the ability to author your serverless applications and focus on your application architecture without needing expertise in AWS authorization capabilities, policy language, and service\-specific security settings\. Therefore, connectors are a great benefit to developers who may be new to serverless development, or seasoned developers looking to increase their development velocity\.

## Learn more<a name="connector-learn-more"></a>

For more information about using AWS SAM connectors, see [AWS::Serverless::Connector](sam-resource-connector.md)\.

## Provide feedback<a name="connector-feedback"></a>

To provide feedback on connectors, [submit a new issue](https://github.com/aws/serverless-application-model/issues/new?assignees=&labels=area%2Fconnectors,stage%2Fneeds-triage&template=other.md&title=%28Feature%20Request%29) at the *serverless\-application\-model AWS GitHub repository*\.