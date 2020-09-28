# Policy template list<a name="serverless-policy-template-list"></a>

The following are the available policy templates, along with the permissions that are applied to each one\. AWS Serverless Application Model \(AWS SAM\) automatically populates the placeholder items \(such as AWS Region and account ID\) with the appropriate information\.

## SQSPollerPolicy<a name="sqs-poller-policy"></a>

Gives permission to poll an Amazon Simple Queue Service \(Amazon SQS\) queue\.

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

Gives permission to invoke an AWS Lambda function, alias, or version\.

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

## CloudWatchDescribeAlarmHistoryPolicy<a name="cloudwatch-describe-alarm-history-policy"></a>

Gives permission to describe Amazon CloudWatch alarm history\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "cloudwatch:DescribeAlarmHistory"
            ],
            "Resource": "*"
          }
        ]
```

## CloudWatchPutMetricPolicy<a name="cloudwatch-put-metric-policy"></a>

Gives permission to send metrics to CloudWatch\.

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

Gives permission to describe Amazon Elastic Compute Cloud \(Amazon EC2\) instances\.

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

Gives create, read, update, and delete permissions to an Amazon DynamoDB table\.

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
              "dynamodb:DescribeTable",
              "dynamodb:ConditionCheckItem"
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

## DynamoDBWritePolicy<a name="dynamo-db-write-policy"></a>

Gives write\-only permission to a DynamoDB table\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "dynamodb:PutItem",
              "dynamodb:UpdateItem",
              "dynamodb:BatchWriteItem"
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

Gives SendBounce permission to an Amazon Simple Email Service \(Amazon SES\) identity\.

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

Gives POST and PUT permission to Amazon Elasticsearch Service\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "es:ESHttpPost",
              "es:ESHttpPut"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:es:${AWS::Region}:${AWS::AccountId}:domain/${domainName}/*",
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

Gives read\-only permission to objects in an Amazon Simple Storage Service \(Amazon S3\) bucket\.

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

## S3WritePolicy<a name="s3-write-policy"></a>

Gives write permission to objects in an Amazon S3 bucket\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "s3:PutObject",
              "s3:PutObjectAcl",
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

Gives permission to publish a message to an Amazon Simple Notification Service \(Amazon SNS\) topic\.

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

Gives access to create, delete, describe, and detach elastic network interfaces\.

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
              "dynamodb:GetShardIterator"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}/stream/${streamName}",
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
          },
         {
            "Effect": "Allow",
            "Action": [
              "dynamodb:ListStreams"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:dynamodb:${AWS::Region}:${AWS::AccountId}:table/${tableName}/stream/*",
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
              "kinesis:DescribeStreamSummary",
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
              "ses:SendRawEmail",
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
              "kinesis:DescribeStreamSummary",
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

Gives permission to decrypt with an AWS Key Management Service \(AWS KMS\) key\.

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

## KMSEncryptPolicy<a name="kms-encrypt-policy"></a>

Gives permission to encrypt with an AWS KMS key\.

```
        "Statement": [
          {
            "Action": "kms:Encrypt",
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
              "s3:DeleteObject",
              "s3:DeleteObjectTagging",
              "s3:DeleteObjectVersionTagging",
              "s3:GetObjectTagging",
              "s3:GetObjectVersionTagging",
              "s3:PutObjectTagging",
              "s3:PutObjectVersionTagging"
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

Gives permission for a Lambda function invoked by AWS CodePipeline to report the status of the job\.

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

Gives permission to create and list applications in the AWS Serverless Application Repository \(AWS SAM\) service\.

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

Gives permission to get the secret value for the specified AWS Secrets Manager secret\.

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
              "codepipeline:ListPipelineExecutions"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:codepipeline:${AWS::Region}:${AWS::AccountId}:${pipelinename}",
                {
                  "pipelinename": {
                    "Ref": "PipelineName"
                  }
                }
              ]
            }
          }
        ]
