# AWS SAM Template Anatomy<a name="sam-specification-template-anatomy"></a>

The format of an AWS SAM template file closely follows the format of an AWS CloudFormation template file, which is described in [Template Anatomy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html) in the *AWS CloudFormation User Guide*\.

The primary differences between AWS SAM template files and AWS CloudFormation template files are the following:
+ **Transform declaration\.** The declaration `Transform: AWS::Serverless-2016-10-31` is required for AWS SAM template files\. This declaration identifies an AWS CloudFormation template file as an AWS SAM template file\. For more information about transforms, see [Transform](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/transform-section-structure.html) in the *AWS CloudFormation User Guide*\.
+ **Globals section\. ** The Globals section is unique to AWS SAM\. It defines properties that are common to all your serverless functions and APIs\. All the `AWS::Serverless::Function`, `AWS::Serverless::Api`, and `AWS::Serverless::SimpleTable` resources inherit the properties that are defined in the Globals section\. For more information about the Globals section, see [Globals Section of the Template](sam-specification-template-anatomy-globals.md) in the *AWS Serverless Application Model Developer Guide*\.
+ **Resources section\. ** In AWS SAM templates the Resources section can contain a combination of AWS CloudFormation resources and AWS SAM resources\. For more information about AWS CloudFormation resources, see [AWS Resource and Property Types Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html) in the *AWS CloudFormation User Guide*\. For more information about AWS SAM resources see [AWS SAM Resource and Property Reference](sam-specification-resources-and-properties.md) in the *AWS Serverless Application Model Developer Guide*\.

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

## Template Sections<a name="template-anatomy-sections"></a>

Templates include several major sections\. `Transform` and `Resources` are the only required sections\.

The sections in a template can be in any order\. However, as you build your template, it can be helpful to use the logical order that's shown in the following list\. This is because the values in one section might refer to values from a previous section\. 

**[Transform \(required\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/transform-section-structure.html)**  
For AWS SAM templates, you must include this section with a value of `AWS::Serverless-2016-10-31`\.  
Additional transforms are optional\. For more information about transforms, see [Transform](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/transform-section-structure.html) in the *AWS CloudFormation User Guide*\.

**[Globals \(optional\)](sam-specification-template-anatomy-globals.md)**  
A section in your AWS SAM template to define properties that are common to all your serverless functions, APIs, and simple tables\. All the `AWS::Serverless::Function`, `AWS::Serverless::Api`, and `AWS::Serverless::SimpleTable` resources inherit the properties that are defined in the Globals section\.  
This section is unique to AWS SAM\. There isn't a corresponding section in AWS CloudFormation templates\.

**[Description \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-description-structure.html)**  
A text string that describes the template\.  
This section corresponds directly with the Description section of AWS CloudFormation templates\.

**[Metadata \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/metadata-section-structure.html)**  
Objects that provide additional information about the template\.  
This section corresponds directly with the Metadata section of AWS CloudFormation templates\.

**[Parameters \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html)**  
Values to pass to your template at runtime \(when you create or update a stack\)\. You can refer to parameters from the `Resources` and `Outputs` sections of the template\.  
This section corresponds directly with the Parameters section of AWS CloudFormation templates\.

**[Mappings \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/mappings-section-structure.html)**  
A mapping of keys and associated values that you can use to specify conditional parameter values, similar to a lookup table\. You can match a key to a corresponding value by using the [Fn::FindInMap](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-findinmap.html) intrinsic function in the `Resources` and `Outputs` sections\.  
This section corresponds directly with the Mappings section of AWS CloudFormation templates\.

**[Conditions \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/conditions-section-structure.html)**  
Conditions that control whether certain resources are created or whether certain resource properties are assigned a value during stack creation or update\. For example, you could conditionally create a resource that depends on whether the stack is for a production or test environment\.  
This section corresponds directly with the Conditions section of AWS CloudFormation templates\.

**[Resources \(required\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resources-section-structure.html)**  
Specifies the stack resources and their properties, such as an Amazon EC2 instance or an Amazon S3 bucket\. You can refer to resources in the `Resources` and `Outputs` sections of the template\.  
This section is similar to the Resources section of AWS CloudFormation templates\. In AWS SAM templates, this section can contain AWS SAM resources in addition to AWS CloudFormation resources\.

**[Outputs \(optional\)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/outputs-section-structure.html)**  
Describes the values that are returned whenever you view your stack's properties\. For example, you can declare an output for an S3 bucket name, and then call the `aws cloudformation describe-stacks` AWS CLI command to view the name\.  
This section corresponds directly with the Outputs section of AWS CloudFormation templates\.

## Next Steps<a name="template-anatomy-next-steps"></a>

To download and deploy a sample serverless application that contains an AWS SAM template file, see [Getting Started with AWS SAM](serverless-getting-started.md) and execute the [Tutorial: Deploying a Hello World Application](serverless-getting-started-hello-world.md)\.