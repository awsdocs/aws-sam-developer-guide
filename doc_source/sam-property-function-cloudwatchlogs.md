# CloudWatchLogs<a name="sam-property-function-cloudwatchlogs"></a>

The object describing a `CloudWatchLogs` event source type\.

This event generates a [AWS::Logs::SubscriptionFilter](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-logs-subscriptionfilter.html) resource and specifies a subscription filter and associates it with the specified log group\.

## Syntax<a name="sam-property-function-cloudwatchlogs-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-cloudwatchlogs-syntax.yaml"></a>

```
  [FilterPattern](#sam-function-cloudwatchlogs-filterpattern): String
  [LogGroupName](#sam-function-cloudwatchlogs-loggroupname): String
```

## Properties<a name="sam-property-function-cloudwatchlogs-properties"></a>

 `FilterPattern`   <a name="sam-function-cloudwatchlogs-filterpattern"></a>
The filtering expressions that restrict what gets delivered to the destination AWS resource\. For more information about the filter pattern syntax, see [Filter and Pattern Syntax](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/FilterAndPatternSyntax.html)\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[FilterPattern](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-logs-subscriptionfilter.html#cfn-cwl-subscriptionfilter-filterpattern)` property of an `AWS::Logs::SubscriptionFilter` resource\.

 `LogGroupName`   <a name="sam-function-cloudwatchlogs-loggroupname"></a>
The log group to associate with the subscription filter\. All log events that are uploaded to this log group are filtered and delivered to the specified AWS resource if the filter pattern matches the log events\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[LogGroupName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-logs-subscriptionfilter.html#cfn-cwl-subscriptionfilter-loggroupname)` property of an `AWS::Logs::SubscriptionFilter` resource\.

## Examples<a name="sam-property-function-cloudwatchlogs--examples"></a>

### Cloudwatchlogs Subscription filter<a name="sam-property-function-cloudwatchlogs--examples--cloudwatchlogs-subscription-filter"></a>

Cloudwatchlogs Subscription filter Example

#### YAML<a name="sam-property-function-cloudwatchlogs--examples--cloudwatchlogs-subscription-filter--yaml"></a>

```
CWLog:
  Type: CloudWatchLogs
  Properties:
    LogGroupName:
      Ref: CloudWatchLambdaLogsGroup
    FilterPattern: My pattern
```