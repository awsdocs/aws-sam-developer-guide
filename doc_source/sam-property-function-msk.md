# MSK<a name="sam-property-function-msk"></a>

The object describing an `MSK` event source type\. For more information, see [Using AWS Lambda with Amazon MSK](https://docs.aws.amazon.com/lambda/latest/dg/with-msk.html) in the *AWS Lambda Developer Guide*\.

AWS SAM generates an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html) resource when this event type is set\.

## Syntax<a name="sam-property-function-msk-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-msk-syntax.yaml"></a>

```
  [MaximumBatchingWindowInSeconds](#sam-function-msk-maximumbatchingwindowinseconds): Integer
  [StartingPosition](#sam-function-msk-startingposition): String
  [Stream](#sam-function-msk-stream): String
  [Topics](#sam-function-msk-topics): List
```

## Properties<a name="sam-property-function-msk-properties"></a>

 `MaximumBatchingWindowInSeconds`   <a name="sam-function-msk-maximumbatchingwindowinseconds"></a>
The maximum amount of time to gather records before invoking the function, in seconds\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[MaximumBatchingWindowInSeconds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumbatchingwindowinseconds)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `StartingPosition`   <a name="sam-function-msk-startingposition"></a>
The position in a stream from which to start reading\.  
*Valid values*: `TRIM_HORIZON` or `LATEST`  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[StartingPosition](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-startingposition)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Stream`   <a name="sam-function-msk-stream"></a>
The Amazon Resource Name \(ARN\) of the data stream or a stream consumer\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EventSourceArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-eventsourcearn)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Topics`   <a name="sam-function-msk-topics"></a>
The name of the Kafka topic\.  
*Type*: List  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Topics](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-topics)` property of an `AWS::Lambda::EventSourceMapping` resource\.

## Examples<a name="sam-property-function-msk--examples"></a>

### Amazon MSK Example for Existing Cluster<a name="sam-property-function-msk--examples--amazon-msk-example-for-existing-cluster"></a>

The following is an example of an `MSK` event source type for an Amazon MSK cluster that already exists in an AWS account\.

#### YAML<a name="sam-property-function-msk--examples--amazon-msk-example-for-existing-cluster--yaml"></a>

```
Events:
  MSKEvent:
    Type: MSK
    Properties:
      StartingPosition: LATEST
      Stream: arn:aws:kafka:us-east-1:012345678012:cluster/exampleClusterName/abcdefab-1234-abcd-5678-cdef0123ab01-2
      Topics:
        - MyTopic
```

### Amazon MSK Example for Cluster Declared in Same Template<a name="sam-property-function-msk--examples--amazon-msk-example-for-cluster-declared-in-same-template"></a>

The following is an example of an `MSK` event source type for an Amazon MSK cluster that is declared in the same template file\.

#### YAML<a name="sam-property-function-msk--examples--amazon-msk-example-for-cluster-declared-in-same-template--yaml"></a>

```
Events:
  MSKEvent:
    Type: MSK
    Properties:
      StartingPosition: LATEST
      Stream:
        Ref: MyMskCluster   # This must be the name of an MSK cluster declared in the same template file
      Topics:
        - MyTopic
```