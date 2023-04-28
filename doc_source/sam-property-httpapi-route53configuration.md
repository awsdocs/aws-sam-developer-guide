# Route53Configuration<a name="sam-property-httpapi-route53configuration"></a>

Configures the Route53 record sets for an API\.

## Syntax<a name="sam-property-httpapi-route53configuration-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-httpapi-route53configuration-syntax.yaml"></a>

```
  [DistributionDomainName](#sam-httpapi-route53configuration-distributiondomainname): String
  [EvaluateTargetHealth](#sam-httpapi-route53configuration-evaluatetargethealth): Boolean
  [HostedZoneId](#sam-httpapi-route53configuration-hostedzoneid): String
  [HostedZoneName](#sam-httpapi-route53configuration-hostedzonename): String
  [IpV6](#sam-httpapi-route53configuration-ipv6): Boolean
  Region: String
  SetIdentifier: String
```

## Properties<a name="sam-property-httpapi-route53configuration-properties"></a>

 `DistributionDomainName`   <a name="sam-httpapi-route53configuration-distributiondomainname"></a>
Configures a custom distribution of the API custom domain name\.  
*Type*: String  
*Required*: No  
*Default*: Use the API Gateway distribution\.  
*AWS CloudFormation compatibility*: This property is passed directly to the `[DNSName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-aliastarget-1.html#cfn-route53-aliastarget-dnshostname)` property of an `AWS::Route53::RecordSetGroup AliasTarget` resource\.  
*Additional notes*: The domain name of a [CloudFront distribution](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cloudfront-distribution.html)\.

 `EvaluateTargetHealth`   <a name="sam-httpapi-route53configuration-evaluatetargethealth"></a>
When EvaluateTargetHealth is true, an alias record inherits the health of the referenced AWS resource, such as an Elastic Load Balancing load balancer or another record in the hosted zone\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EvaluateTargetHealth](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-aliastarget.html#cfn-route53-aliastarget-evaluatetargethealth)` property of an `AWS::Route53::RecordSetGroup AliasTarget` resource\.  
*Additional notes*: You can't set EvaluateTargetHealth to true when the alias target is a CloudFront distribution\.

 `HostedZoneId`   <a name="sam-httpapi-route53configuration-hostedzoneid"></a>
The ID of the hosted zone that you want to create records in\.  
Specify either `HostedZoneName` or `HostedZoneId`, but not both\. If you have multiple hosted zones with the same domain name, you must specify the hosted zone using `HostedZoneId`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[HostedZoneId](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-recordset-1.html#cfn-route53-recordset-hostedzoneid)` property of an `AWS::Route53::RecordSetGroup RecordSet` resource\.

 `HostedZoneName`   <a name="sam-httpapi-route53configuration-hostedzonename"></a>
The name of the hosted zone that you want to create records in\. You must include a trailing dot \(for example, `www.example.com.`\) as part of the `HostedZoneName`\.  
Specify either `HostedZoneName` or `HostedZoneId`, but not both\. If you have multiple hosted zones with the same domain name, you must specify the hosted zone using `HostedZoneId`\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[HostedZoneName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-recordset-1.html#cfn-route53-recordset-hostedzonename)` property of an `AWS::Route53::RecordSetGroup RecordSet` resource\.

 `IpV6`   <a name="sam-httpapi-route53configuration-ipv6"></a>
When this property is set, AWS SAM creates a `AWS::Route53::RecordSet` resource and sets [Type](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-recordset.html#cfn-route53-recordset-type) to `AAAA` for the provided HostedZone\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

`Region`  <a name="sam-httpapi-route53configuration-region"></a>
*Latency\-based resource record sets only:* The Amazon EC2 Region where you created the resource that this resource record set refers to\. The resource typically is an AWS resource, such as an EC2 instance or an ELB load balancer, and is referred to by an IP address or a DNS domain name, depending on the record type\.  
When Amazon Route 53 receives a DNS query for a domain name and type for which you have created latency resource record sets, Route 53 selects the latency resource record set that has the lowest latency between the end user and the associated Amazon EC2 Region\. Route 53 then returns the value that is associated with the selected resource record set\.  
Note the following:  
+ You can only specify one `ResourceRecord` per latency resource record set\.
+ You can only create one latency resource record set for each Amazon EC2 Region\.
+ You aren't required to create latency resource record sets for all Amazon EC2 Regions\. Route 53 will choose the region with the best latency from among the regions that you create latency resource record sets for\.
+ You can't create non\-latency resource record sets that have the same values for the `Name` and `Type` elements as latency resource record sets\.
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ Region](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-recordset-1.html#cfn-route53-recordset-region)` property of an `AWS::Route53::RecordSetGroup` `RecordSet` data type\.

`SetIdentifier`  <a name="sam-httpapi-route53configuration-setidentifier"></a>
*Resource record sets that have a routing policy other than simple:* An identifier that differentiates among multiple resource record sets that have the same combination of name and type, such as multiple weighted resource record sets named acme\.example\.com that have a type of A\. In a group of resource record sets that have the same name and type, the value of `SetIdentifier` must be unique for each resource record set\.  
For information about routing policies, see [Choosing a routing policy](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html) in the *Amazon Route 53 Developer Guide*\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ SetIdentifier](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-route53-recordset-1.html#cfn-route53-recordset-setidentifier)` property of an `AWS::Route53::RecordSetGroup` `RecordSet` data type\.

## Examples<a name="sam-property-httpapi-route53configuration--examples"></a>

### Route 53 Configuration Example<a name="sam-property-httpapi-route53configuration--examples--route-53-configuration-example"></a>

This example shows how to configure Route 53\.

#### YAML<a name="sam-property-httpapi-route53configuration--examples--route-53-configuration-example--yaml"></a>

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