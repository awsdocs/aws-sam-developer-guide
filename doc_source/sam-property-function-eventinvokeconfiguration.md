# EventInvokeConfiguration<a name="sam-property-function-eventinvokeconfiguration"></a>

Configuration options for [asynchronous](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html) Lambda Alias or Version invocations\.

## Syntax<a name="sam-property-function-eventinvokeconfiguration-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-eventinvokeconfiguration-syntax.yaml"></a>

```
  [DestinationConfig](#sam-function-eventinvokeconfiguration-destinationconfig): EventInvokeDestinationConfiguration
  [MaximumEventAgeInSeconds](#sam-function-eventinvokeconfiguration-maximumeventageinseconds): Integer
  [MaximumRetryAttempts](#sam-function-eventinvokeconfiguration-maximumretryattempts): Integer
```

## Properties<a name="sam-property-function-eventinvokeconfiguration-properties"></a>

 `DestinationConfig`   <a name="sam-function-eventinvokeconfiguration-destinationconfig"></a>
A configuration object that specifies the destination of an event after Lambda processes it\.  
*Type*: [EventInvokeDestinationConfiguration](sam-property-function-eventinvokedestinationconfiguration.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[DestinationConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventinvokeconfig-destinationconfig.html)` property of an `AWS::Lambda::EventInvokeConfig` resource\. SAM requires an extra parameter, "Type", that does not exist in CloudFormation\.

 `MaximumEventAgeInSeconds`   <a name="sam-function-eventinvokeconfiguration-maximumeventageinseconds"></a>
The maximum age of a request that Lambda sends to a function for processing\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MaximumEventAgeInSeconds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventinvokeconfig.html#cfn-lambda-eventinvokeconfig-maximumeventageinseconds)` property of an `AWS::Lambda::EventInvokeConfig` resource\.

 `MaximumRetryAttempts`   <a name="sam-function-eventinvokeconfiguration-maximumretryattempts"></a>
The maximum number of times to retry before the function returns an error\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MaximumRetryAttempts](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventinvokeconfig.html#cfn-lambda-eventinvokeconfig-maximumretryattempts)` property of an `AWS::Lambda::EventInvokeConfig` resource\.

## Examples<a name="sam-property-function-eventinvokeconfiguration--examples"></a>

### MaximumEventAgeInSeconds<a name="sam-property-function-eventinvokeconfiguration--examples--maximumeventageinseconds"></a>

MaximumEventAgeInSeconds example

#### YAML<a name="sam-property-function-eventinvokeconfiguration--examples--maximumeventageinseconds--yaml"></a>

```
EventInvokeConfig:
  MaximumEventAgeInSeconds: 60
  MaximumRetryAttempts: 2
  DestinationConfig:
    OnSuccess:
      Type: SQS
      Destination: arn:aws:sqs:us-west-2:012345678901:my-queue
    OnFailure:
      Type: Lambda
      Destination: !GetAtt DestinationLambda.Arn
```