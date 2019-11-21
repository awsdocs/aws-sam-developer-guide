# AWS SAM Policy Templates<a name="serverless-policy-templates"></a>

AWS SAM allows you to choose from a list of policy templates to scope the permissions of your Lambda functions to the resources that are used by your application\.

AWS SAM applications in the AWS Serverless Application Repository that use policy templates don't require any special customer acknowledgments to deploy the application from the AWS Serverless Application Repository\.

If you want to request a new policy template to be added, do the following:

1. Submit a pull request against the policy\_templates\.json source file in the `develop` branch of the AWS SAM GitHub project\. You can find the source file in [policy\_templates\.json](https://github.com/awslabs/serverless-application-model/blob/develop/samtranslator/policy_templates_data/policy_templates.json) on the GitHub website\.

1. Submit an issue in the AWS SAM GitHub project that includes the reasons for your pull request and a link to the request\. Use this link to submit a new issue: [AWS Serverless Application Model: Issues](https://github.com/awslabs/serverless-application-model/issues/new)\.

## Examples<a name="serverless-policy-template-examples"></a>

There are two AWS SAM template examples in this section: one with a policy template that includes placeholder values, and one that doesn't include placeholder values\.

### Example 1: Policy Template with Placeholder Values<a name="policy-template-example-1"></a>

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

### Example 2: Policy Template with No Placeholder Values<a name="policy-template-example-2"></a>

The following example contains the [CloudWatchPutMetricPolicy](serverless-policy-template-list.md#cloudwatch-put-metric-policy) policy template, which has no placeholder values\.

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

## Policy Template Table<a name="serverless-policy-template-table"></a>

The following is a table of the available policy templates\.


****  

| Policy Template | Description | 
| --- | --- | 
| [SQSPollerPolicy](serverless-policy-template-list.md#sqs-poller-policy) | Gives permission to poll an Amazon SQS Queue\. | 
| [LambdaInvokePolicy](serverless-policy-template-list.md#lambda-invoke-policy) | Gives permission to invoke a Lambda function, alias, or version\. | 
| [CloudWatchPutMetricPolicy](serverless-policy-template-list.md#cloudwatch-put-metric-policy) | Gives permission to put metrics to CloudWatch\. | 
| [EC2DescribePolicy](serverless-policy-template-list.md#ec2-describe-policy) | Gives permission to describe Amazon EC2 instances\. | 
| [DynamoDBCrudPolicy](serverless-policy-template-list.md#dynamo-db-crud-policy) | Gives create, read, update, and delete permissions to a DynamoDB table\. | 
| [DynamoDBReadPolicy](serverless-policy-template-list.md#dynamo-db-read-policy) | Gives read\-only permission to a DynamoDB table\. | 
| [DynamoDBReconfigurePolicy](serverless-policy-template-list.md#dynamo-db-reconfigure-policy) | Gives permission to reconfigure a DynamoDB table\. | 
| [SESSendBouncePolicy](serverless-policy-template-list.md#ses-send-bounce-policy) | Gives SendBounce permission to an Amazon SES identity\. | 
| [ElasticsearchHttpPostPolicy](serverless-policy-template-list.md#elastic-search-http-post-policy) | Gives POST permission to Amazon Elasticsearch Service\. | 
| [S3ReadPolicy](serverless-policy-template-list.md#s3-read-policy) | Gives read\-only permission to objects in an Amazon S3 bucket\. | 
| [S3CrudPolicy](serverless-policy-template-list.md#s3-crud-policy) | Gives create, read, update, and delete permission to objects in an Amazon S3 bucket\. | 
| [AMIDescribePolicy](serverless-policy-template-list.md#ami-describe-policy) | Gives permission to describe Amazon Machine Images \(AMIs\)\. | 
| [CloudFormationDescribeStacksPolicy](serverless-policy-template-list.md#cloud-formation-describe-stacks-policy) | Gives permission to describe AWS CloudFormation stacks\. | 
| [RekognitionDetectOnlyPolicy](serverless-policy-template-list.md#rekognition-detect-only-policy) | Gives permission to detect faces, labels, and text\. | 
| [RekognitionNoDataAccessPolicy](serverless-policy-template-list.md#rekognition-no-data-access-policy) | Gives permission to compare and detect faces and labels\. | 
| [RekognitionReadPolicy](serverless-policy-template-list.md#rekognition-read-policy) | Gives permission to list and search faces\. | 
| [RekognitionWriteOnlyAccessPolicy](serverless-policy-template-list.md#rekognition-write-only-access-policy) | Gives permission to create collection and index faces\. | 
| [SQSSendMessagePolicy](serverless-policy-template-list.md#sqs-send-message-policy) | Gives permission to send message to an Amazon SQS queue\. | 
| [SNSPublishMessagePolicy](serverless-policy-template-list.md#sqs-publish-message-policy) | Gives permission to publish a message to an Amazon SNS topic\. | 
| [VPCAccessPolicy](serverless-policy-template-list.md#vpc-access-policy) | Gives access to create, delete, describe, and detach Elastic Network Interfaces\. | 
| [DynamoDBStreamReadPolicy](serverless-policy-template-list.md#dynamo-db-stream-read-policy) | Gives permission to describe and read DynamoDB streams and records\. | 
| [KinesisStreamReadPolicy](serverless-policy-template-list.md#kinesis-stream-read-policy) | Gives permission to list and read an Amazon Kinesis stream\. | 
| [SESCrudPolicy](serverless-policy-template-list.md#ses-crud-policy) | Gives permission to send email and verify identity\. | 
| [SNSCrudPolicy](serverless-policy-template-list.md#sns-crud-policy) | Gives permission to create, publish, and subscribe to Amazon SNS topics\. | 
| [KinesisCrudPolicy](serverless-policy-template-list.md#kinesis-crud-policy) | Gives permission to create, publish, and delete an Amazon Kinesis stream\. | 
| [KMSDecryptPolicy](serverless-policy-template-list.md#kms-decrypt-policy) | Gives permission to decrypt with an AWS KMS key\. | 
| [PollyFullAccessPolicy](serverless-policy-template-list.md#polly-full-access-policy) | Gives full access permission to Amazon Polly lexicon resources\. | 
| [S3FullAccessPolicy](serverless-policy-template-list.md#s3-full-access-policy) | Gives full access permission to objects in an Amazon S3 bucket\. | 
| [CodePipelineLambdaExecutionPolicy](serverless-policy-template-list.md#code-pipeline-lambda-execution-policy) | Gives permission for a Lambda function invoked by CodePipeline to report the status of the job\. | 
| [ServerlessRepoReadWriteAccessPolicy](serverless-policy-template-list.md#serverlessrepo-read-write-access-policy) | Gives permission to create and list applications in the AWS Serverless Application Repository service\. | 
| [EC2CopyImagePolicy](serverless-policy-template-list.md#ec2-copy-image-policy) | Gives permission to copy Amazon EC2 images\. | 
| [AWSSecretsManagerRotationPolicy](serverless-policy-template-list.md#secrets-manager-rotation-policy) | Gives permission to rotate a secret in AWS Secrets Manager\. | 
| [AWSSecretsManagerGetSecretValuePolicy](serverless-policy-template-list.md#secrets-manager-get-secret-value-policy) | Gives permission to GetSecretValue for the specified AWS Secrets Manager secret\. | 
| [CodePipelineReadOnlyPolicy](serverless-policy-template-list.md#code-pipeline-readonly-policy) | Gives read permission to get details about a CodePipeline pipeline\. | 
| [CloudWatchDashboardPolicy](serverless-policy-template-list.md#cloudwatch-dashboard-policy) | Gives permissions to put metrics to operate on CloudWatch dashboards\. | 
| [RekognitionFacesManagementPolicy](serverless-policy-template-list.md#rekognition-face-management-policy) | Gives permission to add, delete, and search faces in a collection\. | 
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
| [FilterLogEventsPolicy](serverless-policy-template-list.md#filter-log-events-policy) | Gives permission to filter log events from a specified log group\. | 
| [SSMParameterReadPolicy](serverless-policy-template-list.md#ssm-parameter-read-policy) | Gives permission to access a parameter to load secrets in this account\. | 
| [StepFunctionsExecutionPolicy](serverless-policy-template-list.md#stepfunctions-execution-policy) | Gives permission to access a parameter to load secrets in this account\. | 
| [CodeCommitCrudPolicy](serverless-policy-template-list.md#codecommit-crud-policy) | Gives permissions to create/read/update/delete objects within a specific codecommit repository\. | 
| [CodeCommitReadPolicy](serverless-policy-template-list.md#codecommit-read-policy) | Gives permissions to read objects within a specific codecommit repository\. | 