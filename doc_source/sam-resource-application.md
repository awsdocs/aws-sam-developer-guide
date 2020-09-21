# AWS::Serverless::Application<a name="sam-resource-application"></a>

Embeds a serverless application from the [AWS Serverless Application Repository](https://serverlessrepo.aws.amazon.com/applications) or from an Amazon S3 bucket as a nested application\. Nested applications are deployed as nested [AWS::CloudFormation::Stack](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cloudformation-stack.html) resources, which can contain multiple other resources including other [AWS::Serverless::Application](#sam-resource-application) resources\.

## Syntax<a name="sam-resource-application-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-resource-application-syntax.yaml"></a>

```
Type: AWS::Serverless::Application
Properties:
  [Location](#sam-application-location): String | ApplicationLocationObject
  [NotificationARNs](#sam-application-notificationarns): List
  [Parameters](#sam-application-parameters): Map
  [Tags](#sam-application-tags): Map
  [TimeoutInMinutes](#sam-application-timeoutinminutes): Integer
```

## Properties<a name="sam-resource-application-properties"></a>

 `Location`   <a name="sam-application-location"></a>
Template URL, file path, or location object of a nested application\.  
If a template URL is provided, it must follow the format specified in the [CloudFormation TemplateUrl documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-stack.html#cfn-cloudformation-stack-templateurl) and contain a valid CloudFormation or SAM template\. An [ApplicationLocationObject](sam-property-application-applicationlocationobject.md) can be used to specify an application that has been published to the [AWS Serverless Application Repository](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/what-is-serverlessrepo.html)\.  
If a local file path is provided, the template must go through the workflow that includes the `sam deploy` or `sam package` command, in order for the application to be transformed properly\.  
*Type*: String \| [ApplicationLocationObject](sam-property-application-applicationlocationobject.md)  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is similar to the `[TemplateURL](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-stack.html#cfn-cloudformation-stack-templateurl)` property of an `AWS::CloudFormation::Stack` resource\. The CloudFormation version does not take an [ApplicationLocationObject](sam-property-application-applicationlocationobject.md) to retrieve an application from the AWS Serverless Application Repository\.

 `NotificationARNs`   <a name="sam-application-notificationarns"></a>
A list of existing Amazon SNS topics where notifications about stack events are sent\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[NotificationARNs](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-stack.html#cfn-cloudformation-stack-notificationarns)` property of an `AWS::CloudFormation::Stack` resource\.

 `Parameters`   <a name="sam-application-parameters"></a>
Application parameter values\.  
*Type*: Map  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Parameters](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-stack.html#cfn-cloudformation-stack-parameters)` property of an `AWS::CloudFormation::Stack` resource\.

 `Tags`   <a name="sam-application-tags"></a>
A map \(string to string\) that specifies the tags to be added to this application\. Keys and values are limited to alphanumeric characters\. Keys can be 1 to 127 Unicode characters in length and cannot be prefixed with aws:\. Values can be 1 to 255 Unicode characters in length\.  
*Type*: Map  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[Tags](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-stack.html#cfn-cloudformation-stack-tags)` property of an `AWS::CloudFormation::Stack` resource\. The Tags property in SAM consists of Key:Value pairs; in CloudFormation it consists of a list of Tag objects\. When the stack is created, SAM will automatically add a `lambda:createdBy:SAM` tag to this application\. In addition, if this application is from the AWS Serverless Application Repository, then SAM will also automatically the two additional tags `serverlessrepo:applicationId:ApplicationId` and `serverlessrepo:semanticVersion:SemanticVersion`\.

 `TimeoutInMinutes`   <a name="sam-application-timeoutinminutes"></a>
The length of time, in minutes, that AWS CloudFormation waits for the nested stack to reach the `CREATE_COMPLETE` state\. The default is no timeout\. When AWS CloudFormation detects that the nested stack has reached the `CREATE_COMPLETE` state, it marks the nested stack resource as `CREATE_COMPLETE` in the parent stack and resumes creating the parent stack\. If the timeout period expires before the nested stack reaches `CREATE_COMPLETE`, AWS CloudFormation marks the nested stack as failed and rolls back both the nested stack and parent stack\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[TimeoutInMinutes](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-stack.html#cfn-cloudformation-stack-timeoutinminutes)` property of an `AWS::CloudFormation::Stack` resource\.

## Return Values<a name="sam-resource-application-return-values"></a>

### Ref<a name="sam-resource-application-return-values-ref"></a>

When the logical ID of this resource is provided to the `Ref` intrinsic function, it returns the resource name of the underlying `AWS::CloudFormation::Stack` resource\.

For more information about using the `Ref` function, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html) in the *AWS CloudFormation User Guide*\. 

### Fn::GetAtt<a name="sam-resource-application-return-values-fn--getatt"></a>

`Fn::GetAtt` returns a value for a specified attribute of this type\. The following are the available attributes and sample return values\. 

For more information about using `Fn::GetAtt`, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html) in the *AWS CloudFormation User Guide*\. 

`Outputs.ApplicationOutputName`  <a name="Outputs.ApplicationOutputName-fn::getatt"></a>
The value of the stack output with name `ApplicationOutputName`\.

## Examples<a name="sam-resource-application--examples"></a>

### SAR Application<a name="sam-resource-application--examples--sar-application"></a>

Application that uses a template from the Serverless Application Repository

#### YAML<a name="sam-resource-application--examples--sar-application--yaml"></a>

```
Type: AWS::Serverless::Application
Properties:
  Location:
    ApplicationId: 'arn:aws:serverlessrepo:us-east-1:012345678901:applications/my-application'
    SemanticVersion: 1.0.0
  Parameters:
    StringParameter: parameter-value
    IntegerParameter: 2
```

### Normal\-Application<a name="sam-resource-application--examples--normal-application"></a>

Application from an S3 url

#### YAML<a name="sam-resource-application--examples--normal-application--yaml"></a>

```
Type: AWS::Serverless::Application
Properties:
  Location: https://s3.amazonaws.com/demo-bucket/template.yaml
```