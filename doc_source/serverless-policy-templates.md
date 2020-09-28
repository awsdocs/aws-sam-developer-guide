# AWS SAM policy templates<a name="serverless-policy-templates"></a>

AWS SAM allows you to choose from a list of policy templates to scope the permissions of your Lambda functions to the resources that are used by your application\.

AWS SAM applications in the AWS Serverless Application Repository that use policy templates don't require any special customer acknowledgments to deploy the application from the AWS Serverless Application Repository\.

If you want to request a new policy template to be added, do the following:

1. Submit a pull request against the policy\_templates\.json source file in the `develop` branch of the AWS SAM GitHub project\. You can find the source file in [policy\_templates\.json](https://github.com/aws/serverless-application-model/blob/develop/samtranslator/policy_templates_data/policy_templates.json) on the GitHub website\.

1. Submit an issue in the AWS SAM GitHub project that includes the reasons for your pull request and a link to the request\. Use this link to submit a new issue: [AWS Serverless Application Model: Issues](https://github.com/aws/serverless-application-model/issues/new)\.

## Syntax<a name="serverless-policy-template-syntax"></a>

For every policy template you specify in your AWS SAM template file, you must always specify an object containing the policy template's placeholder values\. If a policy template does not require any placeholder values, you must specify an empty object\.

### YAML<a name="serverless-policy-template-syntax.yaml"></a>

```
MyFunction:
  Type: AWS::Serverless::Function
  Properties:
    Policies:
      - PolicyTemplateName1:        # Policy template with placeholder value
          Key1: Value1
      - PolicyTemplateName2: {}     # Policy template with no placeholder value
```

## Examples<a name="serverless-policy-template-examples"></a>

### Example 1: Policy template with placeholder values<a name="policy-template-example-1"></a>

The following example shows that the [SQSPollerPolicy](serverless-policy-template-list.md#sqs-poller-policy) policy template expects a `QueueName` as a resource\. The AWS SAM template retrieves the name of the "`MyQueue`" Amazon SQS queue, which you can create in the same application or requested as a parameter to the application\.

```
 1. MyFunction:
 2.   Type: 'AWS::Serverless::Function'
 3.   Properties:
 4.     CodeUri: ${codeuri}
 5.     Handler: hello.handler
 6.     Runtime: python2.7
 7.     Policies:
 8.       - SQSPollerPolicy:
 9.           QueueName:
10.             !GetAtt MyQueue.QueueName
```

### Example 2: Policy template with no placeholder values<a name="policy-template-example-2"></a>

The following example contains the [CloudWatchPutMetricPolicy](serverless-policy-template-list.md#cloudwatch-put-metric-policy) policy template, which has no placeholder values\.

**Note**  
Even though there are no placeholder values, you must specify an empty object, otherwise an error will result\.

```
1. MyFunction:
2.   Type: 'AWS::Serverless::Function'
3.   Properties:
4.     CodeUri: ${codeuri}
5.     Handler: hello.handler
6.     Runtime: python2.7
7.     Policies:
8.       - CloudWatchPutMetricPolicy: {}
```

## Policy template table<a name="serverless-policy-template-table"></a>

The following is a table of the available policy templates\.


****  

| Policy Template | Description | 
| --- | --- | 
| [SQSPollerPolicy](serverless-policy-template-list.md#sqs-poller-policy) | Gives permission to poll an Amazon Simple Queue Service \(Amazon SQS\) queue\. | 
| [LambdaInvokePolicy](serverless-policy-template-list.md#lambda-invoke-policy) | Gives permission to invoke an AWS Lambda function, alias, or version\. | 
| [CloudWatchDescribeAlarmHistoryPolicy](serverless-policy-template-list.md#cloudwatch-describe-alarm-history-policy) | Gives permission to describe CloudWatch alarm history\. | 
| [CloudWatchPutMetricPolicy](serverless-policy-template-list.md#cloudwatch-put-metric-policy) | Gives permission to send metrics to CloudWatch\. | 
| [EC2DescribePolicy](serverless-policy-template-list.md#ec2-describe-policy) | Gives permission to describe Amazon Elastic Compute Cloud \(Amazon EC2\) instances\. | 
| [DynamoDBCrudPolicy](serverless-policy-template-list.md#dynamo-db-crud-policy) | Gives create, read, update, and delete permissions to an Amazon DynamoDB table\. | 
| [DynamoDBReadPolicy](serverless-policy-template-list.md#dynamo-db-read-policy) | Gives read\-only permission to a DynamoDB table\. | 
| [DynamoDBWritePolicy](serverless-policy-template-list.md#dynamo-db-write-policy) | Gives write\-only permission to a DynamoDB table\. | 
| [DynamoDBReconfigurePolicy](serverless-policy-template-list.md#dynamo-db-reconfigure-policy) | Gives permission to reconfigure a DynamoDB table\. | 
| [SESSendBouncePolicy](serverless-policy-template-list.md#ses-send-bounce-policy) | Gives SendBounce permission to an Amazon Simple Email Service \(Amazon SES\) identity\. | 
| [ElasticsearchHttpPostPolicy](serverless-policy-template-list.md#elastic-search-http-post-policy) | Gives POST permission to Amazon Elasticsearch Service\. | 
| [S3ReadPolicy](serverless-policy-template-list.md#s3-read-policy) | Gives read\-only permission to objects in an Amazon Simple Storage Service \(Amazon S3\) bucket\. | 
| [S3WritePolicy](serverless-policy-template-list.md#s3-write-policy) | Gives write permission to objects in an Amazon S3 bucket\. | 
| [S3CrudPolicy](serverless-policy-template-list.md#s3-crud-policy) | Gives create, read, update, and delete permission to objects in an Amazon S3 bucket\. | 
| [AMIDescribePolicy](serverless-policy-template-list.md#ami-describe-policy) | Gives permission to describe Amazon Machine Images \(AMIs\)\. | 
| [CloudFormationDescribeStacksPolicy](serverless-policy-template-list.md#cloud-formation-describe-stacks-policy) | Gives permission to describe AWS CloudFormation stacks\. | 
| [RekognitionDetectOnlyPolicy](serverless-policy-template-list.md#rekognition-detect-only-policy) | Gives permission to detect faces, labels, and text\. | 
| [RekognitionNoDataAccessPolicy](serverless-policy-template-list.md#rekognition-no-data-access-policy) | Gives permission to compare and detect faces and labels\. | 
| [RekognitionReadPolicy](serverless-policy-template-list.md#rekognition-read-policy) | Gives permission to list and search faces\. | 
| [RekognitionWriteOnlyAccessPolicy](serverless-policy-template-list.md#rekognition-write-only-access-policy) | Gives permission to create collection and index faces\. | 
| [SQSSendMessagePolicy](serverless-policy-template-list.md#sqs-send-message-policy) | Gives permission to send message to an Amazon SQS queue\. | 
| [SNSPublishMessagePolicy](serverless-policy-template-list.md#sqs-publish-message-policy) | Gives permission to publish a message to an Amazon Simple Notification Service \(Amazon SNS\) topic\. | 
| [VPCAccessPolicy](serverless-policy-template-list.md#vpc-access-policy) | Gives access to create, delete, describe, and detach elastic network interfaces\. | 
| [DynamoDBStreamReadPolicy](serverless-policy-template-list.md#dynamo-db-stream-read-policy) | Gives permission to describe and read DynamoDB streams and records\. | 
| [KinesisStreamReadPolicy](serverless-policy-template-list.md#kinesis-stream-read-policy) | Gives permission to list and read an Amazon Kinesis stream\. | 
| [SESCrudPolicy](serverless-policy-template-list.md#ses-crud-policy) | Gives permission to send email and verify identity\. | 
| [SNSCrudPolicy](serverless-policy-template-list.md#sns-crud-policy) | Gives permission to create, publish, and subscribe to Amazon SNS topics\. | 
| [KinesisCrudPolicy](serverless-policy-template-list.md#kinesis-crud-policy) | Gives permission to create, publish, and delete an Amazon Kinesis stream\. | 
| [KMSDecryptPolicy](serverless-policy-template-list.md#kms-decrypt-policy) | Gives permission to decrypt with an AWS Key Management Service \(AWS KMS\) key\. | 
| [KMSEncryptPolicy](serverless-policy-template-list.md#kms-encrypt-policy) | Gives permission to encrypt with an AWS Key Management Service \(AWS KMS\) key\. | 
| [PollyFullAccessPolicy](serverless-policy-template-list.md#polly-full-access-policy) | Gives full access permission to Amazon Polly lexicon resources\. | 
| [S3FullAccessPolicy](serverless-policy-template-list.md#s3-full-access-policy) | Gives full access permission to objects in an Amazon S3 bucket\. | 
| [CodePipelineLambdaExecutionPolicy](serverless-policy-template-list.md#code-pipeline-lambda-execution-policy) | Gives permission for a Lambda function invoked by CodePipeline to report the status of the job\. | 
| [ServerlessRepoReadWriteAccessPolicy](serverless-policy-template-list.md#serverlessrepo-read-write-access-policy) | Gives permission to create and list applications in the AWS Serverless Application Repository service\. | 
| [EC2CopyImagePolicy](serverless-policy-template-list.md#ec2-copy-image-policy) | Gives permission to copy Amazon EC2 images\. | 
| [AWSSecretsManagerRotationPolicy](serverless-policy-template-list.md#secrets-manager-rotation-policy) | Gives permission to rotate a secret in AWS Secrets Manager\. | 
| [AWSSecretsManagerGetSecretValuePolicy](serverless-policy-template-list.md#secrets-manager-get-secret-value-policy) | Gives permission to get the secret value for the specified AWS Secrets Manager secret\. | 
| [CodePipelineReadOnlyPolicy](serverless-policy-template-list.md#code-pipeline-readonly-policy) | Gives read permission to get details about a CodePipeline pipeline\. | 
| [CloudWatchDashboardPolicy](serverless-policy-template-list.md#cloudwatch-dashboard-policy) | Gives permissions to put metrics to operate on CloudWatch dashboards\. | 
| [RekognitionFacesManagementPolicy](serverless-policy-template-list.md#rekognition-face-management-policy) | Gives permission to add, delete, and search faces in an Amazon Rekognition collection\. | 
| [RekognitionFacesPolicy](serverless-policy-template-list.md#rekognition-faces-policy) | Gives permission to compare and detect faces and labels\. | 
| [RekognitionLabelsPolicy](serverless-policy-template-list.md#rekognition-labels-policy) | Gives permission to detect object and moderation labels\. | 
| [DynamoDBBackupFullAccessPolicy](serverless-policy-template-list.md#ddb-back-full-policy) | Gives read and write permission to DynamoDB on\-demand backups for a table\. | 
| [DynamoDBRestoreFromBackupPolicy](serverless-policy-template-list.md#ddb-restore-from-backup-policy) | Gives permission to restore a DynamoDB table from backup\. | 
| [ComprehendBasicAccessPolicy](serverless-policy-template-list.md#comprehend-basic-access-policy) | Gives permission for detecting entities, key phrases, languages, and sentiments\. | 
| [MobileAnalyticsWriteOnlyAccessPolicy](serverless-policy-template-list.md#mobile-analytics-write-only-access-policy) | Gives write\-only permission to put event data for all application resources\. | 
| [PinpointEndpointAccessPolicy](serverless-policy-template-list.md#pinpoint-endpoint-access-policy) | Gives permission to get and update endpoints for an Amazon Pinpoint application\. | 
| [FirehoseWritePolicy](serverless-policy-template-list.md#firehose-write-policy) | Gives permission to write to a Kinesis Data Firehose delivery stream\. | 
| [FirehoseCrudPolicy](serverless-policy-template-list.md#firehose-crud-policy) | Gives permission to create, write, update, and delete a Kinesis Data Firehose delivery stream\. | 
| [EKSDescribePolicy](serverless-policy-template-list.md#eks-describe-policy) | Gives permission to describe or list Amazon EKS clusters\. | 
| [CostExplorerReadOnlyPolicy](serverless-policy-template-list.md#cost-explorer-readonly-policy) | Gives read\-only permission to the read\-only Cost Explorer APIs for billing history\. | 
| [OrganizationsListAccountsPolicy](serverless-policy-template-list.md#organizations-list-accounts-policy) | Gives read\-only permission to list child account names and IDs\. | 
| [SESBulkTemplatedCrudPolicy](serverless-policy-template-list.md#ses-bulk-templated-crud-policy) | Gives permission to send email, templated email, templated bulk emails and verify identity\. | 
| [SESEmailTemplateCrudPolicy](serverless-policy-template-list.md#ses-email-template-crud-policy) | Gives permission to create, get, list, update and delete Amazon SES email templates\. | 
| [FilterLogEventsPolicy](serverless-policy-template-list.md#filter-log-events-policy) | Gives permission to filter CloudWatch Logs events from a specified log group\. | 
| [SSMParameterReadPolicy](serverless-policy-template-list.md#ssm-parameter-read-policy) | Gives permission to access a parameters from an Amazon EC2 Systems Manager \(SSM\) parameter store to load secrets in this account\. | 
| [StepFunctionsExecutionPolicy](serverless-policy-template-list.md#stepfunctions-execution-policy) | Gives permission to start a Step Functions state machine execution\. | 
| [CodeCommitCrudPolicy](serverless-policy-template-list.md#codecommit-crud-policy) | Gives permissions to create/read/update/delete objects within a specific CodeCommit repository\. | 
| [CodeCommitReadPolicy](serverless-policy-template-list.md#codecommit-read-policy) | Gives permissions to read objects within a specific CodeCommit repository\. | 
| [AthenaQueryPolicy](serverless-policy-template-list.md#athena-query-policy) | Gives permissions to execute Athena queries\. | 
| [TextractPolicy](serverless-policy-template-list.md#textract-policy) | Gives full access to Amazon Textract\. | 
| [TextractDetectAnalyzePolicy](serverless-policy-template-list.md#textract-detect-analyze-policy) | Gives access to detect and analyze documents with Amazon Textract\. | 
| [TextractGetResultPolicy](serverless-policy-template-list.md#textract-get-result-policy) | Gives access to get detected and analyzed documents from Amazon Textract\. | 
| [EventBridgePutEventsPolicy](serverless-policy-template-list.md#eventbridge-put-events-policy) | Gives permissions to send events to EventBridge\. | 
| [ElasticMapReduceModifyInstanceFleetPolicy](serverless-policy-template-list.md#elastic-map-reduce-modify-instance-fleet-policy) | Gives permission to list details and modify capacities for instance fleets within a cluster\. | 
| [ElasticMapReduceSetTerminationProtectionPolicy](serverless-policy-template-list.md#elastic-map-reduce-set-termination-protection-policy) | Gives permission to set termination protection for a cluster\. | 
| [ElasticMapReduceModifyInstanceGroupsPolicy](serverless-policy-template-list.md#elastic-map-reduce-modify-instance-groups-policy) | Gives permission to list details and modify settings for instance groups within a cluster\. | 
| [ElasticMapReduceCancelStepsPolicy](serverless-policy-template-list.md#elastic-map-reduce-cancel-steps-policy) | Gives permission to cancel a pending step or steps in a running cluster\. | 
| [ElasticMapReduceTerminateJobFlowsPolicy](serverless-policy-template-list.md#elastic-map-reduce-terminate-job-flows-policy) | Gives permission to shut down a cluster\. | 
| [ElasticMapReduceAddJobFlowStepsPolicy](serverless-policy-template-list.md#elastic-map-reduce-add-job-flows-policy) | Gives permission to add new steps to a running cluster\. | 
| [SageMakerCreateEndpointPolicy](serverless-policy-template-list.md#sagemaker-create-endpoint-policy) | Gives permission to create an endpoint in Amazon SageMaker\. | 
| [SageMakerCreateEndpointConfigPolicy](serverless-policy-template-list.md#sagemaker-create-endpoint-config-policy) | Gives permission to create an endpoint configuration in Amazon SageMaker\. | 
| [EcsRunTaskPolicy](serverless-policy-template-list.md#ecs-run-task-policy) | Gives permission to start a new task for a task definition\. | 
| [EFSWriteAccessPolicy](serverless-policy-template-list.md#efs-write-access-policy) | Gives permission to mount an Amazon EFS file system with write access\. | 

## Troubleshooting<a name="serverless-policy-template-troubleshooting"></a>

### SAM CLI error: "Must specify valid parameter values for policy template '<policy\-template\-name>'"<a name="serverless-policy-template-troubleshooting-"></a>

When executing `sam build`, you see the following error:

```
"Must specify valid parameter values for policy template '<policy-template-name>'"
```

This means that you did not pass an empty object when declaring a policy template that does not have any placeholder values\.

To fix this, declare the policy like the following example for [CloudWatchPutMetricPolicy](serverless-policy-template-list.md#cloudwatch-put-metric-policy)\.

```
1. MyFunction:
2.   Policies:
3.     - CloudWatchPutMetricPolicy: {}
```