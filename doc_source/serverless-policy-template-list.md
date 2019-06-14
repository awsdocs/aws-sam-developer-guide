# Policy Template List<a name="serverless-policy-template-list"></a>

The following are the available policy templates, along with the permissions that are applied to each one\. AWS SAM automatically populates the placeholder items \(such as AWS Region and account ID\) with the appropriate information\.

## SQSPollerPolicy<a name="sqs-poller-policy"></a>

Gives permission to poll an Amazon SQS Queue\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "sqs:ChangeMessageVisibility",
              "sqs:ChangeMessageVisibilityBatch",
              "sqs:DeleteMessage",
              "sqs:DeleteMessageBatch",
              "sqs:GetQueueAttributes",
              "sqs:ReceiveMessage"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:sqs:${AWS::Region}:${AWS::AccountId}:${queueName}",
                {
                  "queueName": {
                    "Ref": "QueueName"
                  }
                }
              ]
            }
          }
        ]
```

## LambdaInvokePolicy<a name="lambda-invoke-policy"></a>

Gives permission to invoke a Lambda function, alias, or version\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "lambda:InvokeFunction"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:lambda:${AWS::Region}:${AWS::AccountId}:function:${functionName}*",
                {
                  "functionName": {
                    "Ref": "FunctionName"
                  }
                }
              ]
            }
          }
        ]
```

## CloudWatchPutMetricPolicy<a name="cloudwatch-put-metric-policy"></a>

Gives permission to put metrics to CloudWatch\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "cloudwatch:PutMetricData"
            ],
            "Resource": "*"
          }
        ]
```

## EC2DescribePolicy<a name="ec2-describe-policy"></a>

Gives permission to describe Amazon EC2 instances\.

```
         "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ec2:DescribeRegions",
              "ec2:DescribeInstances"
            ],
            "Resource": "*"
          }
        ]
```

## DynamoDBCrudPolicy<a name="dynamo-db-crud-policy"></a>

Gives create, read, update, and delete permissions to a DynamoDB table\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "dynamodb:GetItem",
              "dynamodb:DeleteItem",
              "dynamodb:PutItem",
              "dynamodb:Scan",
              "dynamodb:Query",
              "dynamodb:UpdateItem",
              "dynamodb:BatchWriteItem",
              "dynamodb:BatchGetItem",
              "dynamodb:DescribeTable"
            ],
            "Resource": [
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}",
                  {
                    "tableName": {
                      "Ref": "TableName"
                    }
                  }
                ]
              },
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}/index/*",
                  {
                    "tableName": {
                      "Ref": "TableName"
                    }
                  }
                ]
              }
            ]
          }
        ]
```

## DynamoDBReadPolicy<a name="dynamo-db-read-policy"></a>

