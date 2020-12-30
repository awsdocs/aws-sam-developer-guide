# ApiStateMachineAuth<a name="sam-property-statemachine-apistatemachineauth"></a>

Configures authorization at the event level, for a specific API, path, and method\.

## Syntax<a name="sam-property-statemachine-apistatemachineauth-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-statemachine-apistatemachineauth-syntax.yaml"></a>

```
  [ApiKeyRequired](#sam-statemachine-apistatemachineauth-apikeyrequired): Boolean
  [AuthorizationScopes](#sam-statemachine-apistatemachineauth-authorizationscopes): List
  [Authorizer](#sam-statemachine-apistatemachineauth-authorizer): String
  [ResourcePolicy](#sam-statemachine-apistatemachineauth-resourcepolicy): ResourcePolicyStatement
```

## Properties<a name="sam-property-statemachine-apistatemachineauth-properties"></a>

 `ApiKeyRequired`   <a name="sam-statemachine-apistatemachineauth-apikeyrequired"></a>
Requires an API key for this API, path, and method\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AuthorizationScopes`   <a name="sam-statemachine-apistatemachineauth-authorizationscopes"></a>
The authorization scopes to apply to this API, path, and method\.  
The scopes that you specify will override any scopes applied by the `DefaultAuthorizer` property if you have specified it\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Authorizer`   <a name="sam-statemachine-apistatemachineauth-authorizer"></a>
The `Authorizer` for a specific state machine\.  
If you have specified a global authorizer for the API and want to make this state machine public, override the global authorizer by setting `Authorizer` to `NONE`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ResourcePolicy`   <a name="sam-statemachine-apistatemachineauth-resourcepolicy"></a>
Configure the resource policy for this API and path\.  
*Type*: [ResourcePolicyStatement](sam-property-statemachine-resourcepolicystatement.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-statemachine-apistatemachineauth--examples"></a>

### StateMachine\-Auth<a name="sam-property-statemachine-apistatemachineauth--examples--statemachine-auth"></a>

The following example specifies authorization at the state machine level\.

#### YAML<a name="sam-property-statemachine-apistatemachineauth--examples--statemachine-auth--yaml"></a>

```
Auth:
  ApiKeyRequired: true
  Authorizer: NONE
```