```

## CloudWatchDashboardPolicy<a name="cloudwatch-dashboard-policy"></a>

Gives permissions to put metrics to operate on CloudWatch dashboards\.

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

## RekognitionFacesManagementPolicy<a name="rekognition-face-management-policy"></a>

Gives permission to add, delete, and search faces in an Amazon Rekognition collection\.

```
        "Statement": [{
          "Effect": "Allow",
          "Action": [
            "rekognition:IndexFaces",
            "rekognition:DeleteFaces",
            "rekognition:SearchFaces",
            "rekognition:SearchFacesByImage",
            "rekognition:ListFaces"
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

## RekognitionFacesPolicy<a name="rekognition-faces-policy"></a>

Gives permission to compare and detect faces and labels\.

```
        "Statement": [{
          "Effect": "Allow",
          "Action": [
            "rekognition:CompareFaces",
            "rekognition:DetectFaces"
          ],
          "Resource": "*"
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

Gives permission to describe or list Amazon Elastic Kubernetes Service \(Amazon EKS\) clusters\.

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

Gives read\-only permission to the read\-only AWS Cost Explorer \(Cost Explorer\) APIs for billing history\.

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

Gives permission to send Amazon SES email, templated email, and templated bulk emails and to verify identity\.

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

Gives permission to create, get, list, update, and delete Amazon SES email templates\.

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

Gives permission to filter CloudWatch Logs events from a specified log group\.

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

Gives permission to access a parameters from an Amazon EC2 Systems Manager \(SSM\) parameter store to load secrets in this account\.

**Note**  
If you are not using default key, you will also need the `KMSDecryptPolicy` policy\.

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
              "ssm:GetParameter",
              "ssm:GetParametersByPath"
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

## StepFunctionsExecutionPolicy<a name="stepfunctions-execution-policy"></a>

Gives permission to start a Step Functions state machine execution\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "states:StartExecution"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:states:${AWS::Region}:${AWS::AccountId}:stateMachine:${stateMachineName}",
                {
                  "stateMachineName": {
                    "Ref": "StateMachineName"
                  }
                }
              ]
            }
          }
        ]
```

## CodeCommitCrudPolicy<a name="codecommit-crud-policy"></a>

Gives permissions to create, read, update, and delete objects within a specific CodeCommit repository\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "codecommit:GitPull",
              "codecommit:GitPush",
              "codecommit:CreateBranch",
              "codecommit:DeleteBranch",
              "codecommit:GetBranch",
              "codecommit:ListBranches",
              "codecommit:MergeBranchesByFastForward",
              "codecommit:MergeBranchesBySquash",
              "codecommit:MergeBranchesByThreeWay",
              "codecommit:UpdateDefaultBranch",
              "codecommit:BatchDescribeMergeConflicts",
              "codecommit:CreateUnreferencedMergeCommit",
              "codecommit:DescribeMergeConflicts",
              "codecommit:GetMergeCommit",
              "codecommit:GetMergeOptions",
              "codecommit:BatchGetPullRequests",
              "codecommit:CreatePullRequest",
              "codecommit:DescribePullRequestEvents",
              "codecommit:GetCommentsForPullRequest",
              "codecommit:GetCommitsFromMergeBase",
              "codecommit:GetMergeConflicts",
              "codecommit:GetPullRequest",
              "codecommit:ListPullRequests",
              "codecommit:MergePullRequestByFastForward",
              "codecommit:MergePullRequestBySquash",
              "codecommit:MergePullRequestByThreeWay",
              "codecommit:PostCommentForPullRequest",
              "codecommit:UpdatePullRequestDescription",
              "codecommit:UpdatePullRequestStatus",
              "codecommit:UpdatePullRequestTitle",
              "codecommit:DeleteFile",
              "codecommit:GetBlob",
              "codecommit:GetFile",
              "codecommit:GetFolder",
              "codecommit:PutFile",
              "codecommit:DeleteCommentContent",
              "codecommit:GetComment",
              "codecommit:GetCommentsForComparedCommit",
              "codecommit:PostCommentForComparedCommit",
              "codecommit:PostCommentReply",
              "codecommit:UpdateComment",
              "codecommit:BatchGetCommits",
              "codecommit:CreateCommit",
              "codecommit:GetCommit",
              "codecommit:GetCommitHistory",
              "codecommit:GetDifferences",
              "codecommit:GetObjectIdentifier",
              "codecommit:GetReferences",
              "codecommit:GetTree",
              "codecommit:GetRepository",
              "codecommit:UpdateRepositoryDescription",
              "codecommit:ListTagsForResource",
              "codecommit:TagResource",
              "codecommit:UntagResource",
              "codecommit:GetRepositoryTriggers",
              "codecommit:PutRepositoryTriggers",
              "codecommit:TestRepositoryTriggers",
              "codecommit:GetBranch",
              "codecommit:GetCommit",
              "codecommit:UploadArchive",
              "codecommit:GetUploadArchiveStatus",
              "codecommit:CancelUploadArchive"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:codecommit:${AWS::Region}:${AWS::AccountId}:${repositoryName}",
                {
                  "repositoryName": {
                    "Ref": "RepositoryName"
                  }
                }
              ]
            }
          }
        ]
