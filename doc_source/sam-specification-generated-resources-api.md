# AWS CloudFormation resources generated when AWS::Serverless::Api is specified<a name="sam-specification-generated-resources-api"></a>

When an `AWS::Serverless::Api` is specified, AWS Serverless Application Model \(AWS SAM\) always generates the following AWS CloudFormation resources: an `AWS::ApiGateway::RestApi`, an `AWS::ApiGateway::Stage`, and an `AWS::ApiGateway::Deployment`\.

**`AWS::ApiGateway::RestApi`**  
*`LogicalId`: *`<api‑LogicalId>`  
*Referenceable property: *N/A \(you must use the `LogicalId` to reference this AWS CloudFormation resource\)

**`AWS::ApiGateway::Stage`**  
*`LogicalId`: *`<api‑LogicalId><stage‑name>Stage`  
`<stage‑name>` is the string that the `StageName` property is set to\. For example, if you set `StageName` to `Gamma`, the `LogicalId` is `MyRestApiGammaStage`\.  
*Referenceable property: *`<api‑LogicalId>.Stage`

**`AWS::ApiGateway::Deployment`**  
*`LogicalId`: *`<api‑LogicalId>Deployment<sha>`  
`<sha>` is a unique hash value that is generated when the stack is created\. For example, `MyRestApiDeployment926eeb5ff1`\.  
*Referenceable property: *`<api‑LogicalId>.Deployment`

In addition to these AWS CloudFormation resources, when `AWS::Serverless::Api` is specified, AWS SAM generates additional AWS CloudFormation resources for the following scenarios\.

**Topics**
+ [DomainName property is specified](#sam-specification-generated-resources-api-domain-name)
+ [UsagePlan property is specified](#sam-specification-generated-resources-api-usage-plan)

## DomainName property is specified<a name="sam-specification-generated-resources-api-domain-name"></a>

When the `DomainName` property of the `Domain` property of an `AWS::Serverless::Api` is specified, AWS SAM generates the `AWS::ApiGateway::DomainName` AWS CloudFormation resource\.

**`AWS::ApiGateway::DomainName`**  
*`LogicalId`: *`ApiGatewayDomainName<sha>`  
`<sha>` is a unique hash value that is generated when the stack is created\. For example: `ApiGatewayDomainName926eeb5ff1`\.  
*Referenceable property: *`<api‑LogicalId>.DomainName`

## UsagePlan property is specified<a name="sam-specification-generated-resources-api-usage-plan"></a>

When the `UsagePlan` property of the `Auth` property of an `AWS::Serverless::Api` is specified, AWS SAM generates the following AWS CloudFormation resources: `AWS::ApiGateway::UsagePlan`, `AWS::ApiGateway::UsagePlanKey`, and `AWS::ApiGateway::ApiKey`\.

**`AWS::ApiGateway::UsagePlan`**  
*`LogicalId`: *`<api‑LogicalId>UsagePlan`  
*Referenceable property: *`<api‑LogicalId>.UsagePlan`

**`AWS::ApiGateway::UsagePlanKey`**  
*`LogicalId`: *`<api‑LogicalId>UsagePlanKey`  
*Referenceable property: *`<api‑LogicalId>.UsagePlanKey`

**`AWS::ApiGateway::ApiKey`**  
*`LogicalId`: *`<api‑LogicalId>ApiKey`  
*Referenceable property: *`<api‑LogicalId>.ApiKey`