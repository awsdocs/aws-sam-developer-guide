# DomainConfiguration<a name="sam-property-api-domainconfiguration"></a>

Configuration for a custom domain for an API\.

## Syntax<a name="sam-property-api-domainconfiguration-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-api-domainconfiguration-syntax.yaml"></a>

```
  [BasePath](#sam-api-domainconfiguration-basepath): List
  [CertificateArn](#sam-api-domainconfiguration-certificatearn): String
  [EndpointConfiguration](#sam-api-domainconfiguration-endpointconfiguration): String
  [DomainName](#sam-api-domainconfiguration-domainname): String
  [Route53](#sam-api-domainconfiguration-route53): [Route53Configuration](sam-property-api-route53configuration.md)
```

## Properties<a name="sam-property-api-domainconfiguration-properties"></a>

 `BasePath`   <a name="sam-api-domainconfiguration-basepath"></a>
List of basepaths to be configured with the API Gateway Domain Name\.  
*Type*: List  
*Required*: No  
*Default*: /  
*CloudFormation Compatibility*: This property is similar to the `[BasePath](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-basepathmapping.html#cfn-apigateway-basepathmapping-basepath)` property of an `AWS::ApiGateway::BasePathMapping`\. SAM will create multiple `AWS::ApiGateway::BasePathMapping` resources, one per `BasePath` specified in this property\.

 `CertificateArn`   <a name="sam-api-domainconfiguration-certificatearn"></a>
The reference to an AWS\-managed certificate for use by the endpoint for this domain name\. AWS Certificate Manager is the only supported source\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is similar to the `[CertificateArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-certificatearn)` property of an `AWS::ApiGateway::DomainName`\. If `EndpointConfiguration` is set to `REGIONAL` \(the default value\), `CertificateArn` maps to [RegionalCertificateArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-regionalcertificatearn) in `AWS::ApiGateway::DomainName`\. If the `EndpointConfiguration` is set to `EDGE`, `CertificateArn` maps to [CertificateArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-certificatearn) in `AWS::ApiGateway::DomainName`\.  
*Additional Notes*: For an `EDGE` endpoint, the certificate must be created in the `us-east-1` region\.

 `EndpointConfiguration`   <a name="sam-api-domainconfiguration-endpointconfiguration"></a>
Property to define the type of API Gateway endpoint to be mapped to the custom domain\. The value of this property controls how the `CertificateArn` property gets mapped in AWS CloudFormation\. See `CertificateArn` above\.  
Valid values are `REGIONAL` or `EDGE`\.  
*Type*: String  
*Required*: No  
*Default*: REGIONAL  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

 `DomainName`   <a name="sam-api-domainconfiguration-domainname"></a>
The custom domain name for your API Gateway API\. Uppercase letters are not supported\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is passed directly to the `[DomainName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-domainname.html#cfn-apigateway-domainname-domainname)` property of an `AWS::ApiGateway::DomainName`\.

 `Route53`   <a name="sam-api-domainconfiguration-route53"></a>
Property that adds Route53 configuration based on the values defined\.  
*Type*: [Route53Configuration](sam-property-api-route53configuration.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-api-domainconfiguration--examples"></a>

### DomainName<a name="sam-property-api-domainconfiguration--examples--domainname"></a>

DomainName example

#### YAML<a name="sam-property-api-domainconfiguration--examples--domainname--yaml"></a>

```
Domain:
  BasePath:
  - /foo
  - /bar
  CertificateArn: arn-example
  DomainName: www.example.com
  EndpointConfiguration: EDGE
  Route53:
    HostedZoneId: xyz
```
