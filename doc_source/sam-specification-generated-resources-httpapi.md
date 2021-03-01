# AWS CloudFormation resources generated when AWS::Serverless::HttpApi is specified<a name="sam-specification-generated-resources-httpapi"></a>

When an `AWS::Serverless::HttpApi` is specified, AWS Serverless Application Model \(AWS SAM\) generates the `AWS::ApiGatewayV2::Api` AWS CloudFormation resource\.

**`AWS::ApiGatewayV2::Api`**  
*`LogicalId`: *`<httpapi‑LogicalId>`  
*Referenceable property: *N/A \(you must use the `LogicalId` to reference this AWS CloudFormation resource\)

In addition to this AWS CloudFormation resource, when `AWS::Serverless::HttpApi` is specified, AWS SAM also generates AWS CloudFormation resources for the following scenarios:

**Topics**
+ [StageName property is specified](#sam-specification-generated-resources-httpapi-stage-name)
+ [StageName property is *not* specified](#sam-specification-generated-resources-httpapi-not-stage-name)
+ [DomainName property is specified](#sam-specification-generated-resources-httpapi-domain-name)

## StageName property is specified<a name="sam-specification-generated-resources-httpapi-stage-name"></a>

When the `StageName` property of an `AWS::Serverless::HttpApi` is specified, AWS SAM generates the `AWS::ApiGatewayV2::Stage` AWS CloudFormation resource\.

**`AWS::ApiGatewayV2::Stage`**  
*`LogicalId`: *`<httpapi‑LogicalId><stage‑name>Stage`  
`<stage‑name>` is the string that the `StageName` property is set to\. For example, if you set `StageName` to `Gamma`, the `LogicalId` is: *MyHttpApiGamma*Stage\.  
*Referenceable property: *`<httpapi‑LogicalId>.Stage`

## StageName property is *not* specified<a name="sam-specification-generated-resources-httpapi-not-stage-name"></a>

When the `StageName` property of an `AWS::Serverless::HttpApi` is *not* specified, AWS SAM generates the `AWS::ApiGatewayV2::Stage` AWS CloudFormation resource\.

**`AWS::ApiGatewayV2::Stage`**  
*`LogicalId`: *`<httpapi‑LogicalId>ApiGatewayDefaultStage`  
*Referenceable property: *`<httpapi‑LogicalId>.Stage`

## DomainName property is specified<a name="sam-specification-generated-resources-httpapi-domain-name"></a>

When the `DomainName` property of the `Domain` property of an `AWS::Serverless::HttpApi` is specified, AWS SAM generates the `AWS::ApiGatewayV2::DomainName` AWS CloudFormation resource\.

**`AWS::ApiGatewayV2::DomainName`**  
*`LogicalId`: *`ApiGatewayDomainNameV2<sha>`  
`<sha>` is a unique hash value that is generated when the stack is created\. For example, `ApiGatewayDomainNameV2`*926eeb5ff1*\.  
*Referenceable property: *`<httpapi‑LogicalId>.DomainName`