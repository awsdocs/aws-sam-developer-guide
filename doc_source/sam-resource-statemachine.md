# AWS::Serverless::StateMachine<a name="sam-resource-statemachine"></a>

Creates an AWS Step Functions state machine, which you can use to orchestrate AWS Lambda functions and other AWS resources to form complex and robust workflows\.

For more information about Step Functions, see the [AWS Step Functions Developer Guide](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)\.

**Note**: To manage AWS SAM templates that contain Step Functions state machines, you must use version 0\.52\.0 or later of the AWS SAM CLI\. To check which version you have, run the command `sam --version`\.

## Syntax<a name="sam-resource-statemachine-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-resource-statemachine-syntax.yaml"></a>

```
Type: AWS::Serverless::StateMachine
Properties:
  [Definition](#sam-statemachine-definition): Map
  [DefinitionSubstitutions](#sam-statemachine-definitionsubstitutions): Map
  [DefinitionUri](#sam-statemachine-definitionuri): String | [S3Location](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-definitions3location)
  [Events](#sam-statemachine-events): EventSource
  [Logging](#sam-statemachine-logging): [LoggingConfiguration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-loggingconfiguration)
  [Name](#sam-statemachine-name): String
  [Policies](#sam-statemachine-policies): String | List | Map
  [Role](#sam-statemachine-role): String
  [Tags](#sam-statemachine-tags): Map
  [Tracing](#sam-statemachine-tracing): [TracingConfiguration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-tracingconfiguration)
  [Type](#sam-statemachine-type): String
```

## Properties<a name="sam-resource-statemachine-properties"></a>

 `Definition`   <a name="sam-statemachine-definition"></a>
The state machine definition is an object, where the format of the object matches the format of your AWS SAM template file, for example, JSON or YAML\. State machine definitions adhere to the [Amazon States Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html)\.  
For an example of an inline state machine definition, see [Examples](#sam-resource-statemachine--examples)\.  
You must provide either a `Definition` or a `DefinitionUri`\.  
*Type*: Map  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `DefinitionSubstitutions`   <a name="sam-statemachine-definitionsubstitutions"></a>
A string\-to\-string map that specifies the mappings for placeholder variables in the state machine definition\. This enables you to inject values obtained at runtime \(for example, from intrinsic functions\) into the state machine definition\.  
*Type*: Map  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[DefinitionSubstitutions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-definitionsubstitutions)` property of an `AWS::StepFunctions::StateMachine` resource\. If any intrinsic functions are specified in an inline state machine definition, AWS SAM adds entries to this property to inject them into the state machine definition\.

 `DefinitionUri`   <a name="sam-statemachine-definitionuri"></a>
The Amazon Simple Storage Service \(Amazon S3\) URI or local file path of the state machine definition written in the [Amazon States Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html)\.  
If you provide a local file path, the template must go through the workflow that includes the `sam deploy` or `sam package` command to correctly transform the definition\. To do this, you must use version 0\.52\.0 or later of the AWS SAM CLI\.  
You must provide either a `Definition` or a `DefinitionUri`\.  
*Type*: String \| [S3Location](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-definitions3location)  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is passed directly to the `[DefinitionS3Location](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-definitions3location)` property of an `AWS::StepFunctions::StateMachine` resource\.

 `Events`   <a name="sam-statemachine-events"></a>
Specifies the events that trigger this state machine\. Events consist of a type and a set of properties that depend on the type\.  
*Type*: [EventSource](sam-property-statemachine-statemachineeventsource.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Logging`   <a name="sam-statemachine-logging"></a>
Defines which execution history events are logged and where they are logged\.  
*Type*: [LoggingConfiguration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-loggingconfiguration)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[LoggingConfiguration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-loggingconfiguration)` property of an `AWS::StepFunctions::StateMachine` resource\.

 `Name`   <a name="sam-statemachine-name"></a>
The name of the state machine\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[StateMachineName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-statemachinename)` property of an `AWS::StepFunctions::StateMachine` resource\.

 `Policies`   <a name="sam-statemachine-policies"></a>
One or more policies that this state machine's execution role needs\.  
This property accepts a single string or a list of strings\. The property can be the name of AWS managed AWS Identity and Access Management \(IAM\) policies, AWS SAM policy templates, or one or more inline policy documents formatted as a map\.  
You provide either a `Role` or `Policies`\.  
If the `Role` property is set, this property is ignored\.  
*Type*: String \| List \| Map  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Role`   <a name="sam-statemachine-role"></a>
The Amazon Resource Name \(ARN\) of an IAM role to use as this state machine's execution role\.  
You must provide either a `Role` or `Policies`\.  
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RoleArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-rolearn)` property of an `AWS::StepFunctions::StateMachine` resource\.

 `Tags`   <a name="sam-statemachine-tags"></a>
A string\-to\-string map that specifies the tags added to the state machine and the corresponding IAM execution role\.  
*Type*: Map  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Tags](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-tags)` property of an `AWS::StepFunctions::StateMachine` resource\.

 `Tracing`   <a name="sam-statemachine-tracing"></a>
Selects whether or not AWS X\-Ray is enabled for the state machine\. For more information about using X\-Ray with Step Functions, see [AWS X\-Ray and Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-xray-tracing.html) in the AWS Step Functions Developer Guide\.  
*Type*: [TracingConfiguration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-tracingconfiguration)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[TracingConfiguration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-tracingconfiguration)` property of an `AWS::StepFunctions::StateMachine` resource\.

 `Type`   <a name="sam-statemachine-type"></a>
