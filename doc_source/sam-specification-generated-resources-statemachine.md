# AWS CloudFormation resources generated when AWS::Serverless::StateMachine is specified<a name="sam-specification-generated-resources-statemachine"></a>

When an `AWS::Serverless::StateMachine` is specified, AWS Serverless Application Model \(AWS SAM\) generates an `AWS::StepFunctions::StateMachine` base AWS CloudFormation resource\.

**`AWS::StepFunctions::StateMachine`**  
*`LogicalId`: *`<statemachine‑LogicalId>`  
*Referenceable property: *N/A \(you must use the `LogicalId` to reference this AWS CloudFormation resource\)

In addition to this AWS CloudFormation resource, when `AWS::Serverless::StateMachine` is specified, AWS SAM also generates AWS CloudFormation resources for the following scenarios:

**Topics**
+ [Role property is not specified](#sam-specification-generated-resources-statemachine-not-role)
+ [An Api event source is specified](#sam-specification-generated-resources-statemachine-api)
+ [An event bridge \(or event bus\) event source is specified](#sam-specification-generated-resources-statemachine-eventbridge)

## Role property is not specified<a name="sam-specification-generated-resources-statemachine-not-role"></a>

When the `Role` property of an `AWS::Serverless::StateMachine` is *not* specified, AWS SAM generates an `AWS::IAM::Role` AWS CloudFormation resource\.

**`AWS::IAM::Role`**  
*`LogicalId`: *`<statemachine‑LogicalId>Role`  
*Referenceable property: *N/A \(you must use the `LogicalId` to reference this AWS CloudFormation resource\)

## An Api event source is specified<a name="sam-specification-generated-resources-statemachine-api"></a>

When the `Event` property of an `AWS::Serverless::StateMachine` is set to `Api`, but the `RestApiId` property is *not* specified, AWS SAM generates the `AWS::ApiGateway::RestApi` AWS CloudFormation resource\.

**`AWS::ApiGateway::RestApi`**  
*`LogicalId`: *`ServerlessRestApi`  
*Referenceable property: *N/A \(you must use the `LogicalId` to reference this AWS CloudFormation resource\)

## An event bridge \(or event bus\) event source is specified<a name="sam-specification-generated-resources-statemachine-eventbridge"></a>

When the `Event` property of an `AWS::Serverless::StateMachine` is set to one of the event bridge \(or event bus\) types, AWS SAM generates the `AWS::Events::Rule` AWS CloudFormation resource\. This applies to the following types: `EventBridgeRule`, `Schedule`, and `CloudWatchEvents`\.

**`AWS::Events::Rule`**  
*`LogicalId`: *`<statemachine‑LogicalId><event‑LogicalId>`  
*Referenceable property: *N/A \(you must use the `LogicalId` to reference this AWS CloudFormation resource\)