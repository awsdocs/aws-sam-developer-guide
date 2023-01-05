# AWS SAM template anatomy<a name="sam-specification-template-anatomy"></a>

An AWS SAM template file closely follows the format of an AWS CloudFormation template file, which is described in [Template anatomy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html) in the *AWS CloudFormation User Guide*\. The primary differences between AWS SAM template files and AWS CloudFormation template files are the following:
+ **Transform declaration\.** The declaration `Transform: AWS::Serverless-2016-10-31` is required for AWS SAM template files\. This declaration identifies an AWS CloudFormation template file as an AWS SAM template file\. For more information about transforms, see [Transform](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/transform-section-structure.html) in the *AWS CloudFormation User Guide*\.
+ **Globals section\.** The `Globals` section is unique to AWS SAM\. It defines properties that are common to all your serverless functions and APIs\. All the `AWS::Serverless::Function`, `AWS::Serverless::Api`, and `AWS::Serverless::SimpleTable` resources inherit the properties that are defined in the `Globals` section\. For more information about this section, see [Globals section of the AWS SAM template](sam-specification-template-anatomy-globals.md)\.
+ **Resources section\.** In AWS SAM templates the `Resources` section can contain a combination of AWS CloudFormation resources and AWS SAM resources\. For more information about AWS CloudFormation resources, see [AWS resource and property types reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html) in the *AWS CloudFormation User Guide*\. For more information about AWS SAM resources, see [AWS SAM resource and property reference](sam-specification-resources-and-properties.md)\.
+ **Parameters section\.** Objects that are declared in the `Parameters` section cause the `sam deploy --guided` command to present additional prompts to the user\. For examples of declared objects and the corresponding prompts, see [sam deploy](sam-cli-command-reference-sam-deploy.md) in the AWS SAM CLI command reference\.

All other sections of an AWS SAM template file correspond to the AWS CloudFormation template file section of the same name\.

## YAML<a name="template-anatomy-outline.yaml"></a>

The following example shows a YAML\-formatted template fragment\.

```
Transform: AWS::Serverless-2016-10-31

Globals:
  set of globals

Description:
  String

Metadata:
  template metadata

Parameters:
  set of parameters

Mappings:
  set of mappings

Conditions:
  set of conditions

Resources:
  set of resources

Outputs:
  set of outputs
```

## Template sections<a name="template-anatomy-sections"></a>

AWS SAM templates can include several major sections\. Only the `Transform` and `Resources` sections are required\.

You can include template sections in any order\. However, as you build your template, it can be helpful to use the logical order that's shown in the following list\. This is because the values in one section might refer to values from a previous section\.

**[Transform \(required\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/transform-section-structure.html)**  
For AWS SAM templates, you must include this section with a value of `AWS::Serverless-2016-10-31`\.  
Additional transforms are optional\. For more information about transforms, see [Transform](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/transform-section-structure.html) in the *AWS CloudFormation User Guide*\.

**[Globals \(optional\)](sam-specification-template-anatomy-globals.md)**  
Properties that are common to all your serverless functions, APIs, and simple tables\. All the `AWS::Serverless::Function`, `AWS::Serverless::Api`, and `AWS::Serverless::SimpleTable` resources inherit the properties that are defined in the `Globals` section\.  
This section is unique to AWS SAM\. There isn't a corresponding section in AWS CloudFormation templates\.

**[Description \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-description-structure.html)**  
A text string that describes the template\.  
This section corresponds directly with the `Description` section of AWS CloudFormation templates\.

**[Metadata \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/metadata-section-structure.html)**  
Objects that provide additional information about the template\.  
This section corresponds directly with the `Metadata` section of AWS CloudFormation templates\.

**[Parameters \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html)**  
Values to pass to your template at runtime \(when you create or update a stack\)\. You can refer to parameters from the `Resources` and `Outputs` sections of the template\.  
Values that are passed in using the `--parameter-overrides` parameter of the `sam deploy` command—and entries in the configuration file—take precendence over entries in the AWS SAM template file\. For more information about the `sam deploy` command, see [sam deploy](sam-cli-command-reference-sam-deploy.md) in the AWS SAM CLI command reference\. For more information about the configuration file, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\.

**[Mappings \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/mappings-section-structure.html)**  
A mapping of keys and associated values that you can use to specify conditional parameter values, similar to a lookup table\. You can match a key to a corresponding value by using the [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-findinmap.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-findinmap.html) intrinsic function in the `Resources` and `Outputs` sections\.  
This section corresponds directly with the `Mappings` section of AWS CloudFormation templates\.

**[Conditions \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/conditions-section-structure.html)**  
Conditions that control whether certain resources are created or whether certain resource properties are assigned a value during stack creation or update\. For example, you could conditionally create a resource that depends on whether the stack is for a production or test environment\.  
This section corresponds directly with the `Conditions` section of AWS CloudFormation templates\.

**[Resources \(required\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resources-section-structure.html)**  
The stack resources and their properties, such as an Amazon Elastic Compute Cloud \(Amazon EC2\) instance or an Amazon Simple Storage Service \(Amazon S3\) bucket\. You can refer to resources in the `Resources` and `Outputs` sections of the template\.  
This section is similar to the `Resources` section of AWS CloudFormation templates\. In AWS SAM templates, this section can contain AWS SAM resources in addition to AWS CloudFormation resources\.

**[Outputs \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/outputs-section-structure.html)**  
The values that are returned whenever you view your stack's properties\. For example, you can declare an output for an S3 bucket name, and then call the `aws cloudformation describe-stacks` AWS Command Line Interface \(AWS CLI\) command to view the name\.  
This section corresponds directly with the `Outputs` section of AWS CloudFormation templates\.

## Next steps<a name="template-anatomy-next-steps"></a>

To download and deploy a sample serverless application that contains an AWS SAM template file, see [Getting started with AWS SAM](serverless-getting-started.md) and follow the instructions in [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md)\.