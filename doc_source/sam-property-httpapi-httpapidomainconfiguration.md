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
  [MutualTlsAuthentication](#sam-httpapi-httpapidomainconfiguration-mutualtlsauthentication): [MutualTlsAuthentication](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-domainname.html#cfn-apigatewayv2-domainname-mutualtlsauthentication)
  [OwnershipVerificationCertificateArn](#sam-httpapi-httpapidomainconfiguration-ownershipverificationcertificatearn): String
  [Route53](#sam-httpapi-httpapidomainconfiguration-route53): Route53Configuration
  [SecurityPolicy](#sam-httpapi-httpapidomainconfiguration-securitypolicy): String
```

## Properties<a name="sam-property-httpapi-httpapidomainconfiguration-properties"></a>

 `BasePath`   <a name="sam-httpapi-httpapidomainconfiguration-basepath"></a>
A list of the basepaths to configure with the Amazon API Gateway domain name\.  
*Type*: List  
*Required*: No  
*Default*: /  
*AWS CloudFormation compatibility*: This property is similar to the `[ApiMappingKey](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-apimapping.html#cfn-apigatewayv2-apimapping-apimappingkey)` property of an `AWS::ApiGatewayV2::ApiMapping` resource\. AWS SAM creates multiple `AWS::ApiGatewayV2::ApiMapping` resources, one per value specified in this property\.

 `CertificateArn`   <a name="sam-httpapi-httpapidomainconfiguration-certificatearn"></a>
The Amazon Resource Name \(ARN\) of an AWS managed certificate for this domain name's endpoint\. AWS Certificate Manager is the only supported source\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[CertificateArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigatewayv2-domainname-domainnameconfiguration.html#cfn-apigatewayv2-domainname-domainnameconfiguration-certificatearn)` property of an `AWS::ApiGateway2::DomainName DomainNameConfiguration` resource\.

 `DomainName`   <a name="sam-httpapi-httpapidomainconfiguration-domainname"></a>
The custom domain name for your API Gateway API\. Uppercase letters are not supported\.  
AWS SAM generates an `AWS::ApiGatewayV2::DomainName` resource when this property is set\. For information about this scenario, see [DomainName property is specified](sam-specification-generated-resources-httpapi.md#sam-specification-generated-resources-httpapi-domain-name)\. For information about generated AWS CloudFormation resources, see [Generated AWS CloudFormation resources](sam-specification-generated-resources.md)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[DomainName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-domainname.html#cfn-apigatewayv2-domainname-domainname)` property of an `AWS::ApiGateway2::DomainName` resource\.

 `EndpointConfiguration`   <a name="sam-httpapi-httpapidomainconfiguration-endpointconfiguration"></a>
Defines the type of API Gateway endpoint to map to the custom domain\. The value of this property determines how the `CertificateArn` property is mapped in AWS CloudFormation\.  
The only valid value for HTTP APIs is `REGIONAL`\.  
*Type*: String  
*Required*: No  
*Default*: `REGIONAL`  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `MutualTlsAuthentication`   <a name="sam-httpapi-httpapidomainconfiguration-mutualtlsauthentication"></a>
The mutual transport layer security \(TLS\) authentication configuration for a custom domain name\.  
*Type*: [MutualTlsAuthentication](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-domainname.html#cfn-apigatewayv2-domainname-mutualtlsauthentication)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MutualTlsAuthentication](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-domainname.html#cfn-apigatewayv2-domainname-mutualtlsauthentication)` property of an `AWS::ApiGatewayV2::DomainName` resource\.

 `OwnershipVerificationCertificateArn`   <a name="sam-httpapi-httpapidomainconfiguration-ownershipverificationcertificatearn"></a>
The ARN of the public certificate issued by ACM to validate ownership of your custom domain\. Required only when you configure mutual TLS and you specify an ACM imported or private CA certificate ARN for the `CertificateArn`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[OwnershipVerificationCertificateArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigatewayv2-domainname-domainnameconfiguration.html#cfn-apigatewayv2-domainname-domainnameconfiguration-ownershipverificationcertificatearn)` property of the `AWS::ApiGatewayV2::DomainName` `DomainNameConfiguration` data type\.

 `Route53`   <a name="sam-httpapi-httpapidomainconfiguration-route53"></a>
Defines an Amazon Route 53 configuration\.  
*Type*: [Route53Configuration](sam-property-httpapi-route53configuration.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `SecurityPolicy`   <a name="sam-httpapi-httpapidomainconfiguration-securitypolicy"></a>
The TLS version of the security policy for this domain name\.  
The only valid value for HTTP APIs is `TLS_1_2`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[SecurityPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-apigatewayv2-domainname-domainnameconfiguration.html#cfn-apigatewayv2-domainname-domainnameconfiguration-securitypolicy)` property of the `AWS::ApiGatewayV2::DomainName` `DomainNameConfiguration` data type\.

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
    - foo
    - bar
```