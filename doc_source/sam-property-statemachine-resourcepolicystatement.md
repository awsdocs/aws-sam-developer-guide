# ResourcePolicyStatement<a name="sam-property-statemachine-resourcepolicystatement"></a>

Configures a resource policy for all methods and paths of an API\. For more information about resource policies, see [Controlling access to an API with API Gateway resource policies](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies.html) in the *API Gateway Developer Guide*\.

## Syntax<a name="sam-property-statemachine-resourcepolicystatement-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-statemachine-resourcepolicystatement-syntax.yaml"></a>

```
  [AwsAccountBlacklist](#sam-statemachine-resourcepolicystatement-awsaccountblacklist): List
  [AwsAccountWhitelist](#sam-statemachine-resourcepolicystatement-awsaccountwhitelist): List
  [CustomStatements](#sam-statemachine-resourcepolicystatement-customstatements): List
  [IntrinsicVpcBlacklist](#sam-statemachine-resourcepolicystatement-intrinsicvpcblacklist): List
  [IntrinsicVpcWhitelist](#sam-statemachine-resourcepolicystatement-intrinsicvpcwhitelist): List
  [IntrinsicVpceBlacklist](#sam-statemachine-resourcepolicystatement-intrinsicvpceblacklist): List
  [IntrinsicVpceWhitelist](#sam-statemachine-resourcepolicystatement-intrinsicvpcewhitelist): List
  [IpRangeBlacklist](#sam-statemachine-resourcepolicystatement-iprangeblacklist): List
  [IpRangeWhitelist](#sam-statemachine-resourcepolicystatement-iprangewhitelist): List
  [SourceVpcBlacklist](#sam-statemachine-resourcepolicystatement-sourcevpcblacklist): List
  [SourceVpcWhitelist](#sam-statemachine-resourcepolicystatement-sourcevpcwhitelist): List
```

## Properties<a name="sam-property-statemachine-resourcepolicystatement-properties"></a>

 `AwsAccountBlacklist`   <a name="sam-statemachine-resourcepolicystatement-awsaccountblacklist"></a>
The AWS accounts to block\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AwsAccountWhitelist`   <a name="sam-statemachine-resourcepolicystatement-awsaccountwhitelist"></a>
The AWS accounts to allow\. For an example use of this property, see the Examples section at the bottom of this page\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `CustomStatements`   <a name="sam-statemachine-resourcepolicystatement-customstatements"></a>
A list of custom resource policy statements to apply to this API\. For an example use of this property, see the Examples section at the bottom of this page\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `IntrinsicVpcBlacklist`   <a name="sam-statemachine-resourcepolicystatement-intrinsicvpcblacklist"></a>
The list of virtual private clouds \(VPCs\) to block, where each VPC is specified as a reference such as a [dynamic reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/dynamic-references.html) or the `Ref` [intrinsic function](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)\. For an example use of this property, see the Examples section at the bottom of this page\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `IntrinsicVpcWhitelist`   <a name="sam-statemachine-resourcepolicystatement-intrinsicvpcwhitelist"></a>
The list of VPCs to allow, where each VPC is specified as a reference such as a [dynamic reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/dynamic-references.html) or the `Ref` [intrinsic function](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `IntrinsicVpceBlacklist`   <a name="sam-statemachine-resourcepolicystatement-intrinsicvpceblacklist"></a>
The list of VPC endpoints to block, where each VPC endpoint is specified as a reference such as a [dynamic reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/dynamic-references.html) or the `Ref` [intrinsic function](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `IntrinsicVpceWhitelist`   <a name="sam-statemachine-resourcepolicystatement-intrinsicvpcewhitelist"></a>
The list of VPC endpoints to allow, where each VPC endpoint is specified as a reference such as a [dynamic reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/dynamic-references.html) or the `Ref` [intrinsic function](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)\. For an example use of this property, see the Examples section at the bottom of this page\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `IpRangeBlacklist`   <a name="sam-statemachine-resourcepolicystatement-iprangeblacklist"></a>
The IP addresses or address ranges to block\. For an example use of this property, see the Examples section at the bottom of this page\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `IpRangeWhitelist`   <a name="sam-statemachine-resourcepolicystatement-iprangewhitelist"></a>
The IP addresses or address ranges to allow\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `SourceVpcBlacklist`   <a name="sam-statemachine-resourcepolicystatement-sourcevpcblacklist"></a>
The source VPC or VPC endpoints to block\. Source VPC names must start with `"vpc-"` and source VPC endpoint names must start with `"vpce-"`\. For an example use of this property, see the Examples section at the bottom of this page\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `SourceVpcWhitelist`   <a name="sam-statemachine-resourcepolicystatement-sourcevpcwhitelist"></a>
The source VPC or VPC endpoints to allow\. Source VPC names must start with `"vpc-"` and source VPC endpoint names must start with `"vpce-"`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-statemachine-resourcepolicystatement--examples"></a>

### Resource Policy Example<a name="sam-property-statemachine-resourcepolicystatement--examples--resource-policy-example"></a>

The following example blocks two IP addresses and a source VPC, and allows an AWS account\.

#### YAML<a name="sam-property-statemachine-resourcepolicystatement--examples--resource-policy-example--yaml"></a>

```
Auth:
  ResourcePolicy:
    CustomStatements: [{
                         "Effect": "Allow",
                         "Principal": "*",
                         "Action": "execute-api:Invoke",
                         "Resource": "execute-api:/Prod/GET/pets",
                         "Condition": {
                           "IpAddress": {
                             "aws:SourceIp": "1.2.3.4"
                           }
                         }
                       }]
    IpRangeBlacklist:
      - "10.20.30.40"
      - "1.2.3.4"
    SourceVpcBlacklist:
      - "vpce-1a2b3c4d"
    AwsAccountWhitelist:
      - "111122223333"
    IntrinsicVpcBlacklist:
      - "{{resolve:ssm:SomeVPCReference:1}}" 
      - !Ref MyVPC
    IntrinsicVpceWhitelist:
      - "{{resolve:ssm:SomeVPCEReference:1}}" 
      - !Ref MyVPCE
```