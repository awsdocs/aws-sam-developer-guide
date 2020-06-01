# ApiStateMachineAuth<a name="sam-property-statemachine-apistatemachineauth"></a>

Configures authorization at the event level\.

Configure Auth for a specific API \+ Path \+ Method

## Syntax<a name="sam-property-statemachine-apistatemachineauth-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-statemachine-apistatemachineauth-syntax.yaml"></a>

```
  [ApiKeyRequired](#sam-statemachine-apistatemachineauth-apikeyrequired): Boolean
  [AuthorizationScopes](#sam-statemachine-apistatemachineauth-authorizationscopes): List
  [Authorizer](#sam-statemachine-apistatemachineauth-authorizer): String
  [ResourcePolicy](#sam-statemachine-apistatemachineauth-resourcepolicy): [ResourcePolicyStatement](sam-property-statemachine-resourcepolicystatement.md)
```

## Properties<a name="sam-property-statemachine-apistatemachineauth-properties"></a>

 `ApiKeyRequired`   <a name="sam-statemachine-apistatemachineauth-apikeyrequired"></a>
Requires an API key for this API path and method\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `AuthorizationScopes`   <a name="sam-statemachine-apistatemachineauth-authorizationscopes"></a>
Authorization scopes to apply to this API \+ Path \+ Method\.  
Scopes listed here will override any scopes applied by the `DefaultAuthorizer` if one exists\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Authorizer`   <a name="sam-statemachine-apistatemachineauth-authorizer"></a>
The `Authorizer` for a specific state machine\.  
If you have specified a Global Authorizer for the API and want to make a specific state machine public, override by setting `Authorizer` to `NONE`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `ResourcePolicy`   <a name="sam-statemachine-apistatemachineauth-resourcepolicy"></a>
Configure Resource Policy for this path on an API\.  
*Type*: [ResourcePolicyStatement](sam-property-statemachine-resourcepolicystatement.md)  
*Required*: No  
*AWS CloudFormation Compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-statemachine-apistatemachineauth--examples"></a>

### StateMachine\-Auth<a name="sam-property-statemachine-apistatemachineauth--examples--statemachine-auth"></a>

Specifing authorization at the state machine level

#### YAML<a name="sam-property-statemachine-apistatemachineauth--examples--statemachine-auth--yaml"></a>

```
Auth:
  ApiKeyRequired: true
  Authorizer: NONE
```