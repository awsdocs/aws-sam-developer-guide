# ApiFunctionAuth<a name="sam-property-function-apifunctionauth"></a>

Configures authorization at the event level, for a specific API, path, and method\.

## Syntax<a name="sam-property-function-apifunctionauth-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-apifunctionauth-syntax.yaml"></a>

```
  [ApiKeyRequired](#sam-function-apifunctionauth-apikeyrequired): Boolean
  [AuthorizationScopes](#sam-function-apifunctionauth-authorizationscopes): List
  [Authorizer](#sam-function-apifunctionauth-authorizer): String
  [InvokeRole](#sam-function-apifunctionauth-invokerole): String
  [ResourcePolicy](#sam-function-apifunctionauth-resourcepolicy): ResourcePolicyStatement
```

## Properties<a name="sam-property-function-apifunctionauth-properties"></a>

 `ApiKeyRequired`   <a name="sam-function-apifunctionauth-apikeyrequired"></a>
Requires an API key for this API, path, and method\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AuthorizationScopes`   <a name="sam-function-apifunctionauth-authorizationscopes"></a>
The authorization scopes to apply to this API, path, and method\.  
The scopes that you specify will override any scopes applied by the `DefaultAuthorizer` property if you have specified it\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Authorizer`   <a name="sam-function-apifunctionauth-authorizer"></a>
The `Authorizer` for a specific Function  
If you have specified a Global Authorizer on the API and want to make a specific Function public, override by setting `Authorizer` to `NONE`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `InvokeRole`   <a name="sam-function-apifunctionauth-invokerole"></a>
Specifies the `InvokeRole` to use for `AWS_IAM` authorization\.  
*Type*: String  
*Required*: No  
*Default*: `CALLER_CREDENTIALS`   
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.  
*Additional Notes*: `CALLER_CREDENTIALS` maps to `arn:aws:iam::*:user/*`, which uses the caller credentials to invoke the endpoint\.

 `ResourcePolicy`   <a name="sam-function-apifunctionauth-resourcepolicy"></a>
Configure Resource Policy for this path on an API\.  
*Type*: [ResourcePolicyStatement](sam-property-function-resourcepolicystatement.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-apifunctionauth--examples"></a>

### Function\-Auth<a name="sam-property-function-apifunctionauth--examples--function-auth"></a>

The following example specifies authorization at the function level\.

#### YAML<a name="sam-property-function-apifunctionauth--examples--function-auth--yaml"></a>

```
Auth:
  ApiKeyRequired: true
  Authorizer: NONE
```