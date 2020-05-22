# Resource Attributes<a name="sam-specification-resource-attributes"></a>

Resource attributes are attributes that you can add to a resource to control additional behaviors and relationships\. For more information about resource attributes, see [Resource Attribute Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-product-attribute-reference.html) in the *AWS CloudFormation User Guide*\.

AWS SAM resources support a subset of resource attributes that are supported by AWS CloudFormation resources\. To see which AWS SAM resources support which resource attributes, see the following table\.


|  |  |  |  |  |  |  | 
| --- |--- |--- |--- |--- |--- |--- |
|  Resource Type  |  [CreationPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-creationpolicy.html)  |  [DeletionPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-deletionpolicy.html)  |  [DependsOn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-dependson.html)  |  [Metadata](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-metadata.html)  |  [UpdatePolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-updatepolicy.html)  |  [UpdateReplacePolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-updatereplacepolicy.html)  | 
|  [AWS::Serverless::Api](sam-resource-api.md)  | No | No | Yes | No | No | No | 
|  [AWS::Serverless::Application](sam-resource-application.md)  | No | No | Yes | No | No | No | 
|  [AWS::Serverless::Function](sam-resource-function.md)  | No | No | Yes | [Yes](building-custom-runtimes.md) | No | No | 
|  [AWS::Serverless::HttpApi](sam-resource-httpapi.md)  | No | No | Yes | No | No | No | 
|  [AWS::Serverless::LayerVersion](sam-resource-layerversion.md)  | No | Yes | Yes | [Yes](building-layers.md) | No | No | 
|  [AWS::Serverless::SimpleTable](sam-resource-simpletable.md)  | No | No | Yes | No | No | No | 