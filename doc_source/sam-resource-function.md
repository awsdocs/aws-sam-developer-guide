# AWS::Serverless::Function<a name="sam-resource-function"></a>

Creates a Lambda function, IAM execution role, and event source mappings which trigger the function\.

## Syntax<a name="sam-resource-function-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-resource-function-syntax.yaml"></a>

```
Type: AWS::Serverless::Function
Properties:
  [AssumeRolePolicyDocument](#sam-function-assumerolepolicydocument): JSON
  [AutoPublishAlias](#sam-function-autopublishalias): String
  [CodeUri](#sam-function-codeuri): String | [FunctionCode](sam-property-function-functioncode.md)
  [DeadLetterQueue](#sam-function-deadletterqueue): Map | [DeadLetterQueue](sam-property-function-deadletterqueue.md)
  [DeploymentPreference](#sam-function-deploymentpreference): [DeploymentPreference](sam-property-function-deploymentpreference.md)
  [Description](#sam-function-description): String
  [Environment](#sam-function-environment): [Environment](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-environment.html)
  [EventInvokeConfig](#sam-function-eventinvokeconfig): [EventInvokeConfiguration](sam-property-function-eventinvokeconfiguration.md)
  [Events](#sam-function-events): [EventSource](sam-property-function-eventsource.md)
  [FunctionName](#sam-function-functionname): String
  [Handler](#sam-function-handler): String
  [InlineCode](#sam-function-inlinecode): String
  [KmsKeyArn](#sam-function-kmskeyarn): String
  [Layers](#sam-function-layers): List
  [MemorySize](#sam-function-memorysize): Integer
  [PermissionsBoundary](#sam-function-permissionsboundary): String
  [Policies](#sam-function-policies): String | List | Map
  [ProvisionedConcurrencyConfig](#sam-function-provisionedconcurrencyconfig): [ProvisionedConcurrencyConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html#cfn-lambda-alias-provisionedconcurrencyconfig)
  [ReservedConcurrentExecutions](#sam-function-reservedconcurrentexecutions): Integer
  [Role](#sam-function-role): String
  [Runtime](#sam-function-runtime): String
  [Tags](#sam-function-tags): Map
  [Timeout](#sam-function-timeout): Integer
  [Tracing](#sam-function-tracing): String
  [VersionDescription](#sam-function-versiondescription): String
  [VpcConfig](#sam-function-vpcconfig): [VpcConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-vpcconfig.html)
```

## Properties<a name="sam-resource-function-properties"></a>

 `AssumeRolePolicyDocument`   <a name="sam-function-assumerolepolicydocument"></a>
