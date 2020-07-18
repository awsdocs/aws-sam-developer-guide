# ResourcePolicyStatement<a name="sam-property-api-resourcepolicystatement"></a>

Configures resource policy for all methods and paths of an API\.

## Syntax<a name="sam-property-api-resourcepolicystatement-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-resourcepolicystatement-syntax.yaml"></a>

```
  [AwsAccountBlacklist](#sam-api-resourcepolicystatement-awsaccountblacklist): List
  [AwsAccountWhitelist](#sam-api-resourcepolicystatement-awsaccountwhitelist): List
  [CustomStatements](#sam-api-resourcepolicystatement-customstatements): List
  [IpRangeBlacklist](#sam-api-resourcepolicystatement-iprangeblacklist): List
  [IpRangeWhitelist](#sam-api-resourcepolicystatement-iprangewhitelist): List
  [SourceVpcBlacklist](#sam-api-resourcepolicystatement-sourcevpcblacklist): List
  [SourceVpcWhitelist](#sam-api-resourcepolicystatement-sourcevpcwhitelist): List
```

## Properties<a name="sam-property-api-resourcepolicystatement-properties"></a>

 `AwsAccountBlacklist`   <a name="sam-api-resourcepolicystatement-awsaccountblacklist"></a>
The AWS accounts to block\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*See Also*: See the [AWS](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies-examples.html#apigateway-resource-policies-cross-account-example) documentation for more information about this property\.

 `AwsAccountWhitelist`   <a name="sam-api-resourcepolicystatement-awsaccountwhitelist"></a>
The AWS accounts to allow\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*See Also*: See the [AWS](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies-examples.html#apigateway-resource-policies-cross-account-example) documentation for more information about this property\.

 `CustomStatements`   <a name="sam-api-resourcepolicystatement-customstatements"></a>
A list of custom resource policy statements to apply to this API\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*See Also*: See the [AWS](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies-examples.html) documentation for more information about this property\.

 `IpRangeBlacklist`   <a name="sam-api-resourcepolicystatement-iprangeblacklist"></a>
The IP addresses or address ranges to block\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*See Also*: See the [AWS](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies-examples.html#apigateway-resource-policies-source-ip-address-example) documentation for more information about this property\.

 `IpRangeWhitelist`   <a name="sam-api-resourcepolicystatement-iprangewhitelist"></a>
The IP addresses or address ranges to allow\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*See Also*: See the [AWS](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies-examples.html#apigateway-resource-policies-source-ip-address-example) documentation for more information about this property\.

 `SourceVpcBlacklist`   <a name="sam-api-resourcepolicystatement-sourcevpcblacklist"></a>
The source VPC or VPC endpoints to block\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*See Also*: See the [AWS](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies-examples.html#apigateway-resource-policies-source-vpc-example) documentation for more information about this property\.

 `SourceVpcWhitelist`   <a name="sam-api-resourcepolicystatement-sourcevpcwhitelist"></a>
The source VPC or VPC endpoints to allow\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*See Also*: See the [AWS](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies-examples.html#apigateway-resource-policies-source-vpc-example) documentation for more information about this property\.

## Examples<a name="sam-property-api-resourcepolicystatement--examples"></a>

### SourceVpcBlacklist<a name="sam-property-api-resourcepolicystatement--examples--sourcevpcblacklist"></a>

The following example blocks two IP addresses and a source VPC, and allows an AWS account\.

#### YAML<a name="sam-property-api-resourcepolicystatement--examples--sourcevpcblacklist--yaml"></a>

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
```