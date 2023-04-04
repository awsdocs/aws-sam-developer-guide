# sam deploy<a name="sam-cli-command-reference-sam-deploy"></a>

Options for the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam deploy` command\.
+ For an introduction to the AWS SAM CLI, see [What is the AWS SAM CLI?](what-is-sam.md#what-is-sam-cli)\.
+ For documentation on using the AWS SAM CLI `sam deploy` command, see [Using sam deploy](using-sam-cli-deploy.md)\.

## Usage<a name="ref-sam-cli-deploy-usage"></a>

```
$ sam deploy <options>
```

## Environment variables<a name="ref-sam-cli-deploy-env"></a>


****  

| Environment variable | Description | 
| --- | --- | 
| SAM\_CLI\_POLL\_DELAY |  Specify a delay, in seconds, between `DescribeStack` API calls\. The following is an example: <pre>$ SAM_CLI_POLL_DELAY=5 sam deploy</pre>  | 

## Options<a name="ref-sam-cli-deploy-options"></a>


****  

| Option | Description | 
| --- | --- | 
| \-g, \-\-guided |  Specify this option to have the AWS SAM CLI use prompts to guide you through the deployment\.  | 
| \-t, \-\-template\-file, \-\-template PATH | The path and file name where your AWS SAM template is located\.**Note:** If you specify this option, then AWS SAM deploys only the template and the local resources that it points to\. | 
| \-\-stack\-name TEXT | \(Required\) The name of the AWS CloudFormation stack that you're deploying to\. If you specify an existing stack, then the command updates the stack\. If you specify a new stack, then the command creates it\. | 
| \-\-s3\-bucket TEXT | The name of the Amazon S3 bucket where this command uploads your AWS CloudFormation template\. If your template is larger than 51,200 bytes, then either the \-\-s3\-bucket option or the \-\-resolve\-s3 option is required\. If you specify both the \-\-s3\-bucket and \-\-resolve\-s3 options, then an error occurs\. | 
| \-\-s3\-prefix TEXT | The prefix added to the names of the artifacts that are uploaded to the Amazon S3 bucket\. The prefix name is a path name \(folder name\) for the Amazon S3 bucket\. | 
| \-\-image\-repository TEXT | The name of the Amazon ECR repository where this command uploads your function's image\. This option is required for functions declared with the Image package type\. | 
| \-\-signing\-profiles LIST | The list of signing profiles to sign your deployment packages with\. This option takes a list of key\-value pairs, where the key is the name of the function or layer to sign, and the value is the signing profile, with an optional profile owner delimited with :\. For example, FunctionNameToSign=SigningProfileName1 LayerNameToSign=SigningProfileName2:SigningProfileOwner\. | 
| \-\-capabilities LIST | A list of capabilities that you must specify to allow AWS CloudFormation to create certain stacks\. Some stack templates might include resources that affect permissions in your AWS account, for example, by creating new AWS Identity and Access Management \(IAM\) users\. For those stacks, you must explicitly acknowledge their capabilities by specifying this option\. The only valid values are CAPABILITY\_IAM and CAPABILITY\_NAMED\_IAM\. If you have IAM resources, then you can specify either capability\. If you have IAM resources with custom names, then you must specify CAPABILITY\_NAMED\_IAM\. If you don't specify this option, then the operation returns an InsufficientCapabilities error\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-kms\-key\-id TEXT | The ID of an AWS Key Management Service \(AWS KMS\) key used to encrypt artifacts that are at rest in the Amazon S3 bucket\. If you don't specify this option, then AWS SAM uses Amazon S3\-managed encryption keys\. | 
| \-\-force\-upload | Specify this option to upload artifacts even if they match existing artifacts in the Amazon S3 bucket\. Matching artifacts are overwritten\. | 
| \-\-no\-execute\-changeset | Indicates whether to apply the changeset\. Specify this option if you want to view your stack changes before applying the changeset\. This command creates an AWS CloudFormation changeset and then exits without applying the changeset\. To apply the changeset, run the same command without this option\. | 
| \-\-role\-arn TEXT | The Amazon Resource Name \(ARN\) of an IAM role that AWS CloudFormation assumes when applying the changeset\. | 
| \-\-fail\-on\-empty\-changeset \| \-\-no\-fail\-on\-empty\-changeset | Specify whether to return a non\-zero exit code if there are no changes to make to the stack\. The default behavior is to return a non\-zero exit code\. | 
| \-\-confirm\-changeset \| \-\-no\-confirm\-changeset | Prompt to confirm whether the AWS SAM CLI deploys the computed changeset\. | 
| \-\-use\-json | Output JSON for the AWS CloudFormation template\. The default output is YAML\. | 
| \-\-resolve\-s3 | Automatically create an Amazon S3 bucket to use for packaging and deploying for non\-guided deployments\. If you specify the \-\-guided option, then the AWS SAM CLI ignores \-\-resolve\-s3\. If you specify both the \-\-s3\-bucket and \-\-resolve\-s3 options, then an error occurs\. | 
| \-\-resolve\-image\-repos | Automatically create Amazon ECR repositories to use for packaging and deploying for non\-guided deployments\. This option applies only to functions and layers with PackageType: Image specified\. If you specify the \-\-guided option, then the AWS SAM CLI ignores \-\-resolve\-image\-repos\. Note: If AWS SAM automatically creates any Amazon ECR repositories for functions or layers with this option, and you later delete those functions or layers from your AWS SAM template, then the corresponding Amazon ECR repositories are automatically deleted\. | 
| \-\-metadata | A map of metadata to attach to all artifacts that are referenced in your template\. | 
| \-\-notification\-arns LIST | A list of Amazon Simple Notification Service \(Amazon SNS\) topic ARNs that AWS CloudFormation associates with the stack\. | 
| \-\-tags LIST | A list of tags to associate with the stack that is created or updated\. AWS CloudFormation also propagates these tags to resources in the stack that support it\. | 
| \-\-parameter\-overrides | A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Use the same format as the AWS Command Line Interface \(AWS CLI\)\. For example, ParameterKey=ParameterValue InstanceType=t1\.micro\. | 
| \-\-disable\-rollback \| \-\-no\-disable\-rollback | Specify whether to roll back your AWS CloudFormation stack if an error occurs during a deployment\. By default, if there's an error during a deployment, your AWS CloudFormation stack rolls back to the last stable state\. If you specify \-\-disable\-rollback and an error occurs during a deployment, then resources that were created or updated before the error occurred aren't rolled back\. | 
| \-\-on\-failure \[ROLLBACK \| DELETE \| DO\_NOTHING\] |  Specify the action to take when a stack fails to create\. The following options are available: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-deploy.html) The default behavior is `ROLLBACK`\. **Note:** You can specify either the `--disable-rollback` option or the `--on-failure` option, but not both\.  | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is samconfig\.toml in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is default\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-no\-progressbar | Do not display a progress bar when uploading artifacts to Amazon S3\. | 
| \-\-debug | Turn on debug logging to print the debug message that the AWS SAM CLI generates and to display timestamps\. | 
| \-\-help | Show this message and exit\. | 