# EventInvokeConfiguration<a name="sam-property-function-eventinvokeconfiguration"></a>

Configuration options for [asynchronous](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html) Lambda Alias or Version invocations\.

## Syntax<a name="sam-property-function-eventinvokeconfiguration-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-function-eventinvokeconfiguration-syntax.yaml"></a>

```
  [DestinationConfig](#sam-function-eventinvokeconfiguration-destinationconfig): [EventInvokeDestinationConfiguration](sam-property-function-eventinvokedestinationconfiguration.md)
  [MaximumEventAgeInSeconds](#sam-function-eventinvokeconfiguration-maximumeventageinseconds): Integer
  [MaximumRetryAttempts](#sam-function-eventinvokeconfiguration-maximumretryattempts): Integer
```

## Properties<a name="sam-property-function-eventinvokeconfiguration-properties"></a>

 `DestinationConfig`   <a name="sam-function-eventinvokeconfiguration-destinationconfig"></a>
A configuration object that specifies the destination of an event after Lambda processes it\.  
*Type*: [EventInvokeDestinationConfiguration](sam-property-function-eventinvokedestinationconfiguration.md)  
*Required*: No  
*CloudFormation Compatibility*: This property is similar to the `[DestinationConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventinvokeconfig-destinationconfig.html)` property of an `AWS::Lambda::EventInvokeConfig`\. SAM requires an extra parameter, "Type", that does not exist in CloudFormation\.

 `MaximumEventAgeInSeconds`   <a name="sam-function-eventinvokeconfiguration-maximumeventageinseconds"></a>
The maximum age of a request that Lambda sends to a function for processing\.  
*Type*: Integer  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[MaximumEventAgeInSeconds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventinvokeconfig.html#cfn-lambda-eventinvokeconfig-maximumeventageinseconds)` property of an `AWS::Lambda::EventInvokeConfig`\.

 `MaximumRetryAttempts`   <a name="sam-function-eventinvokeconfiguration-maximumretryattempts"></a>
The maximum age of a request that Lambda sends to a function for processing\.  
*Type*: Integer  
*Required*: No  
*CloudFormation Compatibility*: This property is passed directly to the `[MaximumRetryAttempts](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventinvokeconfig.html#cfn-lambda-eventinvokeconfig-maximumretryattempts)` property of an `AWS::Lambda::EventInvokeConfig`\.

## Examples<a name="sam-property-function-eventinvokeconfiguration--examples"></a>

### MaximumEventAgeInSeconds<a name="sam-property-function-eventinvokeconfiguration--examples--maximumeventageinseconds"></a>

MaximumEventAgeInSeconds example

#### YAML<a name="sam-property-function-eventinvokeconfiguration--examples--maximumeventageinseconds--yaml"></a>

```
EventInvokeConfig:
  DestinationConfig:
    OnFailure:
      Destination:
        Ref: DestinationLambda
      Type: Lambda
    OnSuccess:
      Destination: arn:aws:sqs:us-west-2:012345678901:my-queue
      Type: SQS
  MaximumEventAgeInSeconds: 60
  MaximumRetryAttempts: 2
```