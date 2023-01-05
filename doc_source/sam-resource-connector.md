# AWS::Serverless::Connector<a name="sam-resource-connector"></a>

Configures permissions between two resources\. For an introduction to connectors, see [Managing resource permissions with AWS SAM connectors](managing-permissions-connectors.md)\.

For more information on generated AWS CloudFormation resources, see [AWS CloudFormation resources generated when you specify AWS::Serverless::Connector](sam-specification-generated-resources-connector.md)\.

To provide feedback on connectors, [submit a new issue](https://github.com/aws/serverless-application-model/issues/new?assignees=&labels=area%2Fconnectors,stage%2Fneeds-triage&template=other.md&title=%28Feature%20Request%29) at the *serverless\-application\-model AWS GitHub repository*\.

## Syntax<a name="sam-resource-connector-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-resource-connector-syntax.yaml"></a>

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
The source resource\.  
*Type*: [ResourceReference](sam-property-connector-resourcereference.md)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-resource-connector--examples"></a>

### Basic example 1<a name="sam-resource-connector--examples--basic-example-1"></a>

The following basic example uses the [AWS::Serverless::Connector](#sam-resource-connector) resource to have an AWS Lambda function read from, and write to an Amazon DynamoDB table\.

For `Source` and `Destination`, you must provide either the `Id` of the resource or a combination of other properties\. For more information, see [AWS SAM connector reference](reference-sam-connector.md)\.

#### YAML<a name="sam-resource-connector--examples--basic-example-1--yaml"></a>

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

### Basic example 2<a name="sam-resource-connector--examples--basic-example-2"></a>

The following example uses the [AWS::Serverless::Connector](#sam-resource-connector) resource to have a Lambda function write to an Amazon SNS topic, with both resources in the same template\.

#### YAML<a name="sam-resource-connector--examples--basic-example-2--yaml"></a>

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

### Basic example 3<a name="sam-resource-connector--examples--basic-example-3"></a>

The following example uses the [AWS::Serverless::Connector](#sam-resource-connector) resource to have a Lambda function write to an Amazon SQS topic, with both resources in the same template\.

#### YAML<a name="sam-resource-connector--examples--basic-example-3--yaml"></a>

```
MyConnector:
  Type: AWS::Serverless::Connector
  Properties:
    Source:
      Id: MyLambda
    Destination:
      Id: MySQSQueue
    Permissions:
      - Write
```

### Multiple functions example<a name="sam-resource-connector--examples--multiple-functions-example"></a>

The following example uses the [AWS::Serverless::Connector](#sam-resource-connector) resource to have an Amazon SNS topic write to a Lambda function, which then writes to an Amazon DynamoDB table, with all resources in the same template\.

#### YAML<a name="sam-resource-connector--examples--multiple-functions-example--yaml"></a>

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

### Transformed AWS CloudFormation template<a name="sam-resource-connector--examples--transformed--template"></a>

The following is the transformed AWS CloudFormation template from the example above\.

#### YAML<a name="sam-resource-connector--examples--transformed--template--yaml"></a>

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