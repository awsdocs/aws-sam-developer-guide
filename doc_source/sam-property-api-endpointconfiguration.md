# EndpointConfiguration<a name="sam-property-api-endpointconfiguration"></a>

The endpoint type of a REST API\.

## Syntax<a name="sam-property-api-endpointconfiguration-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-endpointconfiguration-syntax.yaml"></a>

```
  [Type](#sam-api-endpointconfiguration-type): String
  [VPCEndpointIds](#sam-api-endpointconfiguration-vpcendpointids): List
```

## Properties<a name="sam-property-api-endpointconfiguration-properties"></a>

 `Type`   <a name="sam-api-endpointconfiguration-type"></a>
The endpoint type of a REST API\.  
Valid values: `EDGE` or `REGIONAL` or `PRIVATE`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Types](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigateway-restapi-endpointconfiguration.html#cfn-apigateway-restapi-endpointconfiguration-types)` property of the `AWS::ApiGateway::RestApi` `EndpointConfiguration` data type\.

 `VPCEndpointIds`   <a name="sam-api-endpointconfiguration-vpcendpointids"></a>
A list of VPC endpoint IDs of a REST API against which to create Route53 aliases\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[VpcEndpointIds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigateway-restapi-endpointconfiguration.html#cfn-apigateway-restapi-endpointconfiguration-vpcendpointids)` property of the `AWS::ApiGateway::RestApi` `EndpointConfiguration` data type\.

## Examples<a name="sam-property-api-endpointconfiguration--examples"></a>

### EndpointConfiguration<a name="sam-property-api-endpointconfiguration--examples--endpointconfiguration"></a>

Endpoint Configuration example

#### YAML<a name="sam-property-api-endpointconfiguration--examples--endpointconfiguration--yaml"></a>

```
EndpointConfiguration:
  Type: EDGE
  VPCEndpointIds:
    - vpce-123a123a
    - vpce-321a321a
```