Gives read\-only permission to a DynamoDB table\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "dynamodb:GetItem",
              "dynamodb:Scan",
              "dynamodb:Query",
              "dynamodb:BatchGetItem",
              "dynamodb:DescribeTable"
            ],
            "Resource": [
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}",
                  {
                    "tableName": {
                      "Ref": "TableName"
                    }
                  }
                ]
              },
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}/index/*",
                  {
                    "tableName": {
                      "Ref": "TableName"
                    }
                  }
                ]
              }
            ]
          }
        ]
```

## DynamoDBReconfigurePolicy<a name="dynamo-db-reconfigure-policy"></a>

Gives permission to reconfigure a DynamoDB table\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "dynamodb:UpdateTable"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}",
                {
                  "tableName": {
                    "Ref": "TableName"
                  }
                }
              ]
            }
          }
        ]
```

## SESSendBouncePolicy<a name="ses-send-bounce-policy"></a>

Gives SendBounce permission to an Amazon SES identity\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ses:SendBounce"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:ses:${AWS::Region}:${AWS::AccountId}:identity/${identityName}",
                {
                  "identityName": {
                    "Ref": "IdentityName"
                  }
                }
              ]
            }
          }
        ]
```

## ElasticsearchHttpPostPolicy<a name="elastic-search-http-post-policy"></a>

Gives POST permission to Amazon Elasticsearch Service\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "es:ESHttpPost"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:es:${AWS::Region}:${AWS::AccountId}:domain/${domainName}",
                {
                  "domainName": {
                    "Ref": "DomainName"
                  }
                }
              ]
            }
          }
        ]
```

## S3ReadPolicy<a name="s3-read-policy"></a>

Gives read\-only permission to objects in an Amazon S3 bucket\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "s3:GetObject",
              "s3:ListBucket",
              "s3:GetBucketLocation",
              "s3:GetObjectVersion",
              "s3:GetLifecycleConfiguration"
            ],
            "Resource": [
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:s3:::${bucketName}",
                  {
                    "bucketName": {
                      "Ref": "BucketName"
                    }
                  }
                ]
              },
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:s3:::${bucketName}/*",
                  {
                    "bucketName": {
                      "Ref": "BucketName"
                    }
                  }
                ]
              }
            ]
          }
        ]
```

## S3CrudPolicy<a name="s3-crud-policy"></a>

Gives create, read, update, and delete permission to objects in an Amazon S3 bucket\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "s3:GetObject",
              "s3:ListBucket",
              "s3:GetBucketLocation",
              "s3:GetObjectVersion",
              "s3:PutObject",
              "s3:PutObjectAcl",
              "s3:GetLifecycleConfiguration",
              "s3:PutLifecycleConfiguration",
              "s3:DeleteObject"
            ],
            "Resource": [
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:s3:::${bucketName}",
                  {
                    "bucketName": {
                      "Ref": "BucketName"
                    }
                  }
                ]
              },
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:s3:::${bucketName}/*",
                  {
                    "bucketName": {
                      "Ref": "BucketName"
                    }
                  }
                ]
              }
            ]
          }
        ]
```

## AMIDescribePolicy<a name="ami-describe-policy"></a>

Gives permission to describe Amazon Machine Images \(AMIs\)\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ec2:DescribeImages"
            ],
            "Resource": {
              "Fn::Sub": "arn:${AWS::Partition}:ec2:${AWS::Region}:${AWS::AccountId}:image/*"
            }
          }
        ]
```

## CloudFormationDescribeStacksPolicy<a name="cloud-formation-describe-stacks-policy"></a>

Gives permission to describe AWS CloudFormation stacks\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "cloudformation:DescribeStacks"
            ],
            "Resource": {
              "Fn::Sub": "arn:${AWS::Partition}:cloudformation:${AWS::Region}:${AWS::AccountId}:stack/*"
            }
          }
        ]
```

## RekognitionDetectOnlyPolicy<a name="rekognition-detect-only-policy"></a>

Gives permission to detect faces, labels, and text\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "rekognition:DetectFaces",
              "rekognition:DetectLabels",
              "rekognition:DetectModerationLabels",
              "rekognition:DetectText"
            ],
            "Resource": "*"
          }
        ]
```

## RekognitionNoDataAccessPolicy<a name="rekognition-no-data-access-policy"></a>

Gives permission to compare and detect faces and labels\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "rekognition:CompareFaces",
              "rekognition:DetectFaces",
              "rekognition:DetectLabels",
              "rekognition:DetectModerationLabels"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:rekognition:${AWS::Region}:${AWS::AccountId}:collection/${collectionId}",
                {
                  "collectionId": {
                    "Ref": "CollectionId"
                  }
                }
              ]
            }
          }
        ]
```

## RekognitionReadPolicy<a name="rekognition-read-policy"></a>

Gives permission to list and search faces\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "rekognition:ListCollections",
              "rekognition:ListFaces",
              "rekognition:SearchFaces",
              "rekognition:SearchFacesByImage"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:rekognition:${AWS::Region}:${AWS::AccountId}:collection/${collectionId}",
                {
                  "collectionId": {
                    "Ref": "CollectionId"
                  }
                }
              ]
            }
          }
        ]
```

## RekognitionWriteOnlyAccessPolicy<a name="rekognition-write-only-access-policy"></a>

Gives permission to create collection and index faces\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "rekognition:CreateCollection",
              "rekognition:IndexFaces"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:rekognition:${AWS::Region}:${AWS::AccountId}:collection/${collectionId}",
                {
                  "collectionId": {
                    "Ref": "CollectionId"
                  }
                }
              ]
            }
          }
        ]
```

## SQSSendMessagePolicy<a name="sqs-send-message-policy"></a>

Gives permission to send message to an Amazon SQS queue\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "sqs:SendMessage*"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:sqs:${AWS::Region}:${AWS::AccountId}:${queueName}",
                {
                  "queueName": {
                    "Ref": "QueueName"
                  }
                }
              ]
            }
          }
        ]
```

## SNSPublishMessagePolicy<a name="sqs-publish-message-policy"></a>

Gives permission to publish a message to an Amazon SNS topic\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "sns:Publish"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:sns:${AWS::Region}:${AWS::AccountId}:${topicName}",
                {
                  "topicName": {
                    "Ref": "TopicName"
                  }
                }
              ]
            }
          }
        ]
```

## VPCAccessPolicy<a name="vpc-access-policy"></a>

Gives access to create, delete, describe, and detach Elastic Network Interfaces\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ec2:CreateNetworkInterface",
              "ec2:DeleteNetworkInterface",
              "ec2:DescribeNetworkInterfaces",
              "ec2:DetachNetworkInterface"
            ],
            "Resource": "*"
          }
        ]
```

## DynamoDBStreamReadPolicy<a name="dynamo-db-stream-read-policy"></a>

Gives permission to describe and read DynamoDB streams and records\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "dynamodb:DescribeStream",
              "dynamodb:GetRecords",
              "dynamodb:GetShardIterator",
              "dynamodb:ListStreams"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}/${streamName}",
                {
                  "tableName": {
                    "Ref": "TableName"
                  },
                  "streamName": {
                    "Ref": "StreamName"
                  }
                }
              ]
            }
          }
        ]
```

## KinesisStreamReadPolicy<a name="kinesis-stream-read-policy"></a>

Gives permission to list and read an Amazon Kinesis stream\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "kinesis:ListStreams",
              "kinesis:DescribeLimits"
            ],
            "Resource": {
              "Fn::Sub": "arn:${AWS::Partition}:kinesis:${AWS::Region}:${AWS::AccountId}:stream/*"
            }
          },
          {
            "Effect": "Allow",
            "Action": [
              "kinesis:DescribeStream",
              "kinesis:GetRecords",
              "kinesis:GetShardIterator"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:kinesis:${AWS::Region}:${AWS::AccountId}:stream/${streamName}",
                {
                  "streamName": {
                    "Ref": "StreamName"
                  }
                }
              ]
            }
          }
        ]
```

## SESCrudPolicy<a name="ses-crud-policy"></a>

Gives permission to send email and verify identity\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ses:GetIdentityVerificationAttributes",
              "ses:SendEmail",
              "ses:VerifyEmailIdentity"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:ses:${AWS::Region}:${AWS::AccountId}:identity/${identityName}",
                {
                  "identityName": {
                    "Ref": "IdentityName"
                  }
                }
              ]
            }
          }
        ]
```

## SNSCrudPolicy<a name="sns-crud-policy"></a>

Gives permission to create, publish, and subscribe to Amazon SNS topics\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "sns:ListSubscriptionsByTopic",
              "sns:CreateTopic",
              "sns:SetTopicAttributes",
              "sns:Subscribe",
              "sns:Publish"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:sns:${AWS::Region}:${AWS::AccountId}:${topicName}*",
                {
                  "topicName": {
                    "Ref": "TopicName"
                  }
                }
              ]
            }
          }
        ]
```

## KinesisCrudPolicy<a name="kinesis-crud-policy"></a>

Gives permission to create, publish, and delete an Amazon Kinesis stream\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "kinesis:AddTagsToStream",
              "kinesis:CreateStream",
              "kinesis:DecreaseStreamRetentionPeriod",
              "kinesis:DeleteStream",
              "kinesis:DescribeStream",
              "kinesis:GetShardIterator",
              "kinesis:IncreaseStreamRetentionPeriod",
              "kinesis:ListTagsForStream",
              "kinesis:MergeShards",
              "kinesis:PutRecord",
              "kinesis:PutRecords",
              "kinesis:SplitShard",
              "kinesis:RemoveTagsFromStream"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:kinesis:${AWS::Region}:${AWS::AccountId}:stream/${streamName}",
                {
                  "streamName": {
                    "Ref": "StreamName"
                  }
                }
              ]
            }
          }
        ]
```

## KMSDecryptPolicy<a name="kms-decrypt-policy"></a>

Gives permission to decrypt with an AWS KMS key\.

```
        "Statement": [
          {
            "Action": "kms:Decrypt",
            "Effect": "Allow",
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:kms:${AWS::Region}:${AWS::AccountId}:key/${keyId}",
                {
                  "keyId": {
                    "Ref": "KeyId"
                  }
                }
              ]
            }
          }
        ]
```

## PollyFullAccessPolicy<a name="polly-full-access-policy"></a>

Gives full access permission to Amazon Polly lexicon resources\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "polly:GetLexicon",
              "polly:DeleteLexicon"
            ],
            "Resource": [
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:polly:${AWS::Region}:${AWS::AccountId}:lexicon/${lexiconName}",
                  {
                    "lexiconName": {
                      "Ref": "LexiconName"
                    }
                  }
                ]
              }
            ]
          },
          {
            "Effect": "Allow",
            "Action": [
              "polly:DescribeVoices",
              "polly:ListLexicons",
              "polly:PutLexicon",
              "polly:SynthesizeSpeech"
            ],
            "Resource": [
              {
                "Fn::Sub": "arn:${AWS::Partition}:polly:${AWS::Region}:${AWS::AccountId}:lexicon/*"
              }
            ]
          }
        ]
```

## S3FullAccessPolicy<a name="s3-full-access-policy"></a>

Gives full access permission to objects in an Amazon S3 bucket\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "s3:GetObject",
              "s3:GetObjectAcl",
              "s3:GetObjectVersion",
              "s3:PutObject",
              "s3:PutObjectAcl",
              "s3:DeleteObject"
            ],
            "Resource": [
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:s3:::${bucketName}/*",
                  {
                    "bucketName": {
                      "Ref": "BucketName"
                    }
                  }
                ]
              }
            ]
          },
          {
            "Effect": "Allow",
            "Action": [
              "s3:ListBucket",
              "s3:GetBucketLocation",
              "s3:GetLifecycleConfiguration",
              "s3:PutLifecycleConfiguration"
            ],
            "Resource": [
              {
                "Fn::Sub": [
                  "arn:${AWS::Partition}:s3:::${bucketName}",
                  {
                    "bucketName": {
                      "Ref": "BucketName"
                    }
                  }
                ]
              }
            ]
          }
        ]
```

## CodePipelineLambdaExecutionPolicy<a name="code-pipeline-lambda-execution-policy"></a>

Gives permission for a Lambda function invoked by CodePipeline to report the status of the job\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "codepipeline:PutJobSuccessResult",
              "codepipeline:PutJobFailureResult"
            ],
            "Resource": "*"
          }
        ]
```

## ServerlessRepoReadWriteAccessPolicy<a name="serverlessrepo-read-write-access-policy"></a>

Gives permission to create and list applications in the AWS Serverless Application Repository service\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "serverlessrepo:CreateApplication",
              "serverlessrepo:CreateApplicationVersion",
              "serverlessrepo:GetApplication",
              "serverlessrepo:ListApplications",
              "serverlessrepo:ListApplicationVersions"
            ],
            "Resource": [
              {
                "Fn::Sub": "arn:${AWS::Partition}:serverlessrepo:${AWS::Region}:${AWS::AccountId}:applications/*"
              }
            ]
          }
        ]
```

## EC2CopyImagePolicy<a name="ec2-copy-image-policy"></a>

Gives permission to copy Amazon EC2 images\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ec2:CopyImage"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:ec2:${AWS::Region}:${AWS::AccountId}:image/${imageId}",
                {
                  "imageId": {
                    "Ref": "ImageId"
                  }
                }
              ]
            }
          }
        ]
```

## AWSSecretsManagerRotationPolicy<a name="secrets-manager-rotation-policy"></a>

Gives permission to rotate a secret in AWS Secrets Manager\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "secretsmanager:DescribeSecret",
              "secretsmanager:GetSecretValue",
              "secretsmanager:PutSecretValue",
              "secretsmanager:UpdateSecretVersionStage"
            ],
            "Resource": {
              "Fn::Sub": "arn:${AWS::Partition}:secretsmanager:${AWS::Region}:${AWS::AccountId}:secret:*"
            },
            "Condition": {
              "StringEquals": {
                "secretsmanager:resource/AllowRotationLambdaArn": {
                  "Fn::Sub": [
                    "arn:${AWS::Partition}:lambda:${AWS::Region}:${AWS::AccountId}:function:${functionName}",
                    {
                      "functionName": {
                        "Ref": "FunctionName"
                      }
                    }
                  ]
                }
              }
            }
          },
          {
            "Effect": "Allow",
            "Action": [
              "secretsmanager:GetRandomPassword"
            ],
            "Resource": "*"
          }
        ]
```

## AWSSecretsManagerGetSecretValuePolicy<a name="secrets-manager-get-secret-value-policy"></a>

Gives permission to GetSecretValue for the specified AWS Secrets Manager secret\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "secretsmanager:GetSecretValue"
            ],
            "Resource": {
              "Fn::Sub": [
                "${secretArn}",
                {
                  "secretArn": {
                    "Ref": "SecretArn"
                  }
                }
              ]
            }
          }
        ]
```

## CodePipelineReadOnlyPolicy<a name="code-pipeline-readonly-policy"></a>

Gives read permission to get details about a CodePipeline pipeline\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "cloudwatch:GetDashboard",
              "cloudwatch:ListDashboards",
              "cloudwatch:PutDashboard",
              "cloudwatch:ListMetrics"
            ],
            "Resource": "*"
          }
        ]
```

## RekognitionFacesPolicy<a name="rekognition-faces-policy"></a>

Gives permission to compare and detect faces and labels\.

```
        "Statement": [{
          "Effect": "Allow",
          "Action": [
            "rekognition:CompareFaces",
            "rekognition:DetectFaces"
          ],
          "Resource": {
            "Fn::Sub": [
              "arn:${AWS::Partition}:rekognition:${AWS::Region}:${AWS::AccountId}:collection/${collectionId}",
              {
                "collectionId": {
                  "Ref": "CollectionId"
                }
              }
            ]
          }
        ]
```

## RekognitionLabelsPolicy<a name="rekognition-labels-policy"></a>

Gives permission to detect object and moderation labels\.

```
        "Statement": [{
          "Effect": "Allow",
          "Action": [
            "rekognition:DetectLabels",
            "rekognition:DetectModerationLabels"
          ],
          "Resource": "*"
         }
        ]
```

## DynamoDBBackupFullAccessPolicy<a name="ddb-back-full-policy"></a>

Gives read and write permission to DynamoDB on\-demand backups for a table\.

```
        "Statement": [{
          "Effect": "Allow",
          "Action": [
            "dynamodb:CreateBackup",
            "dynamodb:DescribeContinuousBackups"
          ],
          "Resource": {
            "Fn::Sub": [
              "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}",
              {
                "tableName": {
                  "Ref": "TableName"
                }
              }
            ]
          }
        },
          {
            "Effect": "Allow",
            "Action": [
              "dynamodb:DeleteBackup",
              "dynamodb:DescribeBackup",
              "dynamodb:ListBackups"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}/backup/*",
                {
                  "tableName": {
                    "Ref": "TableName"
                  }
                }
              ]
            }
          }
        ]
```

## DynamoDBRestoreFromBackupPolicy<a name="ddb-restore-from-backup-policy"></a>

Gives permission to restore a DynamoDB table from backup\.

```
        "Statement": [{
          "Effect": "Allow",
          "Action": [
            "dynamodb:RestoreTableFromBackup"
          ],
          "Resource": {
            "Fn::Sub": [
              "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}/backup/*",
              {
                "tableName": {
                  "Ref": "TableName"
                }
              }
            ]
          }
        },
          {
            "Effect": "Allow",
            "Action": [
              "dynamodb:PutItem",
              "dynamodb:UpdateItem",
              "dynamodb:DeleteItem",
              "dynamodb:GetItem",
              "dynamodb:Query",
              "dynamodb:Scan",
              "dynamodb:BatchWriteItem"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}",
                {
                  "tableName": {
                    "Ref": "TableName"
                  }
                }
              ]
            }
          }
        ]
```

## ComprehendBasicAccessPolicy<a name="comprehend-basic-access-policy"></a>

Gives permission for detecting entities, key phrases, languages, and sentiments\.

```
        "Statement": [{
          "Effect": "Allow",
          "Action": [
            "comprehend:BatchDetectKeyPhrases",
            "comprehend:DetectDominantLanguage",
            "comprehend:DetectEntities",
            "comprehend:BatchDetectEntities",
            "comprehend:DetectKeyPhrases",
            "comprehend:DetectSentiment",
            "comprehend:BatchDetectDominantLanguage",
            "comprehend:BatchDetectSentiment"
          ],
          "Resource": "*"
          }
        ]
```

## MobileAnalyticsWriteOnlyAccessPolicy<a name="mobile-analytics-write-only-access-policy"></a>

Gives write\-only permission to put event data for all application resources\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "mobileanalytics:PutEvents"
            ],
            "Resource": "*"
          }
        ]
```

## PinpointEndpointAccessPolicy<a name="pinpoint-endpoint-access-policy"></a>

Gives permission to get and update endpoints for an Amazon Pinpoint application\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "mobiletargeting:GetEndpoint",
              "mobiletargeting:UpdateEndpoint",
              "mobiletargeting:UpdateEndpointsBatch"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:mobiletargeting:${AWS::Region}:${AWS::AccountId}:apps/${pinpointApplicationId}/endpoints/*",
                {
                  "pinpointApplicationId": {
                    "Ref": "PinpointApplicationId"
                  }
                }
              ]
            }
          }
        ]
```

## FirehoseWritePolicy<a name="firehose-write-policy"></a>

Gives permission to write to a Kinesis Data Firehose delivery stream\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "firehose:PutRecord",
              "firehose:PutRecordBatch"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:firehose:${AWS::Region}:${AWS::AccountId}:deliverystream/${deliveryStreamName}",
                {
                  "deliveryStreamName": {
                    "Ref": "DeliveryStreamName"
                  }
                }
              ]
            }
          }
        ]
```

## FirehoseCrudPolicy<a name="firehose-crud-policy"></a>

Gives permission to create, write, update, and delete a Kinesis Data Firehose delivery stream\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "firehose:CreateDeliveryStream",
              "firehose:DeleteDeliveryStream",
              "firehose:DescribeDeliveryStream",
              "firehose:PutRecord",
              "firehose:PutRecordBatch",
              "firehose:UpdateDestination"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:firehose:${AWS::Region}:${AWS::AccountId}:deliverystream/${deliveryStreamName}",
                {
                  "deliveryStreamName": {
                    "Ref": "DeliveryStreamName"
                  }
                }
              ]
            }
          }
        ]
```

## EKSDescribePolicy<a name="eks-describe-policy"></a>

Gives permission to describe or list Amazon EKS clusters\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "eks:DescribeCluster",
              "eks:ListClusters"
            ],
            "Resource": "*"
          }
        ]
```

## CostExplorerReadOnlyPolicy<a name="cost-explorer-readonly-policy"></a>

Gives read\-only permission to the read\-only Cost Explorer APIs for billing history\.

```
        "Statement": [{
          "Effect": "Allow",
          "Action": [
            "ce:GetCostAndUsage",
            "ce:GetDimensionValues",
            "ce:GetReservationCoverage",
            "ce:GetReservationPurchaseRecommendation",
            "ce:GetReservationUtilization",
            "ce:GetTags"
          ],
          "Resource": "*"
        }]
```

## OrganizationsListAccountsPolicy<a name="organizations-list-accounts-policy"></a>

Gives read\-only permission to list child account names and IDs\.

```
        "Statement": [{
          "Effect": "Allow",
          "Action": [
            "organizations:ListAccounts"
          ],
          "Resource": "*"
        }]
```

## SESBulkTemplatedCrudPolicy<a name="ses-bulk-templated-crud-policy"></a>

Gives permission to send email, templated email, templated bulk emails and verify identity\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ses:GetIdentityVerificationAttributes",
              "ses:SendEmail",
              "ses:SendRawEmail",
              "ses:SendTemplatedEmail",
              "ses:SendBulkTemplatedEmail",
              "ses:VerifyEmailIdentity"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:ses:${AWS::Region}:${AWS::AccountId}:identity/${identityName}",
                {
                  "identityName": {
                    "Ref": "IdentityName"
                  }
                }
              ]
            }
          }
       ]
```

## SESEmailTemplateCrudPolicy<a name="ses-email-template-crud-policy"></a>

Gives permission to create, get, list, update and delete Amazon SES email templates\.

```
        "Statement": [{
          "Effect": "Allow",
          "Action": [
            "ses:CreateTemplate",
            "ses:GetTemplate",
            "ses:ListTemplates",
            "ses:UpdateTemplate",
            "ses:DeleteTemplate",
            "ses:TestRenderTemplate"
          ],
          "Resource": "*"
        }]
```

## FilterLogEventsPolicy<a name="filter-log-events-policy"></a>

Gives permission to filter log events from a specified log group\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "logs:FilterLogEvents"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:logs:${AWS::Region}:${AWS::AccountId}:log-group:${logGroupName}:log-stream:*",
                {
                  "logGroupName": {
                    "Ref": "LogGroupName"
                  }
                }
              ]
            }
          }
        ]
```

## SSMParameterReadPolicy<a name="ssm-parameter-read-policy"></a>

Gives permission to access a parameter to load secrets in this account\.

**Note**  
If you are not using default key, you will also need `KMSDecryptPolicy`\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ssm:DescribeParameters"
            ],
            "Resource": "*"
          },
          {
            "Effect": "Allow",
            "Action": [
              "ssm:GetParameters",
              "ssm:GetParameter"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:ssm:${AWS::Region}:${AWS::AccountId}:parameter/${parameterName}",
                {
                  "parameterName": {
                    "Ref": "ParameterName"
                  }
                }
              ]
            }
          }
        ]
```