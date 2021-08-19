# DomainConfiguration<a name="sam-property-api-domainconfiguration"></a>

Configures a custom domain for an API\.

## Syntax<a name="sam-property-api-domainconfiguration-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-domainconfiguration-syntax.yaml"></a>

```
  [BasePath](#sam-api-domainconfiguration-basepath): List
  [CertificateArn](#sam-api-domainconfiguration-certificatearn): String
  [DomainName](#sam-api-domainconfiguration-domainname): String
  [EndpointConfiguration](#sam-api-domainconfiguration-endpointconfiguration): String
  [MutualTlsAuthentication](#sam-api-domainconfiguration-mutualtlsauthentication): [MutualTlsAuthentication](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-mutualtlsauthentication)
  [Route53](#sam-api-domainconfiguration-route53): Route53Configuration
  [SecurityPolicy](#sam-api-domainconfiguration-securitypolicy): String
```

## Properties<a name="sam-property-api-domainconfiguration-properties"></a>

 `BasePath`   <a name="sam-api-domainconfiguration-basepath"></a>
A list of the basepaths to configure with the Amazon API Gateway domain name\.  
*Type*: List  
*Required*: No  
*Default*: /  
*AWS CloudFormation compatibility*: This property is similar to the `[BasePath](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-basepathmapping.html#cfn-apigateway-basepathmapping-basepath)` property of an `AWS::ApiGateway::BasePathMapping` resource\. AWS SAM creates multiple `AWS::ApiGateway::BasePathMapping` resources, one per `BasePath` specified in this property\.

 `CertificateArn`   <a name="sam-api-domainconfiguration-certificatearn"></a>
The Amazon Resource Name \(ARN\) of an AWS managed certificate this domain name's endpoint\. AWS Certificate Manager is the only supported source\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is similar to the `[CertificateArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-certificatearn)` property of an `AWS::ApiGateway::DomainName` resource\. If `EndpointConfiguration` is set to `REGIONAL` \(the default value\), `CertificateArn` maps to [RegionalCertificateArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-regionalcertificatearn) in `AWS::ApiGateway::DomainName`\. If the `EndpointConfiguration` is set to `EDGE`, `CertificateArn` maps to [CertificateArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-certificatearn) in `AWS::ApiGateway::DomainName`\.  
*Additional notes*: For an `EDGE` endpoint, you must create the certificate in the `us-east-1` AWS Region\.

 `DomainName`   <a name="sam-api-domainconfiguration-domainname"></a>
The custom domain name for your API Gateway API\. Uppercase letters are not supported\.  
AWS SAM generates an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html) resource when this property is set\. For information about this scenario, see [DomainName property is specified](sam-specification-generated-resources-api.md#sam-specification-generated-resources-api-domain-name)\. For information about generated AWS CloudFormation resources, see [Generated AWS CloudFormation resources](sam-specification-generated-resources.md)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[DomainName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-domainname)` property of an `AWS::ApiGateway::DomainName` resource\.

 `EndpointConfiguration`   <a name="sam-api-domainconfiguration-endpointconfiguration"></a>
Defines the type of API Gateway endpoint to map to the custom domain\. The value of this property determines how the `CertificateArn` property is mapped in AWS CloudFormation\.  
*Valid values*: `REGIONAL` or `EDGE`  
*Type*: String  
*Required*: No  
*Default*: `REGIONAL`  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `MutualTlsAuthentication`   <a name="sam-api-domainconfiguration-mutualtlsauthentication"></a>
The mutual Transport Layer Security \(TLS\) authentication configuration for a custom domain name\.  
*Type*: [MutualTlsAuthentication](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-mutualtlsauthentication)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MutualTlsAuthentication](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-mutualtlsauthentication)` property of an `AWS::ApiGateway::DomainName` resource\.

 `Route53`   <a name="sam-api-domainconfiguration-route53"></a>
Defines an Amazon Route 53 configuration\.  
*Type*: [Route53Configuration](sam-property-api-route53configuration.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `SecurityPolicy`   <a name="sam-api-domainconfiguration-securitypolicy"></a>
The TLS version plus cipher suite for this domain name\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[SecurityPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-securitypolicy)` property of an `AWS::ApiGateway::DomainName` resource\.

## Examples<a name="sam-property-api-domainconfiguration--examples"></a>

### DomainName<a name="sam-property-api-domainconfiguration--examples--domainname"></a>

DomainName example

#### YAML<a name="sam-property-api-domainconfiguration--examples--domainname--yaml"></a>

```
Domain:
  DomainName: www.example.com
  CertificateArn: arn-example
  EndpointConfiguration: EDGE
  Route53:
    HostedZoneId: Z1PA6795UKMFR9
  BasePath:
    - /foo
    - /bar
```