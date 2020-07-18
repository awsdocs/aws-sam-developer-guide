# Route53Configuration<a name="sam-property-api-route53configuration"></a>

Configures the Route53 record sets for an API\.

## Syntax<a name="sam-property-api-route53configuration-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-route53configuration-syntax.yaml"></a>

```
  [DistributionDomainName](#sam-api-route53configuration-distributiondomainname): String
  [EvaluateTargetHealth](#sam-api-route53configuration-evaluatetargethealth): Boolean
  [HostedZoneId](#sam-api-route53configuration-hostedzoneid): String
  [HostedZoneName](#sam-api-route53configuration-hostedzonename): String
  [IpV6](#sam-api-route53configuration-ipv6): Boolean
```

## Properties<a name="sam-property-api-route53configuration-properties"></a>

 `DistributionDomainName`   <a name="sam-api-route53configuration-distributiondomainname"></a>
Configures a custom distribution of the API custom domain name\.  
*Type*: String  
*Required*: No  
*Default*: Use the API Gateway distribution\.  
*AWS CloudFormation compatibility*: This property is passed directly to the `[DNSName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-aliastarget-1.html#cfn-route53-aliastarget-dnshostname)` property of an `AWS::Route53::RecordSetGroup AliasTarget` resource\.  
*Additional Notes*: The domain name of a [CloudFront distribution](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cloudfront-distribution.html)\.

 `EvaluateTargetHealth`   <a name="sam-api-route53configuration-evaluatetargethealth"></a>
When EvaluateTargetHealth is true, an alias record inherits the health of the referenced AWS resource, such as an Elastic Load Balancing load balancer or another record in the hosted zone\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EvaluateTargetHealth](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-aliastarget.html#cfn-route53-aliastarget-evaluatetargethealth)` property of an `AWS::Route53::RecordSetGroup AliasTarget` resource\.  
*Additional Notes*: You can't set EvaluateTargetHealth to true when the alias target is a CloudFront distribution\.

 `HostedZoneId`   <a name="sam-api-route53configuration-hostedzoneid"></a>
The ID of the hosted zone that you want to create records in\.  
Specify either `HostedZoneName` or `HostedZoneId`, but not both\. If you have multiple hosted zones with the same domain name, you must specify the hosted zone using `HostedZoneId`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[HostedZoneId](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-recordset-1.html#cfn-route53-recordset-hostedzoneid)` property of an `AWS::Route53::RecordSetGroup RecordSet` resource\.

 `HostedZoneName`   <a name="sam-api-route53configuration-hostedzonename"></a>
The name of the hosted zone that you want to create records in\.  
Specify either `HostedZoneName` or `HostedZoneId`, but not both\. If you have multiple hosted zones with the same domain name, you must specify the hosted zone using `HostedZoneId`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[HostedZoneName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-recordset-1.html#cfn-route53-recordset-hostedzonename)` property of an `AWS::Route53::RecordSetGroup RecordSet` resource\.

 `IpV6`   <a name="sam-api-route53configuration-ipv6"></a>
When this property is set, AWS SAM creates a `AWS::Route53::RecordSet` resource and sets [Type](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-recordset.html#cfn-route53-recordset-type) to `AAAA` for the provided HostedZone\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-api-route53configuration--examples"></a>

### Route 53 Configuration Example<a name="sam-property-api-route53configuration--examples--route-53-configuration-example"></a>

This example shows how to configure Route 53\.

#### YAML<a name="sam-property-api-route53configuration--examples--route-53-configuration-example--yaml"></a>

```
Domain:
  DomainName: www.example.com
  CertificateArn: arn-example
  EndpointConfiguration: EDGE
  Route53:
    HostedZoneId: Z1PA6795UKMFR9
    EvaluateTargetHealth: true
    DistributionDomainName: xyz
```