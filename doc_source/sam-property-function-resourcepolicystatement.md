# ResourcePolicyStatement<a name="sam-property-function-resourcepolicystatement"></a>

Configure Resource Policy for all methods and paths on an API\.

## Syntax<a name="sam-property-function-resourcepolicystatement-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-function-resourcepolicystatement-syntax.yaml"></a>

```
  [AwsAccountBlacklist](#sam-function-resourcepolicystatement-awsaccountblacklist): List
  [AwsAccountWhitelist](#sam-function-resourcepolicystatement-awsaccountwhitelist): List
  [CustomStatements](#sam-function-resourcepolicystatement-customstatements): List
  [IpRangeBlacklist](#sam-function-resourcepolicystatement-iprangeblacklist): List
  [IpRangeWhitelist](#sam-function-resourcepolicystatement-iprangewhitelist): List
  [SourceVpcBlacklist](#sam-function-resourcepolicystatement-sourcevpcblacklist): List
  [SourceVpcWhitelist](#sam-function-resourcepolicystatement-sourcevpcwhitelist): List
```

## Properties<a name="sam-property-function-resourcepolicystatement-properties"></a>

 `AwsAccountBlacklist`   <a name="sam-function-resourcepolicystatement-awsaccountblacklist"></a>
Resource Policy statements will be generated and attached to the Api for blacklisting the given list of Aws accounts  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `AwsAccountWhitelist`   <a name="sam-function-resourcepolicystatement-awsaccountwhitelist"></a>
Resource Policy statements will be generated and attached to the Api for whitelisting the given list of Aws accounts  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `CustomStatements`   <a name="sam-function-resourcepolicystatement-customstatements"></a>
A list of resource policy statements can be given for an Api  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `IpRangeBlacklist`   <a name="sam-function-resourcepolicystatement-iprangeblacklist"></a>
Resource Policy statements will be generated and attached to the Api for blacklisting the given list of Ip addresses or ranges  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `IpRangeWhitelist`   <a name="sam-function-resourcepolicystatement-iprangewhitelist"></a>
Resource Policy statements will be generated and attached to the Api for whitelisting the given list of Ip addresses or ranges  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `SourceVpcBlacklist`   <a name="sam-function-resourcepolicystatement-sourcevpcblacklist"></a>
Resource Policy statements will be generated and attached to the Api for blacklisting the given list of Source Vpcs or Vpc endpoints  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `SourceVpcWhitelist`   <a name="sam-function-resourcepolicystatement-sourcevpcwhitelist"></a>
Resource Policy statements will be generated and attached to the Api for whitelisting the given list of Source Vpcs or Vpc endpoints  
*Type*: List  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-resourcepolicystatement--examples"></a>

### SourceVpcBlacklist<a name="sam-property-function-resourcepolicystatement--examples--sourcevpcblacklist"></a>

Blacklisting source VPC or VPC endpoint

#### YAML<a name="sam-property-function-resourcepolicystatement--examples--sourcevpcblacklist--yaml"></a>

```
Auth:
  ResourcePolicy:
    AwsAccountWhitelist:
    - '123456789101'
    CustomStatements:
    - Action: execute-api:Invoke
      Condition:
        IpAddress:
          aws:SourceIp: 1.2.3.4
      Effect: Allow
      Principal: '*'
      Resource: execute-api:/Prod/PUT/get
    IpRangeBlacklist:
    - 10.20.30.40
    - 1.2.3.4
    SourceVpcBlacklist:
    - vpce-1a2b3c4d
```