# AWS CloudFormation resources generated when you specify AWS::Serverless::Connector<a name="sam-specification-generated-resources-connector"></a>

When you specify an `AWS::Serverless::Connector` resource in an AWS SAM template, AWS SAM generates the following AWS CloudFormation resources as needed\.

**`AWS::IAM::ManagedPolicy`**  
 *`LogicalId`:*`<connector‑LogicalId>Policy`   
 *Referenceable property:* N/A \(To reference this AWS CloudFormation resource, you must use the `LogicalId`\.\) 

**`AWS::SNS::TopicPolicy`**  
 *`LogicalId`:*`<connector‑LogicalId>TopicPolicy`   
 *Referenceable property:* N/A \(To reference this AWS CloudFormation resource, you must use the `LogicalId`\.\) 

**`AWS::SQS::QueuePolicy`**  
 *`LogicalId`:*`<connector‑LogicalId>QueuePolicy`   
 *Referenceable property:* N/A \(To reference this AWS CloudFormation resource, you must use the `LogicalId`\.\) 

**`AWS::Lambda::Permission`**  
 *`LogicalId`:*`<connector‑LogicalId><permission>LambdaPermission`   
 `<permission>` is a permission specified by the `Permissions` property\. For example, `Write`\.   
*Referenceable property:* N/A \(To reference this AWS CloudFormation resource, you must use the `LogicalId`\.\) 