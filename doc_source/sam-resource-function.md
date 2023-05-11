# AWS::Serverless::Function<a name="sam-resource-function"></a>

Creates an AWS Lambda function, an AWS Identity and Access Management \(IAM\) execution role, and event source mappings that trigger the function\.

The [AWS::Serverless::Function](#sam-resource-function) resource also supports the `Metadata` resource attribute, so you can instruct AWS SAM to build custom runtimes that your application requires\. For more information about building custom runtimes, see [Building custom runtimes](building-custom-runtimes.md)\.

**Note**  
When you deploy to AWS CloudFormation, AWS SAM transforms your AWS SAM resources into AWS CloudFormation resources\. For more information, see [Generated AWS CloudFormation resources](sam-specification-generated-resources.md)\.

## Syntax<a name="sam-resource-function-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-resource-function-syntax.yaml"></a>

```
Type: AWS::Serverless::Function
Properties:
  [Architectures](#sam-function-architectures): List
  [AssumeRolePolicyDocument](#sam-function-assumerolepolicydocument): JSON
  [AutoPublishAlias](#sam-function-autopublishalias): String
  AutoPublishAliasAllProperties: Boolean
  [AutoPublishCodeSha256](#sam-function-autopublishcodesha256): String
  [CodeSigningConfigArn](#sam-function-codesigningconfigarn): String
  [CodeUri](#sam-function-codeuri): String | FunctionCode
  [DeadLetterQueue](#sam-function-deadletterqueue): Map | DeadLetterQueue
  [DeploymentPreference](#sam-function-deploymentpreference): DeploymentPreference
  [Description](#sam-function-description): String
  [Environment](#sam-function-environment): [Environment](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-environment.html)
  [EphemeralStorage](#sam-function-ephemeralstorage): [EphemeralStorage](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-ephemeralstorage)
  [EventInvokeConfig](#sam-function-eventinvokeconfig): EventInvokeConfiguration
  [Events](#sam-function-events): EventSource
  [FileSystemConfigs](#sam-function-filesystemconfigs): List
  [FunctionName](#sam-function-functionname): String
  [FunctionUrlConfig](#sam-function-functionurlconfig): FunctionUrlConfig
  [Handler](#sam-function-handler): String
  [ImageConfig](#sam-function-imageconfig): [ImageConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-imageconfig)
  [ImageUri](#sam-function-imageuri): String
  [InlineCode](#sam-function-inlinecode): String
  [KmsKeyArn](#sam-function-kmskeyarn): String
  [Layers](#sam-function-layers): List
  [MemorySize](#sam-function-memorysize): Integer
  [PackageType](#sam-function-packagetype): String
  [PermissionsBoundary](#sam-function-permissionsboundary): String
  [Policies](#sam-function-policies): String | List | Map
  [ProvisionedConcurrencyConfig](#sam-function-provisionedconcurrencyconfig): [ProvisionedConcurrencyConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html#cfn-lambda-alias-provisionedconcurrencyconfig)
  [ReservedConcurrentExecutions](#sam-function-reservedconcurrentexecutions): Integer
  [Role](#sam-function-role): String
  [RolePath](#sam-function-rolepath): String
  [Runtime](#sam-function-runtime): String
  RuntimeManagementConfig: [RuntimeManagementConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-runtimemanagementconfig.html)
  SnapStart: [SnapStart](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-snapstart.html)
  [Tags](#sam-function-tags): Map
  [Timeout](#sam-function-timeout): Integer
  [Tracing](#sam-function-tracing): String
  [VersionDescription](#sam-function-versiondescription): String
  [VpcConfig](#sam-function-vpcconfig): [VpcConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-vpcconfig.html)
```

## Properties<a name="sam-resource-function-properties"></a>

 `Architectures`   <a name="sam-function-architectures"></a>
The instruction set architecture for the function\.  
For more information about this property, see [Lambda instruction set architectures](https://docs.aws.amazon.com/lambda/latest/dg/foundation-arch.html) in the *AWS Lambda Developer Guide*\.  
*Valid values*: One of `x86_64` or `arm64`  
*Type*: List  
*Required*: No  
*Default*: `x86_64`  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Architectures](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-architectures)` property of an `AWS::Lambda::Function` resource\.

 `AssumeRolePolicyDocument`   <a name="sam-function-assumerolepolicydocument"></a>
Adds an AssumeRolePolicyDocument for the default created `Role` for this function\. If this property isn't specified, AWS SAM adds a default assume role for this function\.  
*Type*: JSON  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[AssumeRolePolicyDocument](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html#cfn-iam-role-assumerolepolicydocument)` property of an `AWS::IAM::Role` resource\. AWS SAM adds this property to the generated IAM role for this function\. If a role's Amazon Resource Name \(ARN\) is provided for this function, this property does nothing\.

 `AutoPublishAlias`   <a name="sam-function-autopublishalias"></a>
The name of the Lambda alias\. For more information about Lambda aliases, see [Lambda function aliases](https://docs.aws.amazon.com/lambda/latest/dg/configuration-aliases.html) in the *AWS Lambda Developer Guide*\. For examples that use this property, see [Deploying serverless applications gradually](automating-updates-to-serverless-apps.md)\.  
AWS SAM generates [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-version.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-version.html) and [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html) resources when this property is set\. For information about this scenario, see [AutoPublishAlias property is specified](sam-specification-generated-resources-function.md#sam-specification-generated-resources-function-autopublishalias)\. For general information about generated AWS CloudFormation resources, see [Generated AWS CloudFormation resources](sam-specification-generated-resources.md)\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AutoPublishAliasAllProperties`   <a name="sam-function-autopublishaliasallproperties"></a>
Specifies when a new [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-version.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-version.html) is created\. When `true`, a new Lambda version is created when any property in the Lambda function is modified\. When `false`, a new Lambda version is created only when any of the following properties are modified:  
+ `Environment`, `MemorySize`, or `SnapStart`\.
+ Any change that results in an update to the `Code` property, such as `CodeDict`, `ImageUri`, or `InlineCode`\.
This property requires `AutoPublishAlias` to be defined\.  
If `AutoPublishSha256` is also specified, its behavior takes precedence over `AutoPublishAliasAllProperties: true`\.  
*Type*: Boolean  
*Required*: No  
*Default value*: `false`  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AutoPublishCodeSha256`   <a name="sam-function-autopublishcodesha256"></a>
The string value that is used, along with the value in `CodeUri`, to determine whether a new Lambda version should be published\. This property is only used when `AutoPublishAlias` is also defined\.  
This property addresses a problem that occurs when an AWS SAM template has the following characteristics: the `DeploymentPreference` object is configured for gradual deployments \(as described in [Deploying serverless applications gradually](automating-updates-to-serverless-apps.md)\), the `AutoPublishAlias` property is set and doesn't change between deployments, and the `CodeUri` property is set and doesn't change between deployments\.  
This scenario can occur when the deployment package stored in an Amazon Simple Storage Service \(Amazon S3\) location is replaced by a new deployment package that contains updated Lambda function code, but the `CodeUri` property remains unchanged \(as opposed to the new deployment package being uploaded to a new Amazon S3 location and the `CodeUri` being changed to the new location\)\.  
In this scenario, to trigger the gradual deployment successfully, you must provide a unique value for `AutoPublishCodeSha256`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `CodeSigningConfigArn`   <a name="sam-function-codesigningconfigarn"></a>
The ARN of the [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-codesigningconfig.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-codesigningconfig.html) resource, used to enable code signing for this function\. For more information about code signing, see [Configuring code signing for AWS SAM applications](authoring-codesigning.md)\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[CodeSigningConfigArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-codesigningconfigarn)` property of an `AWS::Lambda::Function` resource\.

 `CodeUri`   <a name="sam-function-codeuri"></a>
The function code's Amazon S3 URI, path to local folder, or [FunctionCode](sam-property-function-functioncode.md) object\. This property only applies if the `PackageType` property is set to `Zip`, otherwise it is ignored\.  
**Notes**:  
1\. If the `PackageType` property is set to `Zip` \(default\), then one of `CodeUri` or `InlineCode` is required\.  
2\. If an Amazon S3 URI or [FunctionCode](sam-property-function-functioncode.md) object is provided, the Amazon S3 object referenced must be a valid [Lambda deployment package](https://docs.aws.amazon.com/lambda/latest/dg/deployment-package-v2.html)\.  
3\. If the path to a local folder is provided, for the code to be transformed properly the template must go through the workflow that includes [sam build](sam-cli-command-reference-sam-build.md) followed by either [sam deploy](sam-cli-command-reference-sam-deploy.md) or [sam package](sam-cli-command-reference-sam-package.md)\. By default, relative paths are resolved with respect to the AWS SAM template's location\.  
*Type*: String \| [FunctionCode](sam-property-function-functioncode.md)  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is similar to the `[Code](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-code)` property of an `AWS::Lambda::Function` resource\. The nested Amazon S3 properties are named differently\.

 `DeadLetterQueue`   <a name="sam-function-deadletterqueue"></a>
Configures an Amazon Simple Notification Service \(Amazon SNS\) topic or Amazon Simple Queue Service \(Amazon SQS\) queue where Lambda sends events that it can't process\. For more information about dead\-letter queue functionality, see [AWS Lambda function dead letter queues](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html#dlq) in the *AWS Lambda Developer Guide*\.  
If your Lambda function's event source is an Amazon SQS queue, configure a dead\-letter queue for the source queue, not for the Lambda function\. The dead\-letter queue that you configure for a function is used for the function's [asynchronous invocation queue](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html), not for event source queues\.
*Type*: Map \| [DeadLetterQueue](sam-property-function-deadletterqueue.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[DeadLetterConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-deadletterconfig.html)` property of an `AWS::Lambda::Function` resource\. In AWS CloudFormation the type is derived from the `TargetArn`, whereas in AWS SAM you must pass the type along with the `TargetArn`\.

 `DeploymentPreference`   <a name="sam-function-deploymentpreference"></a>
The settings to enable gradual Lambda deployments\.  
If a `DeploymentPreference` object is specified, AWS SAM creates an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codedeploy-application.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codedeploy-application.html) called `ServerlessDeploymentApplication` \(one per stack\), an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codedeploy-deploymentgroup.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codedeploy-deploymentgroup.html) called `<function-logical-id>DeploymentGroup`, and an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html) called `CodeDeployServiceRole`\.  
*Type*: [DeploymentPreference](sam-property-function-deploymentpreference.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*See also*: For more information about this property, see [Deploying serverless applications gradually](automating-updates-to-serverless-apps.md)\.

 `Description`   <a name="sam-function-description"></a>
A description of the function\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Description](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-description)` property of an `AWS::Lambda::Function` resource\.

 `Environment`   <a name="sam-function-environment"></a>
The configuration for the runtime environment\.  
*Type*: [Environment](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-environment.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Environment](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-environment.html)` property of an `AWS::Lambda::Function` resource\.

 `EphemeralStorage`   <a name="sam-function-ephemeralstorage"></a>
An object that specifies the disk space, in MB, available to your Lambda function in `/tmp`\.  
For more information about this property, see [Lambda execution environment](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-context.html) in the *AWS Lambda Developer Guide*\.  
*Type*: [EphemeralStorage](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-ephemeralstorage)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EphemeralStorage](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-ephemeralstorage)` property of an `AWS::Lambda::Function` resource\.

 `EventInvokeConfig`   <a name="sam-function-eventinvokeconfig"></a>
The object that describes event invoke configuration on a Lambda function\.  
*Type*: [EventInvokeConfiguration](sam-property-function-eventinvokeconfiguration.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Events`   <a name="sam-function-events"></a>
Specifies the events that trigger this function\. Events consist of a type and a set of properties that depend on the type\.  
*Type*: [EventSource](sam-property-function-eventsource.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `FileSystemConfigs`   <a name="sam-function-filesystemconfigs"></a>
List of [FileSystemConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-filesystemconfig.html) objects that specify the connection settings for an Amazon Elastic File System \(Amazon EFS\) file system\.  
If your template contains an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-efs-mounttarget.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-efs-mounttarget.html) resource, you must also specify a `DependsOn` resource attribute to ensure that the mount target is created or updated before the function\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[FileSystemConfigs](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-filesystemconfigs)` property of an `AWS::Lambda::Function` resource\.

 `FunctionName`   <a name="sam-function-functionname"></a>
A name for the function\. If you don't specify a name, a unique name is generated for you\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[FunctionName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-functionname)` property of an `AWS::Lambda::Function` resource\.

 `FunctionUrlConfig`   <a name="sam-function-functionurlconfig"></a>
The object that describes a function URL\. A function URL is an HTTPS endpoint that you can use to invoke your function\.  
For more information, see [Function URLs](https://docs.aws.amazon.com/lambda/latest/dg/lambda-urls.html) in the *AWS Lambda Developer Guide*\.  
*Type*: [FunctionUrlConfig](sam-property-function-functionurlconfig.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Handler`   <a name="sam-function-handler"></a>
The function within your code that is called to begin execution\. This property is only required if the `PackageType` property is set to `Zip`\.  
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Handler](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-handler)` property of an `AWS::Lambda::Function` resource\.

 `ImageConfig`   <a name="sam-function-imageconfig"></a>
The object used to configure Lambda container image settings\. For more information, see [Using container images with Lambda](https://docs.aws.amazon.com/lambda/latest/dg/lambda-images.html) in the *AWS Lambda Developer Guide*\.  
*Type*: [ImageConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-imageconfig)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ImageConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-imageconfig)` property of an `AWS::Lambda::Function` resource\.

 `ImageUri`   <a name="sam-function-imageuri"></a>
The URI of the Amazon Elastic Container Registry \(Amazon ECR\) repository for the Lambda function's container image\. This property only applies if the `PackageType` property is set to `Image`, otherwise it is ignored\. For more information, see [Using container images with Lambda](https://docs.aws.amazon.com/lambda/latest/dg/lambda-images.html) in the *AWS Lambda Developer Guide*\.  
If the `PackageType` property is set to `Image`, then either `ImageUri` is required, or you must build your application with necessary `Metadata` entries in the AWS SAM template file\. For more information, see [Building applications](serverless-sam-cli-using-build.md)\.
Building your application with necessary `Metadata` entries takes precedence over `ImageUri`, so if you specify both then `ImageUri` is ignored\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ImageUri](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-code.html#cfn-lambda-function-code-imageuri)` property of the `AWS::Lambda::Function` `Code` data type\.

 `InlineCode`   <a name="sam-function-inlinecode"></a>
The Lambda function code that is written directly in the template\. This property only applies if the `PackageType` property is set to `Zip`, otherwise it is ignored\.  
If the `PackageType` property is set to `Zip` \(default\), then one of `CodeUri` or `InlineCode` is required\.
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ZipFile](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-code.html#cfn-lambda-function-code-zipfile)` property of the `AWS::Lambda::Function` `Code` data type\.

 `KmsKeyArn`   <a name="sam-function-kmskeyarn"></a>
The ARN of an AWS Key Management Service \(AWS KMS\) key that Lambda uses to encrypt and decrypt your function's environment variables\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[KmsKeyArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-kmskeyarn)` property of an `AWS::Lambda::Function` resource\.

 `Layers`   <a name="sam-function-layers"></a>
The list of `LayerVersion` ARNs that this function should use\. The order specified here is the order in which they will be imported when running the Lambda function\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Layers](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-layers)` property of an `AWS::Lambda::Function` resource\.

 `MemorySize`   <a name="sam-function-memorysize"></a>
The size of the memory in MB allocated per invocation of the function\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MemorySize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-memorysize)` property of an `AWS::Lambda::Function` resource\.

 `PackageType`   <a name="sam-function-packagetype"></a>
The deployment package type of the Lambda function\. For more information, see [Lambda deployment packages](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-package.html) in the *AWS Lambda Developer Guide*\.  
**Notes**:  
1\. If this property is set to `Zip` \(default\), then either `CodeUri` or `InlineCode` applies, and `ImageUri` is ignored\.  
2\. If this property is set to `Image`, then only `ImageUri` applies, and both `CodeUri` and `InlineCode` are ignored\. The Amazon ECR repository required to store the function's container image can be auto created by the AWS SAM CLI\. For more information, see [sam deploy](sam-cli-command-reference-sam-deploy.md)\.  
*Valid values*: `Zip` or `Image`  
*Type*: String  
*Required*: No  
*Default*: `Zip`  
*AWS CloudFormation compatibility*: This property is passed directly to the `[PackageType](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-packagetype)` property of an `AWS::Lambda::Function` resource\.

 `PermissionsBoundary`   <a name="sam-function-permissionsboundary"></a>
The ARN of a permissions boundary to use for this function's execution role\. This property works only if the role is generated for you\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[PermissionsBoundary](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html#cfn-iam-role-permissionsboundary)` property of an `AWS::IAM::Role` resource\.

 `Policies`   <a name="sam-function-policies"></a>
Permission policies for this function\. Policies will be appended to the function's default AWS Identity and Access Management \(IAM\) execution role\.  
This property accepts a single value or list of values\. Allowed values include:  
+ [AWS SAM policy templates](serverless-policy-templates.md)\.
+ The ARN of an [AWS managed policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) or [ customer managed policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies)\.
+ The name of an AWS managed policy from the following [ list](https://github.com/aws/serverless-application-model/blob/develop/samtranslator/internal/data/aws_managed_policies.json)\.
+ An [ inline IAM policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#inline-policies) formatted in YAML as a map\.
If you set the `Role` property, this property is ignored\.
*Type*: String \| List \| Map  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[Policies](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html#cfn-iam-role-policies)` property of an `AWS::IAM::Role` resource\.

 `ProvisionedConcurrencyConfig`   <a name="sam-function-provisionedconcurrencyconfig"></a>
The provisioned concurrency configuration of a function's alias\.  
`ProvisionedConcurrencyConfig` can be specified only if the `AutoPublishAlias` is set\. Otherwise, an error results\.
*Type*: [ProvisionedConcurrencyConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html#cfn-lambda-alias-provisionedconcurrencyconfig)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ProvisionedConcurrencyConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html#cfn-lambda-alias-provisionedconcurrencyconfig)` property of an `AWS::Lambda::Alias` resource\.

 `ReservedConcurrentExecutions`   <a name="sam-function-reservedconcurrentexecutions"></a>
The maximum number of concurrent executions that you want to reserve for the function\.  
For more information about this property, see [Lambda Function Scaling](https://docs.aws.amazon.com/lambda/latest/dg/scaling.html) in the *AWS Lambda Developer Guide*\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ReservedConcurrentExecutions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-reservedconcurrentexecutions)` property of an `AWS::Lambda::Function` resource\.

 `Role`   <a name="sam-function-role"></a>
The ARN of an IAM role to use as this function's execution role\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[Role](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-role)` property of an `AWS::Lambda::Function` resource\. This is required in AWS CloudFormation but not in AWS SAM\. If a role isn't specified, one is created for you with a logical ID of `<function-logical-id>Role`\.

 `RolePath`   <a name="sam-function-rolepath"></a>
The path to the function's IAM execution role\.  
Use this property when the role is generated for you\. Do not use when the role is specified with the `Role` property\.  
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Path](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html#cfn-iam-role-path)` property of an `AWS::IAM::Role` resource\.

 `Runtime`   <a name="sam-function-runtime"></a>
The identifier of the function's [runtime](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html)\. This property is only required if the `PackageType` property is set to `Zip`\.  
If you specify the `provided` identifier for this property, you can use the `Metadata` resource attribute to instruct AWS SAM to build the custom runtime that this function requires\. For more information about building custom runtimes, see [Building custom runtimes](building-custom-runtimes.md)\.
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Runtime](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-runtime)` property of an `AWS::Lambda::Function` resource\.

 `RuntimeManagementConfig`   <a name="sam-function-runtimemanagementconfig"></a>
Configure runtime management options for your Lambda functions such as runtime environment updates, rollback behavior, and selecting a specific runtime version\. To learn more, see [Lambda runtime updates](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-update.html) in the *AWS Lambda Developer Guide*\.  
If `AutoPublishAlias` is configured, `RuntimeManagementConfig` will apply to both `$LATEST` and to the newly created version of the function\.
*Type*: [RuntimeManagementConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-runtimemanagementconfig.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ RuntimeManagementConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-runtimemanagementconfig.html)` property of an `AWS::Lambda::Function` resource\.

 `SnapStart`   <a name="sam-function-snapstart"></a>
Create a snapshot of any new Lambda function version\. A snapshot is a cached state of your initialized function, including all of its dependencies\. The function is initialized just once and the cached state is reused for all future invocations, improving application performance by reducing the number of times your function must be initialized\. To learn more, see [Improving startup performance with Lambda SnapStart](https://docs.aws.amazon.com/lambda/latest/dg/snapstart.html) in the *AWS Lambda Developer Guide*\.  
*Type*: [SnapStart](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-snapstart.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[SnapStart](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-snapstart.html)` property of an `AWS::Lambda::Function` resource\.

 `Tags`   <a name="sam-function-tags"></a>
A map \(string to string\) that specifies the tags added to this function\. For details about valid keys and values for tags, see [Tag Key and Value Requirements](https://docs.aws.amazon.com/lambda/latest/dg/configuration-tags.html#configuration-tags-restrictions) in the *AWS Lambda Developer Guide*\.  
When the stack is created, AWS SAM automatically adds a `lambda:createdBy:SAM` tag to this Lambda function, and to the default roles that are generated for this function\.  
*Type*: Map  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[Tags](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-tags)` property of an `AWS::Lambda::Function` resource\. The `Tags` property in AWS SAM consists of key\-value pairs \(whereas in AWS CloudFormation this property consists of a list of `Tag` objects\)\. Also, AWS SAM automatically adds a `lambda:createdBy:SAM` tag to this Lambda function, and to the default roles that are generated for this function\.

 `Timeout`   <a name="sam-function-timeout"></a>
The maximum time in seconds that the function can run before it is stopped\.  
*Type*: Integer  
*Required*: No  
*Default*: 3  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Timeout](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-timeout)` property of an `AWS::Lambda::Function` resource\.

 `Tracing`   <a name="sam-function-tracing"></a>
The string that specifies the function's X\-Ray tracing mode\. For more information about X\-Ray, see [Using AWS Lambda with AWS X\-Ray](https://docs.aws.amazon.com/lambda/latest/dg/lambda-x-ray.html) in the *AWS Lambda Developer Guide*\.  
*Valid values*: `Active` or `PassThrough`  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[TracingConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-tracingconfig)` property of an `AWS::Lambda::Function` resource\. If the `Tracing` property is set to `Active` and the `Role` property is not specified, then AWS SAM adds the `arn:aws:iam::aws:policy/AWSXrayWriteOnlyAccess` policy to the Lambda execution role that it creates for you\.

 `VersionDescription`   <a name="sam-function-versiondescription"></a>
Specifies the `Description` field that is added on the new Lambda version resource\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Description](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-version.html#cfn-lambda-version-description)` property of an `AWS::Lambda::Version` resource\.

 `VpcConfig`   <a name="sam-function-vpcconfig"></a>
The configuration that enables this function to access private resources within your virtual private cloud \(VPC\)\.  
*Type*: [VpcConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-vpcconfig.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[VpcConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-function-vpcconfig.html)` property of an `AWS::Lambda::Function` resource\.

## Return Values<a name="sam-resource-function-return-values"></a>

### Ref<a name="sam-resource-function-return-values-ref"></a>

When the logical ID of this resource is provided to the `Ref` intrinsic function, it returns the resource name of the underlying Lambda function\.

For more information about using the `Ref` function, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html) in the *AWS CloudFormation User Guide*\. 

### Fn::GetAtt<a name="sam-resource-function-return-values-fn--getatt"></a>

`Fn::GetAtt` returns a value for a specified attribute of this type\. The following are the available attributes and sample return values\. 

For more information about using `Fn::GetAtt`, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html) in the *AWS CloudFormation User Guide*\. 

`Arn`  <a name="Arn-fn::getatt"></a>
The ARN of the underlying Lambda function\.

## Examples<a name="sam-resource-function--examples"></a>

### Simple function<a name="sam-resource-function--examples--simple-function"></a>

The following is a basic example of an [AWS::Serverless::Function](#sam-resource-function) resource of package type `Zip` \(default\) and function code in an Amazon S3 bucket\.

#### YAML<a name="sam-resource-function--examples--simple-function--yaml"></a>

```
Type: AWS::Serverless::Function
Properties:
  Handler: index.handler
  Runtime: python3.9
  CodeUri: s3://bucket-name/key-name
```

### Function properties example<a name="sam-resource-function--examples--function-properties-example"></a>

The following is an example of an [AWS::Serverless::Function](#sam-resource-function) of package type `Zip` \(default\) that uses `InlineCode`, `Layers`, `Tracing`, `Policies`, `Amazon EFS`, and an `Api` event source\.

#### YAML<a name="sam-resource-function--examples--function-properties-example--yaml"></a>

```
Type: AWS::Serverless::Function
DependsOn: MyMountTarget        # This is needed if an AWS::EFS::MountTarget resource is declared for EFS
Properties:
  Handler: index.handler
  Runtime: python3.9
  InlineCode: |
    def handler(event, context):
      print("Hello, world!")
  ReservedConcurrentExecutions: 30
  Layers:
    - Ref: MyLayer
  Tracing: Active
  Timeout: 120
  FileSystemConfigs:
    - Arn: !Ref MyEfsFileSystem
      LocalMountPath: /mnt/EFS
  Policies:
    - AWSLambdaExecute
    - Version: '2012-10-17' 
      Statement:
        - Effect: Allow
          Action:
            - s3:GetObject
            - s3:GetObjectACL
          Resource: 'arn:aws:s3:::my-bucket/*'
  Events:
    ApiEvent:
      Type: Api
      Properties:
        Path: /path
        Method: get
```

### ImageConfig example<a name="sam-resource-function--examples--imageconfig-example"></a>

The following is an example of an `ImageConfig` for a Lambda function of package type `Image`\.

#### YAML<a name="sam-resource-function--examples--imageconfig-example--yaml"></a>

```
HelloWorldFunction:
  Type: AWS::Serverless::Function
  Properties:
    PackageType: Image
    ImageUri: account-id.dkr.ecr.region.amazonaws.com/ecr-repo-name:image-name
    ImageConfig:
      Command:
        - "app.lambda_handler"
      EntryPoint:
        - "entrypoint1"
      WorkingDirectory: "workDir"
```

### RuntimeManagementConfig examples<a name="sam-resource-function--examples--runtimemanagementconfig-examples"></a>

A Lambda function configured to update its runtime environment according to current behavior:

```
TestFunction
  Type: AWS::Serverless::Function
  Properties:
    ...
    Runtime: python3.9
    RuntimeManagementConfig:
      UpdateRuntimeOn: Auto
```

A Lambda function configured to update its runtime environment when the function is updated:

```
TestFunction
  Type: AWS::Serverless::Function
  Properties:
    ...
    Runtime: python3.9
    RuntimeManagementConfig:
      UpdateRuntimeOn: FunctionUpdate
```

A Lambda function configured to update its runtime environment manually:

```
TestFunction
  Type: AWS::Serverless::Function
  Properties:
    ...
    Runtime: python3.9
    RuntimeManagementConfig:
      RuntimeVersionArn: arn:aws:lambda:us-east-1::runtime:4c459dd0104ee29ec65dcad056c0b3ddbe20d6db76b265ade7eda9a066859b1e
      UpdateRuntimeOn: Manual
```

### SnapStart examples<a name="sam-resource-function--examples-snapstart-examples"></a>

Example of a Lambda function with SnapStart turned on for future versions:

```
TestFunc
  Type: AWS::Serverless::Function
  Properties:
    ...
    SnapStart:
      ApplyOn: PublishedVersions
```