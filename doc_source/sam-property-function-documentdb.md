# DocumentDB<a name="sam-property-function-documentdb"></a>

The object describing a `DocumentDB` event source type\. For more information, see [Using AWS Lambda with Amazon DocumentDB](https://docs.aws.amazon.com/lambda/latest/dg/with-documentdb.html) in the *AWS Lambda Developer Guide*\.

## Syntax<a name="sam-property-function-documentdb-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax\.

### YAML<a name="sam-property-function-documentdb-syntax-yaml"></a>

```
BatchSize: Integer
Cluster: [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html)
CollectionName: String
DatabaseName: String
Enabled: Boolean
FilterCriteria: [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html)
FullDocument: String
MaximumBatchingWindowInSeconds: Integer
SecretsManagerKmsKeyId: String
SourceAccessConfigurations: List
StartingPosition: String
StartingPositionTimestamp: Double
```

## Properties<a name="sam-property-function-documentdb-properties"></a>

 `BatchSize`   <a name="sam-function-documentdb-batchsize"></a>
The maximum number of items to retrieve in a single batch\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ BatchSize](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-batchsize)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `Cluster`   <a name="sam-function-documentdb-cluster"></a>
The Amazon Resource Name \(ARN\) of the Amazon DocumentDB cluster\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ EventSourceArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-eventsourcearn)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `CollectionName`   <a name="sam-function-documentdb-collectionname"></a>
The name of the collection to consume within the database\. If you do not specify a collection, Lambda consumes all collections\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ CollectionName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-documentdbeventsourceconfig.html#cfn-lambda-eventsourcemapping-documentdbeventsourceconfig-collectionname)` property of an `AWS::Lambda::EventSourceMapping` `DocumentDBEventSourceConfig` data type\.

 `DatabaseName`   <a name="sam-function-documentdb-databasename"></a>
The name of the database to consume within the Amazon DocumentDB cluster\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ DatabaseName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-documentdbeventsourceconfig.html#cfn-lambda-eventsourcemapping-documentdbeventsourceconfig-databasename)` property of an `AWS::Lambda::EventSourceMapping` `DocumentDBEventSourceConfig`data type\.

 `Enabled`   <a name="sam-function-documentdb-enabled"></a>
If `true`, the event source mapping is active\. To pause polling and invocation, set to `false`\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ Enabled](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-enabled)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `FilterCriteria`   <a name="sam-function-documentdb-filtercriteria"></a>
An object that defines the criteria that determines whether Lambda should process an event\. For more information, see [ Lambda event filtering](https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventfiltering.html) in the *AWS Lambda Developer Guide*\.  
*Type*: [FilterCriteria](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ FilterCriteria](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-filtercriteria.html)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `FullDocument`   <a name="sam-function-documentdb-fulldocument"></a>
Determines what Amazon DocumentDB sends to your event stream during document update operations\. If set to `UpdateLookup`, Amazon DocumentDB sends a delta describing the changes, along with a copy of the entire document\. Otherwise, Amazon DocumentDB sends only a partial document that contains the changes\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ FullDocument](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-documentdbeventsourceconfig.html#cfn-lambda-eventsourcemapping-documentdbeventsourceconfig-fulldocument)` property of an `AWS::Lambda::EventSourceMapping` `DocumentDBEventSourceConfig` data type\.

 `MaximumBatchingWindowInSeconds`   <a name="sam-function-documentdb-maximumbatchingwindowinseconds"></a>
The maximum amount of time to gather records before invoking the function, in seconds\.  
*Type*: Integer  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ MaximumBatchingWindowInSeconds](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-maximumbatchingwindowinseconds)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `SecretsManagerKmsKeyId`   <a name="sam-function-documentdb-secretsmanagerkmskeyid"></a>
The AWS Key Management Service \(AWS KMS\) key ID of a customer managed key from AWS Secrets Manager\. Required when you use a customer managed key from Secrets Manager with a Lambda execution role that doesn’t include the `kms:Decrypt` permission\.  
The value of this property is a UUID\. For example: `1abc23d4-567f-8ab9-cde0-1fab234c5d67`\.  
*Type*: String  
*Required*: Conditional  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn’t have an AWS CloudFormation equivalent\.

 `SourceAccessConfigurations`   <a name="sam-function-documentdb-sourceaccessconfigurations"></a>
An array of the authentication protocol or virtual host\. Specify this using the [ SourceAccessConfigurations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventsourcemapping-sourceaccessconfiguration.html) data type\.  
For the `DocumentDB` event source type, the only valid configuration type is `BASIC_AUTH`\.  
+ `BASIC_AUTH` – The Secrets Manager secret that stores your broker credentials\. For this type, the credential must be in the following format: `{"username": "your-username", "password": "your-password"}`\. Only one object of type `BASIC_AUTH` is allowed\.
*Type*: List  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ SourceAccessConfigurations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-sourceaccessconfigurations)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `StartingPosition`   <a name="sam-function-documentdb-startingposition"></a>
The position in a stream from which to start reading\.  
+ `AT_TIMESTAMP` – Specify a time from which to start reading records\.
+ `LATEST` – Read only new records\.
+ `TRIM_HORIZON` – Process all available records\.
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ StartingPosition](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-startingposition)` property of an `AWS::Lambda::EventSourceMapping` resource\.

 `StartingPositionTimestamp`   <a name="sam-function-documentdb-startingpositiontimestamp"></a>
The time from which to start reading, in Unix time seconds\. Define `StartingPositionTimestamp` when `StartingPosition` is specified as `AT_TIMESTAMP`\.  
*Type*: Double  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ StartingPositionTimestamp](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-eventsourcemapping.html#cfn-lambda-eventsourcemapping-startingpositiontimestamp)` property of an `AWS::Lambda::EventSourceMapping` resource\.

## Examples<a name="sam-property-function-documentdb-examples"></a>

### Amazon DocumentDB event source<a name="sam-property-function-documentdb-examples-example1"></a>

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
    ...
      Events:
        MyDDBEvent:
          Type: DocumentDB
          Properties:
            Cluster: "arn:aws:rds:us-west-2:123456789012:cluster:docdb-2023-01-01"
            BatchSize: 10
            MaximumBatchingWindowInSeconds: 5
            DatabaseName: "db1"
            CollectionName: "collection1"
            FullDocument: "UpdateLookup"
            SourceAccessConfigurations:
              - Type: BASIC_AUTH
                URI: "arn:aws:secretsmanager:us-west-2:123456789012:secret:doc-db"
```