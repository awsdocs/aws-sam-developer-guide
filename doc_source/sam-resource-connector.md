# AWS::Serverless::Connector<a name="sam-resource-connector"></a>

Configures permissions between two resources\. For an introduction to connectors, see [Managing resource permissions with AWS SAM connectors](managing-permissions-connectors.md)\.

For more information on generated AWS CloudFormation resources, see [AWS CloudFormation resources generated when you specify AWS::Serverless::Connector](sam-specification-generated-resources-connector.md)\.

To provide feedback on connectors, [submit a new issue](https://github.com/aws/serverless-application-model/issues/new?assignees=&labels=area%2Fconnectors,stage%2Fneeds-triage&template=other.md&title=%28Feature%20Request%29) at the *serverless\-application\-model AWS GitHub repository*\.

## Syntax<a name="sam-resource-connector-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use any of the following syntaxes\.

**Note**  
We recommend using the embedded connectors syntax for most use cases\. Being embedded within the source resource makes it easier to read and maintain over time\. When you need to reference a source resource that is not within the same AWS SAM template, such as a resource in a nested stack or a shared resource, use the `AWS::Serverless::Connector` syntax\.

### Embedded connectors<a name="sam-resource-connector-syntax-embedded"></a>

```
<source-resource-logical-id>:
  Connectors:
    <connector-logical-id:
      Properties:
        [Destination](#sam-connector-destination): ResourceReference
        [Permissions](#sam-connector-permissions): List
        [SourceReference](#sam-connector-sourcereference): SourceReference
```

### AWS::Serverless::Connector<a name="sam-resource-connector-syntax-connector"></a>

```
Type: AWS::Serverless::Connector
Properties:
  [Destination](#sam-connector-destination): ResourceReference
  [Permissions](#sam-connector-permissions): List
  [Source](#sam-connector-source): ResourceReference
```

## Properties<a name="sam-resource-connector-properties"></a>

 `Destination`   <a name="sam-connector-destination"></a>
The destination resource\.  
*Type*: [ResourceReference](sam-property-connector-resourcereference.md)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Permissions`   <a name="sam-connector-permissions"></a>
The permission type that the source resource is allowed to perform on the destination resource\.  
`Read` includes AWS Identity and Access Management \(IAM\) actions that allow reading data from the resource\.  
`Write` inclues IAM actions that allow initiating and writing data to a resource\.  
*Valid values*: `Read` or `Write`  
*Type*: List  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Source`   <a name="sam-connector-source"></a>
The source resource\. Required when using the `AWS::Serverless::Connector` syntax\.  
*Type*: [ResourceReference](sam-property-connector-resourcereference.md)  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `SourceReference`   <a name="sam-connector-sourcereference"></a>
The source resource\.  
Use with the embedded connectors syntax when defining additional properties for the source resource\.
*Type*: [SourceReference](sam-property-connector-sourcereference.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-resource-connector-examples"></a>

### Embedded connectors<a name="sam-resource-connector-examples-embedded"></a>

The following example uses embedded connectors to define a `Write` data connection between an AWS Lambda function and Amazon DynamoDB table:

```
Transform: AWS::Serverless-2016-10-31
...
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
    ...
```

The following example uses embedded connectors to define `Read` and `Write` permissions:

```
Transform: AWS::Serverless-2016-10-31
...
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Connectors:
      MyConn:
        Properties:
          Destination:
            Id: MyTable
          Permissions:
            - Read
            - Write
  MyTable:
    Type: AWS::DynamoDB::Table
    ...
```

The following example uses embedded connectors to define a source resource with a property other than `Id`:

```
Transform: AWS::Serverless-2016-10-31
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

### AWS::Serverless::Connector<a name="sam-resource-connector--examples-connector"></a>

The following example uses the [AWS::Serverless::Connector](#sam-resource-connector) resource to have an AWS Lambda function read from, and write to an Amazon DynamoDB table:

```
MyConnector:
  Type: AWS::Serverless::Connector
  Properties:
    Source:
      Id: MyFunction
    Destination:
      Id: MyTable
    Permissions:
      - Read
      - Write
```

The following example uses the [AWS::Serverless::Connector](#sam-resource-connector) resource to have a Lambda function write to an Amazon SNS topic, with both resources in the same template:

```
MyConnector:
  Type: AWS::Serverless::Connector
  Properties:
    Source:
      Id: MyLambda
    Destination:
      Id: MySNSTopic
    Permissions:
      - Write
```

The following example uses the [AWS::Serverless::Connector](#sam-resource-connector) resource to have an Amazon SNS topic write to a Lambda function, which then writes to an Amazon DynamoDB table, with all resources in the same template:

```
Transform: AWS::Serverless-2016-10-31
Resources:
  Topic:
    Type: AWS::SNS::Topic
    Properties:
      Subscription:
        - Endpoint: !GetAtt Function.Arn
          Protocol: lambda

  Function:
    Type: AWS::Serverless::Function
    Properties:
      Runtime: nodejs16.x
      Handler: index.handler
      InlineCode: |
        const AWS = require('aws-sdk');
        exports.handler = async (event, context) => {
          const docClient = new AWS.DynamoDB.DocumentClient();
          await docClient.put({ 
            TableName: process.env.TABLE_NAME, 
            Item: {
              id: context.awsRequestId,
              event: JSON.stringify(event)
            }
          }).promise();
        };
      Environment:
        Variables:
          TABLE_NAME: !Ref Table

  Table:
    Type: AWS::Serverless::SimpleTable

  TopicToFunctionConnector:
    Type: AWS::Serverless::Connector
    Properties:
      Source: 
        Id: Topic
      Destination: 
        Id: Function
      Permissions:
        - Write

  FunctionToTableConnector:
    Type: AWS::Serverless::Connector
    Properties:
      Source: 
        Id: Function
      Destination: 
        Id: Table
      Permissions:
        - Write
```

The following is the transformed AWS CloudFormation template from the example above:

```
"FunctionToTableConnectorPolicy": {
  "Type": "AWS::IAM::ManagedPolicy",
  "Metadata": {
    "aws:sam:connectors": {
      "FunctionToTableConnector": {
        "Source": {
          "Type": "AWS::Lambda::Function"
        },
        "Destination": {
          "Type": "AWS::DynamoDB::Table"
        }
      }
    }
  },
  "Properties": {
    "PolicyDocument": {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "dynamodb:PutItem",
            "dynamodb:UpdateItem",
            "dynamodb:DeleteItem",
            "dynamodb:BatchWriteItem",
            "dynamodb:PartiQLDelete",
            "dynamodb:PartiQLInsert",
            "dynamodb:PartiQLUpdate"
          ],
          "Resource": [
            {
              "Fn::GetAtt": [
                "MyTable",
                "Arn"
              ]
            },
            {
              "Fn::Sub": [
                "${DestinationArn}/index/*",
                {
                  "DestinationArn": {
                    "Fn::GetAtt": [
                      "MyTable",
                      "Arn"
                    ]
                  }
                }
              ]
            }
          ]
        }
      ]
    },
    "Roles": [
      {
        "Ref": "MyFunctionRole"
      }
    ]
  }
}
```