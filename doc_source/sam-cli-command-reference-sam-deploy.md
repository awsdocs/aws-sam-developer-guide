# sam deploy<a name="sam-cli-command-reference-sam-deploy"></a>

Deploys an AWS SAM application\.

This command now comes with a guided interactive mode, which you can enable by specifying the `--guided` parameter\. The interactive mode walks you through the parameters required for deployment, provides default options, and saves these options in a configuration file in your project folder\. You can execute subsequent deployments of your application by simply executing `sam deploy` and the needed parameters will be retrieved from the AWS SAM CLI configuration file\.

Deploying Lambda functions through AWS CloudFormation requires an Amazon S3 bucket for the Lambda deployment package\. AWS SAM CLI now creates and manages this Amazon S3 bucket for you\.

**Usage:**

```
sam deploy [OPTIONS] [ARGS]...
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-g, \-\-guided |  Specify this flag to allow AWS SAM to guide you through the deployment using guided prompts\. For more information about settings that optionally get stored when specifying this parameter, see [AWS SAM CLI Config](serverless-sam-cli-config.md)  | 
| \-\-template\-file PATH | The path where your AWS SAM template is located\. Default: template\.\[yaml\|yml\]\. | 
| \-\-stack\-name TEXT | The name of the AWS CloudFormation stack you're deploying to\. If you specify an existing stack, the command updates the stack\. If you specify a new stack, the command creates it\. Required\. | 
| \-\-s3\-bucket TEXT | The name of the Amazon S3 bucket where this command uploads your AWS CloudFormation template\. This is required for the deployment of templates that are larger than 51,200 bytes\. | 
| \-\-s3\-prefix TEXT | Prefix added to the artifacts name that are uploaded to the Amazon S3 bucket\. The prefix name is a path name \(folder name\) for the Amazon S3 bucket\. | 
| \-\-capabilities LIST |  A list of capabilities that you must specify to allow AWS CloudFormation to create certain stacks\. Some stack templates might include resources that can affect permissions in your AWS account, for example, by creating new AWS Identity and Access Management \(IAM\) users\. For those stacks, you must explicitly acknowledge their capabilities by specifying this parameter\. The only valid values are CAPABILITY\_IAM and CAPABILITY\_NAMED\_IAM\. If you have IAM resources, you can specify either capability\. If you have IAM resources with custom names, you must specify CAPABILITY\_NAMED\_IAM\. If you don't specify this parameter, this action returns an InsufficientCapabilities error\. | 
| \-\-region TEXT | The AWS Region to deploy to \(for example, us\-east\-1\)\. | 
| \-\-profile TEXT | Select a specific profile from your credential file to get AWS credentials\. | 
| \-\-kms\-key\-id TEXT | The ID of an AWS KMS key used to encrypt artifacts that are at rest in the Amazon S3 bucket\. | 
| \-\-force\-upload | Override existing files in the Amazon S3 bucket\. Specify this flag to upload artifacts even if they match existing artifacts in the Amazon S3 bucket\. | 
| \-\-no\-execute\-changeset | Indicates whether to execute the change set\. Specify this flag if you want to view your stack changes before executing the change set\. This command creates an AWS CloudFormation change set and then exits without executing the change set\. If you want to execute the changeset, the stack changes can be made by running the same command without this flag\. | 
| \-\-role\-arn TEXT | The Amazon Resource Name \(ARN\) of an AWS Identity and Access Management \(IAM\) role that AWS CloudFormation assumes when executing the change set\. | 
| \-\-fail\-on\-empty\-changeset \| \-\-no\-fail\-on\-empty\-changeset | Specify whether to return a non\-zero exit code if there are no changes to be made to the stack\. The default behavior is to return a non\-zero exit code\. | 
| \-\-confirm\-changeset \| \-\-no\-confirm\-changeset | Prompt to confirm if the computed changeset is to be deployed by SAM CLI\. | 
| \-\-use\-json | Output JSON for the AWS CloudFormation template\. YAML is used by default\. | 
| \-\-metadata | A map of metadata to attach to all artifacts that are referenced in your template\. Optional\. | 
| \-\-notification\-arns LIST | Amazon Simple Notification Service topic Amazon Resource Names \(ARNs\) that AWS CloudFormation associates with the stack\. | 
| \-\-tags | A list of tags to associate with the stack that is created or updated\. AWS CloudFormation also propagates these tags to resources in the stack if the resource supports it\. | 
| \-\-parameter\-overrides | A string that contains AWS CloudFormation parameter overrides encoded as key=value pairs\. Use the same format as the AWS CLI\. For example, ParameterKey=KeyPairName ParameterValue=MyKey ParameterKey=InstanceType ParameterValue=t1\.micro\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 