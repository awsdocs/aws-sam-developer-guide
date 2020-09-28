# HttpApiDomainConfiguration<a name="sam-property-httpapi-httpapidomainconfiguration"></a>

Configures a custom domain for an API\.

## Syntax<a name="sam-property-httpapi-httpapidomainconfiguration-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-httpapi-httpapidomainconfiguration-syntax.yaml"></a>

```
  [BasePath](#sam-httpapi-httpapidomainconfiguration-basepath): List
  [CertificateArn](#sam-httpapi-httpapidomainconfiguration-certificatearn): String
  [DomainName](#sam-httpapi-httpapidomainconfiguration-domainname): String
  [EndpointConfiguration](#sam-httpapi-httpapidomainconfiguration-endpointconfiguration): String
  [Route53](#sam-httpapi-httpapidomainconfiguration-route53): Route53Configuration
```

## Properties<a name="sam-property-httpapi-httpapidomainconfiguration-properties"></a>

 `BasePath`   <a name="sam-httpapi-httpapidomainconfiguration-basepath"></a>
List of basepaths to be configured with the API Gateway Domain Name\.  
*Type*: List  
*Required*: No  
*Default*: /  
*AWS CloudFormation compatibility*: This property is similar to the `[BasePath](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-apimapping.html)` property of an `AWS::ApiGatewayV2::ApiMapping` resource\. SAM will create multiple `AWS::ApiGatewayV2::ApiMapping` resources, one per `BasePath` specified in this property\.  
*Additional Notes*: SAM will create multiple `AWS::ApiGatewayV2::ApiMapping` resources, one per `BasePath` specified in this property\.

 `CertificateArn`   <a name="sam-httpapi-httpapidomainconfiguration-certificatearn"></a>
The reference to an AWS\-managed certificate for use by the endpoint for this domain name\. AWS Certificate Manager is the only supported source\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[CertificateArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigatewayv2-domainname-domainnameconfiguration.html#cfn-apigatewayv2-domainname-domainnameconfiguration-certificatearn)` property of an `AWS::ApiGateway2::DomainName DomainNameConfiguration` resource\.

 `DomainName`   <a name="sam-httpapi-httpapidomainconfiguration-domainname"></a>
The custom domain name for your API Gateway API\. Uppercase letters are not supported\.  
AWS SAM generates an `AWS::ApiGatewayV2::DomainName` resource when this property is set\. For information about this scenario, see [DomainName property is specified](sam-specification-generated-resources-httpapi.md#sam-specification-generated-resources-httpapi-domain-name)\. For general information about generated AWS CloudFormation resources, see [Generated AWS CloudFormation resources](sam-specification-generated-resources.md)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[DomainName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-domainname.html#cfn-apigatewayv2-domainname-domainname)` property of an `AWS::ApiGateway2::DomainName` resource\.

 `EndpointConfiguration`   <a name="sam-httpapi-httpapidomainconfiguration-endpointconfiguration"></a>
Property to define the type of API Gateway endpoint to be mapped to the custom domain\. The value of this property controls how the `CertificateArn` property gets mapped in AWS CloudFormation\. See `CertificateArn` above\.  
Valid value for HttpApis is only `REGIONAL`\.  
*Type*: String  
*Required*: No  
*Default*: `REGIONAL`   
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Route53`   <a name="sam-httpapi-httpapidomainconfiguration-route53"></a>
Property that adds Route53 configuration based on the values defined\.  
*Type*: [Route53Configuration](sam-property-httpapi-route53configuration.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-httpapi-httpapidomainconfiguration--examples"></a>

### DomainName<a name="sam-property-httpapi-httpapidomainconfiguration--examples--domainname"></a>

DomainName example

#### YAML<a name="sam-property-httpapi-httpapidomainconfiguration--examples--domainname--yaml"></a>

```
Domain:
  DomainName: www.example.com
  CertificateArn: arn-example
  EndpointConfiguration: REGIONAL
  Route53:
    HostedZoneId: Z1PA6795UKMFR9
  BasePath:
    - /foo
    - /bar
```