# Route53Configuration<a name="sam-property-api-route53configuration"></a>

## Syntax<a name="sam-property-api-route53configuration-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-api-route53configuration-syntax.yaml"></a>

```
  [DistributionDomainName](#sam-api-route53configuration-distributiondomainname): String
  [EvaluateTargetHealth](#sam-api-route53configuration-evaluatetargethealth): Boolean
  [HostedZoneId](#sam-api-route53configuration-hostedzoneid): String
```

## Properties<a name="sam-property-api-route53configuration-properties"></a>

 `DistributionDomainName`   <a name="sam-api-route53configuration-distributiondomainname"></a>
Use this to configure a custom distribution of the API Custom Domain Name\.  
*Type*: String  
*Required*: No  
*Default*: Use the API Gateway Distribution  
*CloudFormation Compatibility*: This property is passed directly to the `[DNSName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-aliastarget-1.html#cfn-route53-aliastarget-dnshostname)` property of an `AWS::Route53::RecordSetGroup AliasTarget`\.  
*Additional Notes*: Domain name of a [cloudfront distribution](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cloudfront-distribution.html)\.

 `EvaluateTargetHealth`   <a name="sam-api-route53configuration-evaluatetargethealth"></a>
When EvaluateTargetHealth is true, an alias record inherits the health of the referenced AWS resource, such as an ELB load balancer or another record in the hosted zone\.  
*Type*: Boolean  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[EvaluateTargetHealth](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-aliastarget.html#cfn-route53-aliastarget-evaluatetargethealth)` property of an `AWS::Route53::RecordSetGroup AliasTarget`\.  
*Additional Notes*: You can't set EvaluateTargetHealth to true when the alias target is a CloudFront distribution\.

 `HostedZoneId`   <a name="sam-api-route53configuration-hostedzoneid"></a>
HostedZoneId for the domain name\.  
*Type*: String  
*Required*: Yes  
*CloudFormation Compatibility*: This property is passed directly to the `[HostedZoneId](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-recordset-1.html#cfn-route53-recordset-hostedzoneid)` property of an `AWS::Route53::RecordSetGroup RecordSet`\.

## Examples<a name="sam-property-api-route53configuration--examples"></a>

### Route 53 Configuration Example<a name="sam-property-api-route53configuration--examples--route-53-configuration-example"></a>

Shows how to configure route 53

#### YAML<a name="sam-property-api-route53configuration--examples--route-53-configuration-example--yaml"></a>

```
Domain:
  CertificateArn: arn-example
  DomainName: www.example.com
  EndpointConfiguration: EDGE
  Route53:
    DistributionDomainName: xyz
    EvaluateTargetHealth: true
    HostedZoneId: xyz
```