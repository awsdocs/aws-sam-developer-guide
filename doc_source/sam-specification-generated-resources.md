# Generated AWS CloudFormation resources<a name="sam-specification-generated-resources"></a>

When AWS Serverless Application Model \(AWS SAM\) processes your AWS SAM template file, it generates AWS CloudFormation resources\. The set of AWS CloudFormation resources that AWS SAM generates differs depending on the scenarios that you specify\. A *scenario* is the combination of AWS SAM resources and properties specified in your template file\. You can reference the generated AWS CloudFormation resources elsewhere within your template file, similar to how you reference resources that you declare explicitly in your template file\.

For example, if you specify an `AWS::Serverless::Function` resource in your AWS SAM template file, AWS SAM always generates an `AWS::Lambda::Function` base resource\. If you also specify the optional `AutoPublishAlias` property, AWS SAM additionally generates `AWS::Lambda::Alias` and `AWS::Lambda::Version` resources\.

This section lists the scenarios and the AWS CloudFormation resources that they generate, and shows how to reference the generated AWS CloudFormation resources in your AWS SAM template file\.

**Topics**
+ [Referencing generated AWS CloudFormation resources](#sam-specification-generated-resources-referencing)
+ [Generated AWS CloudFormation resource reference](#sam-specification-generated-resources-scenarios)
+ [AWS CloudFormation resources generated when AWS::Serverless::Api is specified](sam-specification-generated-resources-api.md)
+ [AWS CloudFormation resources generated when AWS::Serverless::Function is specified](sam-specification-generated-resources-function.md)
+ [AWS CloudFormation resources generated when AWS::Serverless::HttpApi is specified](sam-specification-generated-resources-httpapi.md)

## Referencing generated AWS CloudFormation resources<a name="sam-specification-generated-resources-referencing"></a>

You have two options for referencing generated AWS CloudFormation resources within your AWS SAM template file, by `LogicalId` or by referenceable property\.

### Referencing generated AWS CloudFormation resources by LogicalId<a name="sam-specification-generated-resources-referencing-logicalid"></a>

The AWS CloudFormation resources that AWS SAM generates each have a `[LogicalId](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resources-section-structure.html#resources-section-structure-logicalid)`, which is an alphanumeric \(A\-Z, a\-z, 0\-9\) identifier that is unique within a template file\. AWS SAM uses the `LogicalIds` of the AWS SAM resources in your template file to construct the `LogicalIds` of the AWS CloudFormation resources it generates\. You can use the `LogicalId` of a generated AWS CloudFormation resource to access properties of that resource within your template file, just like you would for an AWS CloudFormation resource that you have explicitly declared\. For more information about `LogicalIds` in AWS CloudFormation and AWS SAM templates, see [Resources](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resources-section-structure.html) in the *AWS CloudFormation User Guide*\.

**Note**  
The `LogicalIds` of some generated resources include a unique hash value to avoid namespace clashes\. The `LogicalIds` of these resources are derived when the stack is created\. You can retrieve them only after the stack has been created using the AWS Management Console, AWS CLI, or one of the AWS SDKs\. We don't recommend referencing these resources by `LogicalId` because the hash values might change\.

### Referencing generated AWS CloudFormation resources by referenceable property<a name="sam-specification-generated-resources-referencing-referenceable-property"></a>

For some generated resources, AWS SAM provides a referenceable property of the AWS SAM resource\. You can use this property to reference a generated AWS CloudFormation resource and its properties within your AWS SAM template file\.

**Note**  
Not all generated AWS CloudFormation resources have referenceable properties\. For those resources, you must use the `LogicalId`\.

## Generated AWS CloudFormation resource reference<a name="sam-specification-generated-resources-scenarios"></a>

The following table summarizes the AWS SAM resources and properties that make up the scenarios that generate AWS CloudFormation resources\.

The topics in the **AWS SAM Resources** column provide details about the base resources that are generated when you specify the AWS SAM resource\. The topics in the **Scenarios** column provide details about the additional resources generated for that scenario\.


|  |  | 
| --- |--- |
|  AWS SAM Resources  |  Scenarios  | 
| [AWS::Serverless::Api](sam-specification-generated-resources-api.md) |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-specification-generated-resources.html)  | 
| [AWS::Serverless::Function](sam-specification-generated-resources-function.md) |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-specification-generated-resources.html)  | 
| [AWS::Serverless::HttpApi](sam-specification-generated-resources-httpapi.md) |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-specification-generated-resources.html)  | 

**Topics**
+ [Referencing generated AWS CloudFormation resources](#sam-specification-generated-resources-referencing)
+ [Generated AWS CloudFormation resource reference](#sam-specification-generated-resources-scenarios)
+ [AWS CloudFormation resources generated when AWS::Serverless::Api is specified](sam-specification-generated-resources-api.md)
+ [AWS CloudFormation resources generated when AWS::Serverless::Function is specified](sam-specification-generated-resources-function.md)
+ [AWS CloudFormation resources generated when AWS::Serverless::HttpApi is specified](sam-specification-generated-resources-httpapi.md)