```

## CodeCommitReadPolicy<a name="codecommit-read-policy"></a>

Gives permissions to read objects within a specific CodeCommit repository\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "codecommit:GitPull",
              "codecommit:GetBranch",
              "codecommit:ListBranches",
              "codecommit:BatchDescribeMergeConflicts",
              "codecommit:DescribeMergeConflicts",
              "codecommit:GetMergeCommit",
              "codecommit:GetMergeOptions",
              "codecommit:BatchGetPullRequests",
              "codecommit:DescribePullRequestEvents",
              "codecommit:GetCommentsForPullRequest",
              "codecommit:GetCommitsFromMergeBase",
              "codecommit:GetMergeConflicts",
              "codecommit:GetPullRequest",
              "codecommit:ListPullRequests",
              "codecommit:GetBlob",
              "codecommit:GetFile",
              "codecommit:GetFolder",
              "codecommit:GetComment",
              "codecommit:GetCommentsForComparedCommit",
              "codecommit:BatchGetCommits",
              "codecommit:GetCommit",
              "codecommit:GetCommitHistory",
              "codecommit:GetDifferences",
              "codecommit:GetObjectIdentifier",
              "codecommit:GetReferences",
              "codecommit:GetTree",
              "codecommit:GetRepository",
              "codecommit:ListTagsForResource",
              "codecommit:GetRepositoryTriggers",
              "codecommit:TestRepositoryTriggers",
              "codecommit:GetBranch",
              "codecommit:GetCommit",
              "codecommit:GetUploadArchiveStatus"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:codecommit:${AWS::Region}:${AWS::AccountId}:${repositoryName}",
                {
                  "repositoryName": {
                    "Ref": "RepositoryName"
                  }
                }
              ]
            }
          }
        ]
```

## AthenaQueryPolicy<a name="athena-query-policy"></a>

Gives permissions to execute Athena queries\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "athena:ListWorkGroups",
              "athena:GetExecutionEngine",
              "athena:GetExecutionEngines",
              "athena:GetNamespace",
              "athena:GetCatalogs",
              "athena:GetNamespaces",
              "athena:GetTables",
              "athena:GetTable"
            ],
            "Resource": "*"
          },
          {
            "Effect": "Allow",
            "Action": [
              "athena:StartQueryExecution",
              "athena:GetQueryResults",
              "athena:DeleteNamedQuery",
              "athena:GetNamedQuery",
              "athena:ListQueryExecutions",
              "athena:StopQueryExecution",
              "athena:GetQueryResultsStream",
              "athena:ListNamedQueries",
              "athena:CreateNamedQuery",
              "athena:GetQueryExecution",
              "athena:BatchGetNamedQuery",
              "athena:BatchGetQueryExecution",
              "athena:GetWorkGroup"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:athena:${AWS::Region}:${AWS::AccountId}:workgroup/${workgroupName}",
                {
                  "workgroupName": {
                    "Ref": "WorkGroupName"
                  }
                }
              ]
            }
          }
        ]
