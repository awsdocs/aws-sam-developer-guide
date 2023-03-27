# AWS SAM connector reference<a name="reference-sam-connector"></a>

This section contains reference information for the AWS Serverless Application Model \(AWS SAM\) connector resource type\. For an introduction to connectors, see [Managing resource permissions with AWS SAM connectors](managing-permissions-connectors.md)\.

## Supported source and destination resource types for connectors<a name="supported-connector-resource-types"></a>

The `AWS::Serverless::Connector` resource type supports a select number of connections between source and destination resources\. When configuring connectors in your AWS SAM template, use the following table to reference supported connections and the properties that need to be defined for each source and destination resource type\. For more information about configuring connectors in your template, see [AWS::Serverless::Connector](sam-resource-connector.md)\.

For both source and destination resources, when defined within the same template, use the `Id` property\. Optionally, a `Qualifier` can be added to narrow the scope of your defined resource\. When the resource is not within the same template, use a combination of supported properties\.

 To request new connections, [submit a new issue](https://github.com/aws/serverless-application-model/issues/new?assignees=&labels=area%2Fconnectors,stage%2Fneeds-triage&template=other.md&title=%28New%20Connector%20Profile%29) at the *serverless\-application\-model AWS GitHub repository*\.


| Source type | Destination type | Permissions | Source properties | Destination properties | 
| --- | --- | --- | --- | --- | 
| `AWS::ApiGateway::RestApi` | `AWS::Lambda::Function` | `Write` | `Id` or `Qualifier`, `ResourceId`, and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::ApiGateway::RestApi` | `AWS::Serverless::Function` | `Write` | `Id` or `Qualifier`, `ResourceId`, and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::ApiGatewayV2::Api` | `AWS::Lambda::Function` | `Write` | `Id` or `Qualifier`, `ResourceId`, and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::ApiGatewayV2::Api` | `AWS::Serverless::Function` | `Write` | `Id` or `Qualifier`, `ResourceId`, and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::DynamoDB::Table` | `AWS::Lambda::Function` | `Read` | `Id` or `Arn` and `Type` | `Id` or `RoleName` and `Type` | 
| `AWS::DynamoDB::Table` | `AWS::Serverless::Function` | `Read` | `Id` or `Arn` and `Type` | `Id` or `RoleName` and `Type` | 
| `AWS::Events::Rule` | `AWS::Events::EventBus` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Events::Rule` | `AWS::Lambda::Function` | `Write` | `Id` or `Arn` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Events::Rule` | `AWS::Serverless::Function` | `Write` | `Id` or `Arn` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Events::Rule` | `AWS::Serverless::StateMachine` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Events::Rule` | `AWS::SNS::Topic` | `Write` | `Id` or `Arn` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Events::Rule` | `AWS::SQS::Queue` | `Write` | `Id` or `Arn` and `Type` | `Id` or `Arn`, `QueueUrl`, and `Type` | 
| `AWS::Events::Rule` | `AWS::StepFunctions::StateMachine` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Lambda::Function` | `AWS::DynamoDB::Table` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Lambda::Function` | `AWS::Events::EventBus` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Lambda::Function` | `AWS::Lambda::Function` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Lambda::Function` | `AWS::Location::PlaceIndex` | `Read` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Lambda::Function` | `AWS::S3::Bucket` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Lambda::Function` | `AWS::Serverless::Function` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Lambda::Function` | `AWS::Serverless::SimpleTable` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Lambda::Function` | `AWS::Serverless::StateMachine` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn`, `Name`, and `Type` | 
| `AWS::Lambda::Function` | `AWS::SNS::Topic` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Lambda::Function` | `AWS::SQS::Queue` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Lambda::Function` | `AWS::StepFunctions::StateMachine` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn`, `Name`, and `Type` | 
| `AWS::S3::Bucket` | `AWS::Lambda::Function` | `Write` | `Id` or `Arn` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::S3::Bucket` | `AWS::Serverless::Function` | `Write` | `Id` or `Arn` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Api` | `AWS::Lambda::Function` | `Write` | `Id` or `Qualifier`, `ResourceId`, and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Api` | `AWS::Serverless::Function` | `Write` | `Id` or `Qualifier`, `ResourceId`, and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Function` | `AWS::DynamoDB::Table` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Function` | `AWS::Events::EventBus` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Function` | `AWS::Lambda::Function` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Function` | `AWS::S3::Bucket` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Function` | `AWS::Serverless::Function` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Function` | `AWS::Serverless::SimpleTable` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Function` | `AWS::Serverless::StateMachine` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn`, `Name`, and `Type` | 
| `AWS::Serverless::Function` | `AWS::SNS::Topic` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Function` | `AWS::SQS::Queue` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::Function` | `AWS::StepFunctions::StateMachine` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn`, `Name`, and `Type` | 
| `AWS::Serverless::HttpApi` | `AWS::Lambda::Function` | `Write` | `Id` or `Qualifier`, `ResourceId`, and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::HttpApi` | `AWS::Serverless::Function` | `Write` | `Id` or `Qualifier`, `ResourceId`, and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::SimpleTable` | `AWS::Lambda::Function` | `Read` | `Id` or `Arn` and `Type` | `Id` or `RoleName` and `Type` | 
| `AWS::Serverless::SimpleTable` | `AWS::Serverless::Function` | `Read` | `Id` or `Arn` and `Type` | `Id` or `RoleName` and `Type` | 
| `AWS::Serverless::StateMachine` | `AWS::DynamoDB::Table` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::StateMachine` | `AWS::Events::EventBus` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::StateMachine` | `AWS::Lambda::Function` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::StateMachine` | `AWS::S3::Bucket` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::StateMachine` | `AWS::Serverless::Function` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::StateMachine` | `AWS::Serverless::SimpleTable` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::StateMachine` | `AWS::Serverless::StateMachine` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn`, `Name`, and `Type` | 
| `AWS::Serverless::StateMachine` | `AWS::SNS::Topic` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::StateMachine` | `AWS::SQS::Queue` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::Serverless::StateMachine` | `AWS::StepFunctions::StateMachine` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn`, `Name`, and `Type` | 
| `AWS::SNS::Topic` | `AWS::Lambda::Function` | `Write` | `Id` or `Arn` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::SNS::Topic` | `AWS::Serverless::Function` | `Write` | `Id` or `Arn` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::SNS::Topic` | `AWS::SQS::Queue` | `Write` | `Id` or `Arn` and `Type` | `Id` or `Arn`, `QueueUrl`, and `Type` | 
| `AWS::SQS::Queue` | `AWS::Lambda::Function` | `Read`, `Write` | `Id` or `Arn` and `Type` | `Id` or `RoleName` and `Type` | 
| `AWS::SQS::Queue` | `AWS::Serverless::Function` | `Read`, `Write` | `Id` or `Arn` and `Type` | `Id` or `RoleName` and `Type` | 
| `AWS::StepFunctions::StateMachine` | `AWS::DynamoDB::Table` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::StepFunctions::StateMachine` | `AWS::Events::EventBus` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::StepFunctions::StateMachine` | `AWS::Lambda::Function` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::StepFunctions::StateMachine` | `AWS::S3::Bucket` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::StepFunctions::StateMachine` | `AWS::Serverless::Function` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::StepFunctions::StateMachine` | `AWS::Serverless::SimpleTable` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::StepFunctions::StateMachine` | `AWS::Serverless::StateMachine` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn`, `Name`, and `Type` | 
| `AWS::StepFunctions::StateMachine` | `AWS::SNS::Topic` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::StepFunctions::StateMachine` | `AWS::SQS::Queue` | `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn` and `Type` | 
| `AWS::StepFunctions::StateMachine` | `AWS::StepFunctions::StateMachine` | `Read`, `Write` | `Id` or `RoleName` and `Type` | `Id` or `Arn`, `Name`, and `Type` | 