# AWS CloudFormation resources generated when AWS::Serverless::Function is specified<a name="sam-specification-generated-resources-function"></a>

When an `AWS::Serverless::Function` is specified, AWS Serverless Application Model \(AWS SAM\) creates the `AWS::Lambda::Function` AWS CloudFormation resource\.

**`AWS::Lambda::Function`**  
*`LogicalId`: *`<function‑LogicalId>`  
*Referenceable property: *N/A \(you must use the `LogicalId` to reference this AWS CloudFormation resource\)

In addition to this AWS CloudFormation resource, when `AWS::Serverless::Function` is specified, AWS SAM also generates AWS CloudFormation resources for the following scenarios\.

**Topics**
+ [AutoPublishAlias property is specified](#sam-specification-generated-resources-function-autopublishalias)
+ [Role property is *not* specified](#sam-specification-generated-resources-function-not-role)
+ [OnSuccess \(or OnFailure\) property is specified for Amazon SNS events](#sam-specification-generated-resources-function-sns-onsuccess)
+ [OnSuccess \(or OnFailure\) property is specified for Amazon SQS events](#sam-specification-generated-resources-function-sqs-onsuccess)

## AutoPublishAlias property is specified<a name="sam-specification-generated-resources-function-autopublishalias"></a>

When the `AutoPublishAlias` property of an `AWS::Serverless::Function` is specified, AWS SAM generates the following AWS CloudFormation resources: `AWS::Lambda::Alias` and `AWS::Lambda::Version`\.

**`AWS::Lambda::Alias`**  
*`LogicalId`: *`<function‑LogicalId>Alias<alias‑name>`  
`<alias‑name>` is the string that `AutoPublishAlias` is set to\. For example, if you set `AutoPublishAlias` to `live`, the `LogicalId` is: *MyFunction*Alias*live*\.  
*Referenceable property: *`<function‑LogicalId>.Alias`

**`AWS::Lambda::Version`**  
*`LogicalId`: *`<function‑LogicalId>Version<sha>`  
`<sha>` is a unique hash value that is generated when the stack is created\. For example, *MyFunction*Version*926eeb5ff1*\.  
*Referenceable property: *`<function‑LogicalId>.Version`

## Role property is *not* specified<a name="sam-specification-generated-resources-function-not-role"></a>

When the `Role` property of an `AWS::Serverless::Function` is *not* specified, AWS SAM generates the `AWS::IAM::Role` AWS CloudFormation resource\.

**`AWS::IAM::Role`**  
*`LogicalId`: *`<function‑LogicalId>Role`  
*Referenceable property: *N/A \(you must use the `LogicalId` to reference this AWS CloudFormation resource\)

## OnSuccess \(or OnFailure\) property is specified for Amazon SNS events<a name="sam-specification-generated-resources-function-sns-onsuccess"></a>

When the `OnSuccess` \(or `OnFailure`\) property of the `DestinationConfig` property of the `EventInvokeConfig` property of an `AWS::Serverless::Function` is specified, and the destination type is `SNS` but the destination ARN is *not* specified, AWS SAM generates the following AWS CloudFormation resources: `AWS::Lambda::EventInvokeConfig` and `AWS::SNS::Topic`\.

**`AWS::Lambda::EventInvokeConfig`**  
*`LogicalId`: *`<function‑LogicalId>EventInvokeConfig`  
*Referenceable property: *N/A \(you must use the `LogicalId` to reference this AWS CloudFormation resource\)

**`AWS::SNS::Topic`**  
*`LogicalId`: *`<function‑LogicalId>OnSuccessTopic` \(or `<function‑LogicalId>OnFailureTopic`\)  
*Referenceable property: *`<function‑LogicalId>.DestinationTopic`  
If both `OnSuccess` and `OnFailure` are specified for an Amazon SNS event, to distinguish between the generated resources, you must use the `LogicalId`\.

## OnSuccess \(or OnFailure\) property is specified for Amazon SQS events<a name="sam-specification-generated-resources-function-sqs-onsuccess"></a>

When the `OnSuccess` \(or `OnFailure`\) property of the `DestinationConfig` property of the `EventInvokeConfig` property of an `AWS::Serverless::Function` is specified, and the destination type is `SQS` but the destination ARN is *not* specified, AWS SAM generates the following AWS CloudFormation resources: `AWS::Lambda::EventInvokeConfig` and `AWS::SQS::Queue`\.

**`AWS::Lambda::EventInvokeConfig`**  
*`LogicalId`: *`<function‑LogicalId>EventInvokeConfig`  
*Referenceable property: *N/A \(you must use the `LogicalId` to reference this AWS CloudFormation resource\)

**`AWS::SQS::Queue`**  
*`LogicalId`: *`<function‑LogicalId>OnSuccessQueue` \(or `<function‑LogicalId>OnFailureQueue`\)  
*Referenceable property: *`<function‑LogicalId>.DestinationQueue`  
If both `OnSuccess` and `OnFailure` are specified for an Amazon SQS event, to distinguish between the generated resources, you must use the `LogicalId`\.