```

## TextractPolicy<a name="textract-policy"></a>

Gives full access to Amazon Textract\.

```
        "Statement": [
         {
            "Effect": "Allow",
            "Action": [
              "textract:*"
            ],
            "Resource": "*"
          }
        ]
```

## TextractDetectAnalyzePolicy<a name="textract-detect-analyze-policy"></a>

Gives access to detect and analyze documents with Amazon Textract\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "textract:DetectDocumentText",
              "textract:StartDocumentTextDetection",
              "textract:StartDocumentAnalysis",
              "textract:AnalyzeDocument"
            ],
            "Resource": "*"
          }
        ]
```

## TextractGetResultPolicy<a name="textract-get-result-policy"></a>

Gives access to get detected and analyzed documents from Amazon Textract\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "textract:GetDocumentTextDetection",
              "textract:GetDocumentAnalysis"
            ],
            "Resource": "*"
          }
        ]
```

## EventBridgePutEventsPolicy<a name="eventbridge-put-events-policy"></a>

Gives permissions to send events to Amazon EventBridge\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": "events:PutEvents",
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:events:${AWS::Region}:${AWS::AccountId}:event-bus/${eventBusName}",
                {
                  "eventBusName": {
                    "Ref": "EventBusName"
                  }
                }
              ]
            }
          }
        ]
```

## ElasticMapReduceModifyInstanceFleetPolicy<a name="elastic-map-reduce-modify-instance-fleet-policy"></a>

Gives permission to list details and modify capacities for instance fleets within a cluster\.

```
        "Statement": [
          {
            "Action": [
              "elasticmapreduce:ModifyInstanceFleet",
              "elasticmapreduce:ListInstanceFleets"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:elasticmapreduce:${AWS::Region}:${AWS::AccountId}:cluster/${clusterId}",
                {
                  "clusterId": {
                    "Ref": "ClusterId"
                  }
                }
              ]
            },
            "Effect": "Allow"
          }
        ]
```

## ElasticMapReduceSetTerminationProtectionPolicy<a name="elastic-map-reduce-set-termination-protection-policy"></a>

Gives permission to set termination protection for a cluster\.

```
        "Statement": [
          {
            "Action": "elasticmapreduce:SetTerminationProtection",
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:elasticmapreduce:${AWS::Region}:${AWS::AccountId}:cluster/${clusterId}",
                {
                  "clusterId": {
                    "Ref": "ClusterId"
                  }
                }
              ]
            },
            "Effect": "Allow"
          }
        ]
```

## ElasticMapReduceModifyInstanceGroupsPolicy<a name="elastic-map-reduce-modify-instance-groups-policy"></a>

Gives permission to list details and modify settings for instance groups within a cluster\.

```
        "Statement": [
          {
            "Action": [
              "elasticmapreduce:ModifyInstanceGroups",
              "elasticmapreduce:ListInstanceGroups"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:elasticmapreduce:${AWS::Region}:${AWS::AccountId}:cluster/${clusterId}",
                {
                  "clusterId": {
                    "Ref": "ClusterId"
                  }
                }
              ]
            },
            "Effect": "Allow"
          }
        ]
```

## ElasticMapReduceCancelStepsPolicy<a name="elastic-map-reduce-cancel-steps-policy"></a>

Gives permission to cancel a pending step or steps in a running cluster\.

