# ApiUsagePlan<a name="sam-property-api-apiusageplan"></a>

Configures a usage plan for an API Gateway API\. For more information about usage plans, see [Create and Use Usage Plans with API Keys](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html) in the API Gateway Developer Guide\.

## Syntax<a name="sam-property-api-apiusageplan-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-api-apiusageplan-syntax.yaml"></a>

```
  [CreateUsagePlan](#sam-api-apiusageplan-createusageplan): String
  [Description](#sam-api-apiusageplan-description): String
  [Quota](#sam-api-apiusageplan-quota): [QuotaSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html#cfn-apigateway-usageplan-quota)
  [Tags](#sam-api-apiusageplan-tags): List
  [Throttle](#sam-api-apiusageplan-throttle): [ThrottleSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html#cfn-apigateway-usageplan-throttle)
  [UsagePlanName](#sam-api-apiusageplan-usageplanname): String
```

## Properties<a name="sam-property-api-apiusageplan-properties"></a>

 `CreateUsagePlan`   <a name="sam-api-apiusageplan-createusageplan"></a>
Determines how this usage plan is configured\. Valid values are `PER_API`, `SHARED`, and `NONE`\.  
`PER_API` creates [AWS::ApiGateway::UsagePlan](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html), [AWS::ApiGateway::ApiKey](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-apikey.html), and [AWS::ApiGateway::UsagePlanKey](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplankey.html) resources that are specific to this API\. These resources have logical IDs of `<api-logical-id>UsagePlan`, `<api-logical-id>ApiKey`, and `<api-logical-id>UsagePlanKey`, respectively\.  
`SHARED` creates [AWS::ApiGateway::UsagePlan](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html), [AWS::ApiGateway::ApiKey](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-apikey.html), and [AWS::ApiGateway::UsagePlanKey](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplankey.html) resources that are shared across any API that also has `CreateUsagePlan: SHARED` in the same AWS SAM template\. These resources have logical IDs of `ServerlessUsagePlan`, `ServerlessApiKey`, and `ServerlessUsagePlanKey`, respectively\. If you use this option, we recommend that you add additional configuration for this usage plan on only one API resource to avoid conflicting definitions and an uncertain state\.  
`NONE` disables the creation or association of a usage plan with this API\. This is only necessary if `SHARED` or `PER_API` is specified in the [Globals section of the AWS SAM template](sam-specification-template-anatomy-globals.md)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `Description`   <a name="sam-api-apiusageplan-description"></a>
A description of the usage plan\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Description](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html#cfn-apigateway-usageplan-description)` property of an `AWS::ApiGateway::UsagePlan` resource\.

 `Quota`   <a name="sam-api-apiusageplan-quota"></a>
Configures the number of requests that users can make within a given interval\.  
*Type*: [QuotaSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html#cfn-apigateway-usageplan-quota)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Quota](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html#cfn-apigateway-usageplan-quota)` property of an `AWS::ApiGateway::UsagePlan` resource\.

 `Tags`   <a name="sam-api-apiusageplan-tags"></a>
An array of arbitrary tags \(key\-value pairs\) to associate with the usage plan\.  
This property uses the [CloudFormation Tag Type](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-resource-tags.html)\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Tags](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html#cfn-apigateway-usageplan-tags)` property of an `AWS::ApiGateway::UsagePlan` resource\.

 `Throttle`   <a name="sam-api-apiusageplan-throttle"></a>
Configures the overall request rate \(average requests per second\) and burst capacity\.  
*Type*: [ThrottleSettings](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html#cfn-apigateway-usageplan-throttle)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Throttle](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html#cfn-apigateway-usageplan-throttle)` property of an `AWS::ApiGateway::UsagePlan` resource\.

 `UsagePlanName`   <a name="sam-api-apiusageplan-usageplanname"></a>
A name for the usage plan\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[UsagePlanName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-usageplan.html#cfn-apigateway-usageplan-usageplanname)` property of an `AWS::ApiGateway::UsagePlan` resource\.

## Examples<a name="sam-property-api-apiusageplan--examples"></a>

### UsagePlan<a name="sam-property-api-apiusageplan--examples--usageplan"></a>

The following is a usage plan example\.

#### YAML<a name="sam-property-api-apiusageplan--examples--usageplan--yaml"></a>

```
Auth:
  UsagePlan:
    CreateUsagePlan: PER_API
    Description: Usage plan for this API
    Quota:
      Limit: 500
      Period: MONTH
    Throttle:
      BurstLimit: 100
      RateLimit: 50
    Tags:
      - Key: TagName
        Value: TagValue
```