The type of the state machine\.  
Valid values: `STANDARD` or `EXPRESS`\.  
*Type*: String  
*Required*: No  
*Default*: `STANDARD`   
*AWS CloudFormation compatibility*: This property is passed directly to the `[StateMachineType](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-stepfunctions-statemachine.html#cfn-stepfunctions-statemachine-statemachinetype)` property of an `AWS::StepFunctions::StateMachine` resource\.

## Return Values<a name="sam-resource-statemachine-return-values"></a>

### Ref<a name="sam-resource-statemachine-return-values-ref"></a>

When you provide the logical ID of this resource to the `Ref` intrinsic function, `Ref` returns the Amazon Resource Name \(ARN\) of the underlying `AWS::StepFunctions::StateMachine` resource\.

For more information about using the `Ref` function, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html) in the *AWS CloudFormation User Guide*\. 

### Fn::GetAtt<a name="sam-resource-statemachine-return-values-fn--getatt"></a>

`Fn::GetAtt` returns a value for a specified attribute of this type\. The following are the available attributes and sample return values\. 

For more information about using `Fn::GetAtt`, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html) in the *AWS CloudFormation User Guide*\. 

`Name`  <a name="Name-fn::getatt"></a>
Returns the name of the state machine, such as `HelloWorld-StateMachine`\.

## Examples<a name="sam-resource-statemachine--examples"></a>

### State Machine Definition File<a name="sam-resource-statemachine--examples--state-machine-definition-file"></a>

The following is an example of a state machine defined with a definition file\. The `my_state_machine.asl.json` file must be written in the [Amazon States Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html)\.

In this example, the `DefinitionSubstitution` entries allow the state machine to include resources that are declared in the AWS SAM template file\.

#### YAML<a name="sam-resource-statemachine--examples--state-machine-definition-file--yaml"></a>

```
MySampleStateMachine:
  Type: AWS::Serverless::StateMachine
  Properties:
    DefinitionUri: statemachine/my_state_machine.asl.json
    Role: arn:aws:iam::123456123456:role/service-role/my-sample-role
    Tracing:
      Enabled: True
    DefinitionSubstitutions:
      MyFunctionArn: !GetAtt MyFunction.Arn
      MyDDBTable: !Ref TransactionTable
```

### Inline State Machine Definition<a name="sam-resource-statemachine--examples--inline-state-machine-definition"></a>

The following is an example of an inline state machine definition\.

In this example, the AWS SAM template file is written in YAML, so the state machine definition is also in YAML\. To declare an inline state machine definition in JSON, write your AWS SAM template file in JSON\.

#### YAML<a name="sam-resource-statemachine--examples--inline-state-machine-definition--yaml"></a>

```
MySampleStateMachine:
  Type: AWS::Serverless::StateMachine
  Properties:
    Definition:
      StartAt: MyLambdaState
      States:
        MyLambdaState:
          Type: Task
          Resource: arn:aws:lambda:us-east-1:123456123456:function:my-sample-lambda-app
          End: true
    Role: arn:aws:iam::123456123456:role/service-role/my-sample-role
    Tracing:
      Enabled: True
```