```
        "Statement": [
          {
            "Action": "elasticmapreduce:CancelSteps",
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:elasticmapreduce:${AWS::Region}:${AWS::AccountId}:cluster/${clusterId}",
                {
                  "clusterId": {
                    "Ref": "ClusterId"
                  }
                }
              ]
            },
            "Effect": "Allow"
          }
        ]
```

## ElasticMapReduceTerminateJobFlowsPolicy<a name="elastic-map-reduce-terminate-job-flows-policy"></a>

Gives permission to shut down a cluster\.

```
        "Statement": [
          {
            "Action": "elasticmapreduce:TerminateJobFlows",
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:elasticmapreduce:${AWS::Region}:${AWS::AccountId}:cluster/${clusterId}",
                {
                  "clusterId": {
                    "Ref": "ClusterId"
                  }
                }
              ]
            },
            "Effect": "Allow"
          }
        ]
```

## ElasticMapReduceAddJobFlowStepsPolicy<a name="elastic-map-reduce-add-job-flows-policy"></a>

Gives permission to add new steps to a running cluster\.

```
        "Statement": [
          {
            "Action": "elasticmapreduce:AddJobFlowSteps",
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:elasticmapreduce:${AWS::Region}:${AWS::AccountId}:cluster/${clusterId}",
                {
                  "clusterId": {
                    "Ref": "ClusterId"
                  }
                }
              ]
            },
            "Effect": "Allow"
          }
        ]
```

## SageMakerCreateEndpointPolicy<a name="sagemaker-create-endpoint-policy"></a>

Gives permission to create an endpoint in Amazon SageMaker\.

```
        "Statement": [
          {
            "Action": [
              "sagemaker:CreateEndpoint"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:sagemaker:${AWS::Region}:${AWS::AccountId}:endpoint/${endpointName}",
                {
                  "endpointName": {
                    "Ref": "EndpointName"
                  }
                }
              ]
            },
            "Effect": "Allow"
          }
        ]
```

## SageMakerCreateEndpointConfigPolicy<a name="sagemaker-create-endpoint-config-policy"></a>

Gives permission to create an endpoint configuration in Amazon SageMaker\.

```
        "Statement": [
          {
            "Action": [
              "sagemaker:CreateEndpointConfig"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:sagemaker:${AWS::Region}:${AWS::AccountId}:endpoint-config/${endpointConfigName}",
                {
                  "endpointConfigName": {
                    "Ref": "EndpointConfigName"
                  }
                }
              ]
            },
            "Effect": "Allow"
          }
        ]
```

## EcsRunTaskPolicy<a name="ecs-run-task-policy"></a>

Gives permission to start a new task for a task definition\.

```
        "Statement": [
          {
            "Action": [
              "ecs:RunTask"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:ecs:${AWS::Region}:${AWS::AccountId}:task-definition/${taskDefinition}",
                {
                  "taskDefinition": {
                    "Ref": "TaskDefinition"
                  }
                }
              ]
            },
            "Effect": "Allow"
          }
        ]
```

## EFSWriteAccessPolicy<a name="efs-write-access-policy"></a>

Gives permission to mount an Amazon EFS file system with write access\.

```
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "elasticfilesystem:ClientMount",
              "elasticfilesystem:ClientWrite"
            ],
            "Resource": {
              "Fn::Sub": [
                "arn:${AWS::Partition}:elasticfilesystem:${AWS::Region}:${AWS::AccountId}:file-system/${FileSystem}",
                {
                  "FileSystem": {
                    "Ref": "FileSystem"
                  }
                }
              ]
            },
            "Condition": {
              "StringEquals": {
                "elasticfilesystem:AccessPointArn": {
                  "Fn::Sub": [
                    "arn:${AWS::Partition}:elasticfilesystem:${AWS::Region}:${AWS::AccountId}:access-point/${AccessPoint}",
                    {
                      "AccessPoint": {
                        "Ref": "AccessPoint"
                      }
                    }
                  ]
                }
              }
            }
          }
        ]
```