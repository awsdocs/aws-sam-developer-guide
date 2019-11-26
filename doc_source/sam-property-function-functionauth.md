# FunctionAuth<a name="sam-property-function-functionauth"></a>

Configures authorization at the event level\.

Configure Auth for a specific Api \+ Path \+ Method

## Syntax<a name="sam-property-function-functionauth-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-function-functionauth-syntax.yaml"></a>

```
  [ApiKeyRequired](#sam-function-functionauth-apikeyrequired): Boolean
  [Authorizer](#sam-function-functionauth-authorizer): String
  [InvokeRole](#sam-function-functionauth-invokerole): String
  [ResourcePolicy](#sam-function-functionauth-resourcepolicy): [ResourcePolicyStatement](sam-property-function-resourcepolicystatement.md)
```

## Properties<a name="sam-property-function-functionauth-properties"></a>

 `ApiKeyRequired`   <a name="sam-function-functionauth-apikeyrequired"></a>
Requires an API key for this API path and method\.  
*Type*: Boolean  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `Authorizer`   <a name="sam-function-functionauth-authorizer"></a>
The `Authorizer` for a specific Function  
If you have specified a Global Authorizer on the API and want to make a specific Function public, override by setting `Authorizer` to `NONE`\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `InvokeRole`   <a name="sam-function-functionauth-invokerole"></a>
Specifies the `InvokeRole` to use for `AWS_IAM` authorization\.  
*Type*: String  
*Required*: No  
*Default*: CALLER\_CREDENTIALS  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.  
*Additional Notes*: `CALLER_CREDENTIALS` maps to `arn:aws:iam::*:user/*`, which uses the caller credentials to invoke the endpoint\.

 `ResourcePolicy`   <a name="sam-function-functionauth-resourcepolicy"></a>
Configure Resource Policy for this path on an API\.  
*Type*: [ResourcePolicyStatement](sam-property-function-resourcepolicystatement.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-functionauth--examples"></a>

### Function\-Auth<a name="sam-property-function-functionauth--examples--function-auth"></a>

Specifing Authorization at Function level

#### YAML<a name="sam-property-function-functionauth--examples--function-auth--yaml"></a>

```
Auth:
  ApiKeyRequired: true
  Authorizer: NONE
```