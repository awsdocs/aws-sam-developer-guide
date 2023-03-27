# sam sync<a name="sam-cli-command-reference-sam-sync"></a>

Use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam sync` command to sync local application changes to the AWS Cloud\.
+ For an introduction to the AWS SAM CLI, see [What is the AWS SAM CLI?](what-is-sam.md#what-is-sam-cli)\.
+ For documentation on using the AWS SAM CLI, see [Using the AWS SAM CLI](using-sam-cli.md)\.

## Usage<a name="sam-cli-command-reference-sam-sync-usage"></a>

```
$ sam sync <command> <option> ...
```

## Options<a name="sam-cli-command-reference-sam-sync-options"></a>


****  

| Option | Description | 
| --- | --- | 
| \-t, \-\-template\-file, \-\-template PATH | The path and file name where your AWS SAM template is located\.**Note:** If you specify this option, then AWS SAM deploys only the template and the local resources that it points to\. | 
| \-\-code | By default, AWS SAM syncs all resources in your application\. Specify this option to sync only code resources, which include the following:[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-sync.html)To sync code resources, AWS SAM uses AWS service APIs directly, instead of deploying through AWS CloudFormation\. To update your AWS CloudFormation stack, run sam sync \-\-watch or sam deploy\. | 
| \-\-watch | Starts a process that watches your local application for changes and automatically syncs them to the AWS Cloud\. By default, when you specify this option, AWS SAM syncs all resources in your application as you update them\. With this option, AWS SAM performs an initial AWS CloudFormation deployment\. Then, AWS SAM uses AWS service APIs to update code resources\. AWS SAM uses AWS CloudFormation to update infrastructure resources when you update your AWS SAM template\. | 
| \-\-resource\-id TEXT | Specifies the resource ID to sync\. To sync multiple resources, you can specify this option multiple times\. This option is supported with the \-\-code option\. For example, \-\-resource\-id Function1 \-\-resource\-id Function2\. | 
| \-\-resource TEXT | Specifies the resource type to sync\. To sync multiple resources, you can specify this option multiple times\. This option is supported with the \-\-code option\. The value must be one of the listed resources under \-\-code\. For example, \-\-resource AWS::Serverless::Function \-\-resouce AWS::Serverless::LayerVersion\. | 
|  \-\-skip\-deploy\-sync \| \-\-no\-skip\-deploy\-sync  |  Specify `--skip-deploy-sync` to skip the initial infrastructure sync if its not required\. The AWS SAM CLI will compare your local AWS SAM template with the deployed AWS CloudFormation template and perform a deployment only if a change is detected\. Specify `--no-skip-deploy-sync` to perform an AWS CloudFormation deployment every time `sam sync` is run\. To learn more, see [Skip the initial AWS CloudFormation deployment](using-sam-cli-sync.md#using-sam-cli-sync-options-skip-deploy-sync)\. The default option is `--skip-deploy-sync`\.  | 
| \-\-dependency\-layer \| \-\-no\-dependency\-layer |  Specifies whether to separate dependencies of individual functions into another layer to speed up the sync process\. The default setting is `--dependency-layer`\.  | 
| \-u, \-\-use\-container |  If your functions depend on packages that have natively compiled dependencies, use this option to build your function inside an AWS Lambda\-like Docker container\. **Note:** Currently, this option is not compatible with `--dependency-layer`\. If you use `--use-container` with `--dependency-layer`, the AWS SAM CLI informs you and continues with `--no-dependency-layer`\.  | 
| \-\-stack\-name TEXT | \(Required\) The name of the AWS CloudFormation stack for your application\. | 
| \-\-s3\-bucket TEXT | The name of the Amazon Simple Storage Service \(Amazon S3\) bucket where this command uploads your AWS CloudFormation template\. If your template is larger than 51,200 bytes, then either the \-\-s3\-bucket or the \-\-resolve\-s3 option is required\. If you specify both the \-\-s3\-bucket and \-\-resolve\-s3 options, then an error occurs\. | 
| \-\-s3\-prefix TEXT | The prefix added to the names of the artifacts that you upload to the Amazon S3 bucket\. The prefix name is a path name \(folder name\) for the Amazon S3 bucket\. This applies only to functions declared with the Zip package type\. | 
| \-\-capabilities LIST | A list of capabilities that you specify to allow AWS CloudFormation to create certain stacks\. Some stack templates might include resources that can affect permissions in your AWS account\.For example, by creating new AWS Identity and Access Management \(IAM\) users\. The default capabilities are CAPABILITY\_NAMED\_IAM and CAPABILITY\_AUTO\_EXPAND\. Specify this option to override the default values\. Valid values include the following:[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-sync.html) | 
| \-s, \-\-base\-dir DIRECTORY | Resolves relative paths to the function's or layer's source code with respect to this directory\. Use this option to change how relative paths to source code folders are resolved\. By default, relative paths are resolved with respect to the AWS SAM template's location\.In addition to the resources in the root application or stack that you're building, this option also applies to nested applications or stacks\. Additionally, this option applies to the following resource types and properties:[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-sync.html) | 
| \-\-parameter\-overrides | A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Use the same format as the AWS Command Line Interface \(AWS CLI\)\. For example, ParameterKey=ParameterValue InstanceType=t1\.micro\. | 
| \-\-image\-repository TEXT | The name of the Amazon Elastic Container Registry \(Amazon ECR\) repository where this command uploads your function's image\. Required for functions declared with the Image package type\. | 
| \-\-kms\-key\-id TEXT | The ID of an AWS Key Management Service \(AWS KMS\) key used to encrypt artifacts that are at rest in the Amazon S3 bucket\. If you don't specify this option, then AWS SAM uses Amazon S3\-managed encryption keys\. | 
| \-\-role\-arn TEXT | The Amazon Resource Name \(ARN\) of an IAM role that AWS CloudFormation assumes when applying the changeset\. | 
| \-\-notification\-arns LIST | A list of Amazon Simple Notification Service \(Amazon SNS\) topic ARNs that AWS CloudFormation associates with the stack\. | 
| \-\-tags LIST | A list of tags to associate with the stack that is created or updated\. AWS CloudFormation also propagates these tags to resources in the stack that support it\. | 
| \-\-metadata | A map of metadata to attach to all artifacts that you reference in your template\. | 