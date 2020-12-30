# Resource attributes<a name="sam-specification-resource-attributes"></a>

Resource attributes are attributes that you can add to a resource to control additional behaviors and relationships\. For more information about resource attributes, see [Resource Attribute Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-product-attribute-reference.html) in the *AWS CloudFormation User Guide*\.

AWS SAM resources support a subset of resource attributes that are supported by AWS CloudFormation resources\. To see which AWS SAM resources support which resource attributes, see the following table\.


|  |  |  |  |  |  |  | 
| --- |--- |--- |--- |--- |--- |--- |
|  Resource Type  |  [CreationPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-creationpolicy.html)  |  [DeletionPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-deletionpolicy.html)  |  [DependsOn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-dependson.html)  |  [Metadata](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-metadata.html)  |  [UpdatePolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-updatepolicy.html)  |  [UpdateReplacePolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-updatereplacepolicy.html)  | 
|  [AWS::Serverless::Api](sam-resource-api.md)  |  |  | ✓ |  |  |  | 
|  [AWS::Serverless::Application](sam-resource-application.md)  |  |  | ✓ |  |  |  | 
|  [AWS::Serverless::Function](sam-resource-function.md)  |  |  | ✓ | [✓](building-custom-runtimes.md)\* |  |  | 
|  [AWS::Serverless::HttpApi](sam-resource-httpapi.md)  |  |  | ✓ |  |  |  | 
|  [AWS::Serverless::LayerVersion](sam-resource-layerversion.md)  |  | ✓ | ✓ | [✓](building-layers.md)\*\* |  |  | 
|  [AWS::Serverless::SimpleTable](sam-resource-simpletable.md)  |  |  | ✓ |  |  |  | 
|  [AWS::Serverless::StateMachine](sam-resource-statemachine.md)  |  |  | ✓ |  |  |  | 

**Notes:**

\* For more information about using the `Metadata` resource attribute with the `AWS::Serverless::Function` resource type, see [Building custom runtimes](building-custom-runtimes.md)\.

\*\* For more information about using the `Metadata` resource attribute with the `AWS::Serverless::LayerVersion` resource type, see [Building layers](building-layers.md)\.