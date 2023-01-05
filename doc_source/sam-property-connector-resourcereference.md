# ResourceReference<a name="sam-property-connector-resourcereference"></a>

A reference to a resource that the [AWS::Serverless::Connector](sam-resource-connector.md) resource type uses\.

**Note**  
For resources in the same template, provide the `Id`\. For resources not in the same template, use a combination of other properties\. For more information, see [AWS SAM connector reference](reference-sam-connector.md)\.

## Syntax<a name="sam-property-connector-resourcereference-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-connector-resourcereference-syntax.yaml"></a>

```
  [Arn](#sam-connector-resourcereference-arn): String
  [Id](#sam-connector-resourcereference-id): String
  [Name](#sam-connector-resourcereference-name): String
  [Qualifier](#sam-connector-resourcereference-qualifier): String
  [QueueUrl](#sam-connector-resourcereference-queueurl): String
  [ResourceId](#sam-connector-resourcereference-resourceid): String
  [RoleName](#sam-connector-resourcereference-rolename): String
  [Type](#sam-connector-resourcereference-type): String
```

## Properties<a name="sam-property-connector-resourcereference-properties"></a>

 `Arn`   <a name="sam-connector-resourcereference-arn"></a>
The ARN of a resource\.  
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Id`   <a name="sam-connector-resourcereference-id"></a>
The [logical ID](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resources-section-structure.html) of a resource in the same template\.  
When `Id` is specified, if the connector generates AWS Identity and Access Management \(IAM\) policies, the IAM role associated to those policies will be inferred from the resource `Id`\. When `Id` is not specified, provide `RoleName` of the resource for connectors to attach generated IAM policies to an IAM role\.
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Name`   <a name="sam-connector-resourcereference-name"></a>
The name of a resource\.  
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Qualifier`   <a name="sam-connector-resourcereference-qualifier"></a>
A qualifier for a resource that narrows its scope\. `Qualifier` replaces the `*` value at the end of a resource constraint ARN\. For an example, see [API Gateway invoking a Lambda function](#sam-property-connector-resourcereference--examples--api-gateway-invoking-a-lambda-function)\.  
Qualifier definition varies per resource type\. For a list of supported source and destination resource types, see [AWS SAM connector reference](reference-sam-connector.md)\.
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `QueueUrl`   <a name="sam-connector-resourcereference-queueurl"></a>
The Amazon SQS queue URL\. This property only applies to Amazon SQS resources\.  
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ResourceId`   <a name="sam-connector-resourcereference-resourceid"></a>
The ID of a resource\. For example, the API Gateway API ID\.  
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `RoleName`   <a name="sam-connector-resourcereference-rolename"></a>
The role name associated with a resource\.  
When `Id` is specified, if the connector generates IAM policies, the IAM role associated to those policies will be inferred from the resource `Id`\. When `Id` is not specified, provide `RoleName` of the resource for connectors to attach generated IAM policies to an IAM role\.
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Type`   <a name="sam-connector-resourcereference-type"></a>
The AWS CloudFormation type of a resource\. For more information, go to [AWS resource and property types reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html)\.  
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-connector-resourcereference--examples"></a>

### API Gateway invoking a Lambda function<a name="sam-property-connector-resourcereference--examples--api-gateway-invoking-a-lambda-function"></a>

The following example uses the [AWS::Serverless::Connector](sam-resource-connector.md) resource to allow Amazon API Gateway to invoke an AWS Lambda function\.

#### YAML<a name="sam-property-connector-resourcereference--examples--api-gateway-invoking-a-lambda-function--yaml"></a>

```
Transform: AWS::Serverless-2016-10-31
Resources:
  MyRole:
    Type: AWS::IAM::Role
    Properties:
      AssumeRolePolicyDocument:
        Statement:
          - Effect: Allow
            Action: sts:AssumeRole
            Principal:
              Service: lambda.amazonaws.com
      ManagedPolicyArns:
        - !Sub arn:${AWS::Partition}:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole

  MyFunction:
    Type: AWS::Lambda::Function
    Properties:
      Role: !GetAtt MyRole.Arn
      Runtime: nodejs16.x
      Handler: index.handler
      Code:
        ZipFile: |
          exports.handler = async (event) => {
            return {
              statusCode: 200,
              body: JSON.stringify({
                "message": "It works!"
              }),
            };
          };

  MyApi:
    Type: AWS::ApiGatewayV2::Api
    Properties:
      Name: MyApi
      ProtocolType: HTTP

  MyStage:
    Type: AWS::ApiGatewayV2::Stage
    Properties:
      ApiId: !Ref MyApi
      StageName: prod
      AutoDeploy: True

  MyIntegration:
    Type: AWS::ApiGatewayV2::Integration
    Properties:
      ApiId: !Ref MyApi
      IntegrationType: AWS_PROXY
      IntegrationUri: !Sub arn:aws:apigateway:${AWS::Region}:lambda:path/2015-03-31/functions/${MyFunction.Arn}/invocations
      IntegrationMethod: POST
      PayloadFormatVersion: "2.0"

  MyRoute:
    Type: AWS::ApiGatewayV2::Route
    Properties:
      ApiId: !Ref MyApi
      RouteKey: GET /hello
      Target: !Sub integrations/${MyIntegration}

  MyConnector:
    Type: AWS::Serverless::Connector
    Properties:
      Source: # Use 'Id' when resource is in the same template
        Type: AWS::ApiGatewayV2::Api
        ResourceId: !Ref MyApi
        Qualifier: prod/GET/hello # Or "*" to allow all routes
      Destination: # Use 'Id' when resource is in the same template
        Type: AWS::Lambda::Function
        Arn: !GetAtt MyFunction.Arn
      Permissions:
        - Write

Outputs:
  Endpoint:
    Value: !Sub https://${MyApi}.execute-api.${AWS::Region}.${AWS::URLSuffix}/prod/hello
```