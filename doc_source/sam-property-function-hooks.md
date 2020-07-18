# Hooks<a name="sam-property-function-hooks"></a>

Validation Lambda functions that are run before and after traffic shifting\.

**Note**: The Lambda functions referenced in this property configure the `CodeDeployLambdaAliasUpdate` object of the resulting [AWS::Lambda::Alias](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html) resource\. For more information, see [CodeDeployLambdaAliasUpdate Policy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-updatepolicy.html#cfn-attributes-updatepolicy-codedeploylambdaaliasupdate) in the AWS CloudFormation User Guide\.

## Syntax<a name="sam-property-function-hooks-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-hooks-syntax.yaml"></a>

```
  [PostTraffic](#sam-function-hooks-posttraffic): String
  [PreTraffic](#sam-function-hooks-pretraffic): String
```

## Properties<a name="sam-property-function-hooks-properties"></a>

 `PostTraffic`   <a name="sam-function-hooks-posttraffic"></a>
Lambda function that is run after traffic shifting\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `PreTraffic`   <a name="sam-function-hooks-pretraffic"></a>
Lambda function that is run before traffic shifting\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-hooks--examples"></a>

### Hooks<a name="sam-property-function-hooks--examples--hooks"></a>

Example hook functions

#### YAML<a name="sam-property-function-hooks--examples--hooks--yaml"></a>

```
Hooks:
  PreTraffic:
    Ref: PreTrafficLambdaFunction
  PostTraffic:
    Ref: PostTrafficLambdaFunction
```