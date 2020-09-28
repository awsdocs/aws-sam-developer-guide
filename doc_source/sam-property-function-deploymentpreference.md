# DeploymentPreference<a name="sam-property-function-deploymentpreference"></a>

Specifies the configurations to enable gradual Lambda deployments\. For more information about configuring gradual Lambda deployments, see [Deploying serverless applications gradually](automating-updates-to-serverless-apps.md)\.

**Note**: You must specify an `AutoPublishAlias` in your [AWS::Serverless::Function](sam-resource-function.md) to use a `DeploymentPreference` object, otherwise an error will result\.

## Syntax<a name="sam-property-function-deploymentpreference-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-deploymentpreference-syntax.yaml"></a>

```
  [Alarms](#sam-function-deploymentpreference-alarms): List
  [Enabled](#sam-function-deploymentpreference-enabled): Boolean
  [Hooks](#sam-function-deploymentpreference-hooks): Hooks
  [Role](#sam-function-deploymentpreference-role): String
  [TriggerConfigurations](#sam-function-deploymentpreference-triggerconfigurations): List
  [Type](#sam-function-deploymentpreference-type): String
```

## Properties<a name="sam-property-function-deploymentpreference-properties"></a>

 `Alarms`   <a name="sam-function-deploymentpreference-alarms"></a>
A list of CloudWatch alarms that you want to be triggered by any errors raised by the deployment\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Enabled`   <a name="sam-function-deploymentpreference-enabled"></a>
Whether this deployment preference is enabled\.  
*Type*: Boolean  
*Required*: No  
*Default*: True  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Hooks`   <a name="sam-function-deploymentpreference-hooks"></a>
Validation Lambda functions that are run before and after traffic shifting\.  
*Type*: [Hooks](sam-property-function-hooks.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Role`   <a name="sam-function-deploymentpreference-role"></a>
An IAM role ARN that CodeDeploy will use for traffic shifting\. An IAM role will not be created if this is provided\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `TriggerConfigurations`   <a name="sam-function-deploymentpreference-triggerconfigurations"></a>
A list of trigger configurations you want to associate with the deployment group\. Used to notify an SNS topic on lifecycle events\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[TriggerConfigurations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codedeploy-deploymentgroup.html#cfn-codedeploy-deploymentgroup-triggerconfigurations)` property of an `AWS::CodeDeploy::DeploymentGroup` resource\.

 `Type`   <a name="sam-function-deploymentpreference-type"></a>
There are two categories of deployment types at the moment: Linear and Canary\. For more information about available deployment types see [Deploying serverless applications gradually](automating-updates-to-serverless-apps.md)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-deploymentpreference--examples"></a>

### DeploymentPreference<a name="sam-property-function-deploymentpreference--examples--deploymentpreference"></a>

Example deployment preference

#### YAML<a name="sam-property-function-deploymentpreference--examples--deploymentpreference--yaml"></a>

```
DeploymentPreference:
  Enabled: True
  Type: Canary10Percent10Minutes 
  Alarms:
    - Ref: AliasErrorMetricGreaterThanZeroAlarm
    - Ref: LatestVersionErrorMetricGreaterThanZeroAlarm
  Hooks:
    PreTraffic:
      Ref: PreTrafficLambdaFunction
    PostTraffic:
      Ref: PostTrafficLambdaFunction
```