Adds an AssumeRolePolicyDocument for the default created `Role` for this function\. If this property is not specified SAM adds a default assume role for this function\.  
*Type*: JSON  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[AssumeRolePolicyDocument](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html#cfn-iam-role-assumerolepolicydocument)` property of an `AWS::IAM::Role`\. SAM adds this property to the generated IAM Role for this Function\. If a Role ARN is provided for this Function, this property does nothing\.

 `AutoPublishAlias`   <a name="sam-function-autopublishalias"></a>
Name of the Lambda alias\. For more information about Lambda aliases, see [AWS Lambda Function Aliases](https://docs.aws.amazon.com/lambda/latest/dg/configuration-aliases.html)\.  
This AWS SAM property generates two additional resources: an [AWS::Lambda::Version](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-version.html) resource and an [AWS::Lambda::Alias](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html) resource\.  
The [AWS::Lambda::Version](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-version.html) resource has a logical id of `<function-logical-id>Version<sha>`, where the *<sha>* is 10 digits of the SHA256 of CodeUri\. This resource can be referenced in intrinsic functions by using the logical ID or `<function-logical-id>.Version`\.  
The [AWS::Lambda::Alias](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html) resource has a logical id of `<function-logical-id>Alias<alias-name>`, where `<alias-name>` is the alias name specified in this property\. This resource can be referenced in intrinsic functions by using the logical ID or `<function-logical-id>.Alias`\.  
For examples that use this property, see [Deploying Serverless Applications Gradually](automating-updates-to-serverless-apps.md)\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `CodeUri`   <a name="sam-function-codeuri"></a>
AWS S3 Uri, local file path, or [FunctionCode](sam-property-function-functioncode.md) object of the function code\.  
If an AWS S3 Uri or [FunctionCode](sam-property-function-functioncode.md) object is provided, the AWS S3 object referenced must be a valid [Lambda deployment package](https://docs.aws.amazon.com/lambda/latest/dg/deployment-package-v2.html)\.  
If a local file path is provided, the template must go through the workflow that includes the `sam deploy` or `sam package` command, in order for the code to be transformed properly\.  
**Note**: Either `CodeUri` or `InlineCode` is required\.  
*Type*: String \| [FunctionCode](sam-property-function-functioncode.md)  
*Required*: Conditional  
*CloudFormation Compatibility*: This property is similar to the `[Code](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-code)` property of an `AWS::Lambda::Function`\. The nested Amazon S3 properties are named differently\.

 `DeadLetterQueue`   <a name="sam-function-deadletterqueue"></a>
Configures SNS topic or SQS queue where Lambda sends events that it can't process\. For more information about dead letter queue functionality, see [AWS Lambda Function Dead Letter Queues](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html#dlq)\.  
*Type*: Map \| [DeadLetterQueue](sam-property-function-deadletterqueue.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[DeadLetterConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-deadletterconfig.html)` property of an `AWS::Lambda::Function`\. In CloudFormation the type is derived from the TargetArn, whereas in SAM you must pass the type along with the TargetArn\.

 `DeploymentPreference`   <a name="sam-function-deploymentpreference"></a>
Settings to enable gradual Lambda deployments\.  
If a `DeploymentPreference` object is specified, SAM will create an [AWS::CodeDeploy::Application](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codedeploy-application.html) called `ServerlessDeploymentApplication` \(one per stack\), an [AWS::CodeDeploy::DeploymentGroup](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codedeploy-deploymentgroup.html) called `<function-logical-id>DeploymentGroup`, and an [AWS::IAM::Role](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html) called `CodeDeployServiceRole`\.  
*Type*: [DeploymentPreference](sam-property-function-deploymentpreference.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.  
*See Also*: See the [Deploying Serverless Applications Gradually](automating-updates-to-serverless-apps.md) documentation for more information about this property\.

 `Description`   <a name="sam-function-description"></a>
Description of the function\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[Description](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-description)` property of an `AWS::Lambda::Function`\.

 `Environment`   <a name="sam-function-environment"></a>
Configuration for the runtime environment\.  
*Type*: [Environment](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-environment.html)  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[Environment](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-environment.html)` property of an `AWS::Lambda::Function`\.

 `EventInvokeConfig`   <a name="sam-function-eventinvokeconfig"></a>
The object describing event invoke config on a Lambda function\.  
*Type*: [EventInvokeConfiguration](sam-property-function-eventinvokeconfiguration.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `Events`   <a name="sam-function-events"></a>
Specifies the events that trigger this function\. Events consist of a type and a set of properties that depend on the type\.  
*Type*: [EventSource](sam-property-function-eventsource.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `FunctionName`   <a name="sam-function-functionname"></a>
A name for the function\. If you don't specify a name, a unique name will be generated for you\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[FunctionName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-functionname)` property of an `AWS::Lambda::Function`\.

 `Handler`   <a name="sam-function-handler"></a>
Function within your code that is called to begin execution\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is passed directly to the `[Handler](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-handler)` property of an `AWS::Lambda::Function`\.

 `InlineCode`   <a name="sam-function-inlinecode"></a>
Lambda function code written directly in the template\.  
**Note**: Either `CodeUri` or `InlineCode` is required\.  
*Type*: String  
*Required*: Conditional  
*CloudFormation Compatibility*: This property is passed directly to the `[ZipFile](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-code.html#cfn-lambda-function-code-zipfile)` property of the `AWS::Lambda::Function` `Code` data type\.

 `KmsKeyArn`   <a name="sam-function-kmskeyarn"></a>
The Amazon Resource Name \(ARN\) of an AWS Key Management Service \(AWS KMS\) key that Lambda uses to encrypt and decrypt your function's environment variables\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[KmsKeyArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-kmskeyarn)` property of an `AWS::Lambda::Function`\.

 `Layers`   <a name="sam-function-layers"></a>
List of LayerVersion ARNs that should be used by this function\. The order specified here is the order that they will be imported when running the Lambda function\.  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[Layers](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-layers)` property of an `AWS::Lambda::Function`\.

 `MemorySize`   <a name="sam-function-memorysize"></a>
Size of the memory allocated per invocation of the function in MB\.  
*Type*: Integer  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[MemorySize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-memorysize)` property of an `AWS::Lambda::Function`\.

 `PermissionsBoundary`   <a name="sam-function-permissionsboundary"></a>
ARN of a permissions boundary to use for this function's execution role\. This property only works if the Role is generated for you\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[PermissionsBoundary](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html#cfn-iam-role-permissionsboundary)` property of an `AWS::IAM::Role`\.

 `Policies`   <a name="sam-function-policies"></a>
One or more policies that this function needs, which will be appended to the default role for this function\.  
This property accepts a single string or a list of strings, and can be the name of AWS managed IAM policies or SAM Policy Templates, or inline IAM policy document\(s\) formatted in YAML\. If the Role property is set, this property has no meaning\.  
For more information about AWS managed IAM policies, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies)\. For more informationa about AWS SAM Policy Templates, see [AWS SAM Policy Templates](serverless-policy-templates.md)\. For more information about inline policies, see [Inline Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#inline-policies)\.  
*Type*: String \| List \| Map  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[Policies](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html#cfn-iam-role-policies)` property of an `AWS::IAM::Role`\. AWS SAM supports AWS Managed policy names and SAM Policy Templates in addition to JSON policy documents; CloudFormation only accepts JSON policy documents\.

 `ProvisionedConcurrencyConfig`   <a name="sam-function-provisionedconcurrencyconfig"></a>
Provisioned concurrency configuration of a function's alias\.  
**Note**: `ProvisionedConcurrencyConfig` can only be specified if the AutoPublishAlias is set, otherwise an error will result\.  
*Type*: [ProvisionedConcurrencyConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html#cfn-lambda-alias-provisionedconcurrencyconfig)  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[ProvisionedConcurrencyConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html#cfn-lambda-alias-provisionedconcurrencyconfig)` property of an `AWS::Lambda::Alias`\.

 `ReservedConcurrentExecutions`   <a name="sam-function-reservedconcurrentexecutions"></a>
The maximum of concurrent executions you want to reserve for the function\.  
For more information about this property see [AWS Lambda Function Scaling](https://docs.aws.amazon.com/lambda/latest/dg/scaling.html) in the AWS Lambda Developer Guide\.  
*Type*: Integer  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[ReservedConcurrentExecutions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-reservedconcurrentexecutions)` property of an `AWS::Lambda::Function`\.

 `Role`   <a name="sam-function-role"></a>
ARN of an IAM role to use as this function's execution role\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[Role](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-role)` property of an `AWS::Lambda::Function`\. This is required in AWS CloudFormation but not in AWS SAM\. If a role is not specified, one is created for you with a logical id of `<function-logical-id>Role`\.

 `Runtime`   <a name="sam-function-runtime"></a>
The runtime environment\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is passed directly to the `[Runtime](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-runtime)` property of an `AWS::Lambda::Function`\.

 `Tags`   <a name="sam-function-tags"></a>
A map \(string to string\) that specifies the tags added to the Lambda function and the corresponding IAM execution role\. Keys and values are limited to alphanumeric characters\. Keys can be 1 to 127 Unicode characters in length and cannot be prefixed with aws:\. Values can be 1 to 255 Unicode characters in length\.  
*Type*: Map  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[Tags](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-tags)` property of an `AWS::Lambda::Function`\. The Tags property in SAM consists of Key:Value pairs; in CloudFormation it consists of a list of Tag objects\. When the stack is created, SAM automatically adds a `lambda:createdBy:SAM` tag to this Lambda function and the corresponding IAM execution role\.

 `Timeout`   <a name="sam-function-timeout"></a>
Maximum time that the function can run before it is killed in seconds\.  
*Type*: Integer  
*Required*: No  
*Default*: 3  
*CloudFormation Compatibility*: This property is passed directly to the `[Timeout](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-timeout)` property of an `AWS::Lambda::Function`\.

 `Tracing`   <a name="sam-function-tracing"></a>
String that specifies the function's X\-Ray tracing mode\. For more information about X\-Ray, see [Using AWS X\-Ray](https://docs.aws.amazon.com/lambda/latest/dg/lambda-x-ray.html) in the AWS Lambda Developer Guide\.  
Supported values: Active and PassThrough  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[TracingConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-tracingconfig)` property of an `AWS::Lambda::Function`\. If Tracing is set to `Active` then AWS SAM adds the `arn:aws:iam::aws:policy/AWSXrayWriteOnlyAccess` policy to the Lambda role\.

 `VersionDescription`   <a name="sam-function-versiondescription"></a>
A string that specifies the Description field which will be added on the new lambda version resource\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[Description](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-version.html#cfn-lambda-version-description)` property of an `AWS::Lambda::Version`\.

 `VpcConfig`   <a name="sam-function-vpcconfig"></a>
Configuration to enable this function to access private resources within your VPC\.  
*Type*: [VpcConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-vpcconfig.html)  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[VpcConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-vpcconfig.html)` property of an `AWS::Lambda::Function`\.

## Return Values<a name="sam-resource-function-return-values"></a>

### Ref<a name="sam-resource-function-return-values-ref"></a>

When the logical ID of this resource is provided to the Ref intrinsic function, it returns the resource name of the underlying Lambda function\.

For more information about using the Ref function, see [Ref](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)\. 

### Fn::GetAtt<a name="sam-resource-function-return-values-fn--getatt"></a>

Fn::GetAtt returns a value for a specified attribute of this type\. The following are the available attributes and sample return values\. 

For more information about using Fn::GetAtt, see [Fn::GetAtt](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html)\. 

#### GetAtt<a name="sam-resource-function-return-values-fn--getatt-fn--getatt"></a>

`Arn`  <a name="Arn-fn::getatt"></a>
The Amazon Resource Name \(ARN\) of the underlying Lambda function\.

## Examples<a name="sam-resource-function--examples"></a>

### Simple Function<a name="sam-resource-function--examples--simple-function"></a>

Base case example of an AWS::Serverless::Function resource\.

#### YAML<a name="sam-resource-function--examples--simple-function--yaml"></a>

```
Type: AWS::Serverless::Function
Properties:
  Handler: index.handler
  Runtime: python3.6
  CodeUri: s3://bucket/key
```

### Function Properties Example<a name="sam-resource-function--examples--function-properties-example"></a>

Example of an AWS::Serverless::Function that uses InlineCode, Tracing, Policies, and Layers\.

#### YAML<a name="sam-resource-function--examples--function-properties-example--yaml"></a>

```
Type: AWS::Serverless::Function
Properties:
  Handler: index.handler
  Runtime: python3.6
  InlineCode: |
    def handler(event, context):
      print("Hello, world!")
  ReservedConcurrentExecutions: 30
  Layers:
    - Ref: MyLayer
  Tracing: Active
  Timeout: 120
  Policies:
    - AWSLambdaExecute
    - Version: '2012-10-17' 
      Statement:
        - Effect: Allow
          Action:
            - s3:GetObject
            - s3:GetObjectACL
          Resource: 'arn:aws:s3:::my-bucket/*'
```