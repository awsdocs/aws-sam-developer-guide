# sam deploy<a name="sam-cli-command-reference-sam-deploy"></a>

Deploys an AWS SAM application\.

This command comes with a guided interactive mode, which you can enable by specifying the `--guided` parameter\. The interactive mode walks you through the parameters required for deployment, provides default options, and optionally saves these options in a configuration file in your project directory\. When you perform subsequent deployments of your application using `sam deploy`, the AWS SAM CLI retrieves the required parametersfrom the configuration file\.

Objects declared in the `Parameters` section of the AWS SAM template file appear as additional interactive mode prompts\. For examples of these objects and the corresponding prompts, see the [Example](#examples) section later in this topic\.

For more information about settings that are optionally stored when specifying the `--guided` parameter, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\.

Deploying AWS Lambda functions through AWS CloudFormation requires an Amazon Simple Storage Service \(Amazon S3\) bucket for the Lambda deployment package\. The AWS SAM CLI creates and manages this Amazon S3 bucket for you\.

**Usage:**

```
sam deploy [OPTIONS] [ARGS]...
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-g, \-\-guided |  Specify this flag to have AWS SAM use prompts to guide you through the deployment\.  | 
| \-t, \-\-template\-file, \-\-template PATH | The path and file name where your AWS SAM template is located\. Default: template\.\[yaml\|yml\]\. | 
| \-\-stack\-name TEXT | Required\. The name of the AWS CloudFormation stack that you're deploying to\. If you specify an existing stack, the command updates the stack\. If you specify a new stack, the command creates it\. | 
| \-\-s3\-bucket TEXT | The name of the Amazon S3 bucket where this command uploads your AWS CloudFormation template\. This is required to deploy templates that are larger than 51,200 bytes\. | 
| \-\-s3\-prefix TEXT | The prefix added to the names of the artifacts that are uploaded to the Amazon S3 bucket\. The prefix name is a path name \(folder name\) for the Amazon S3 bucket\. | 
| \-\-capabilities LIST | A list of capabilities that you must specify to allow AWS CloudFormation to create certain stacks\. Some stack templates might include resources that can affect permissions in your AWS account, for example, by creating new AWS Identity and Access Management \(IAM\) users\. For those stacks, you must explicitly acknowledge their capabilities by specifying this parameter\. The only valid values are CAPABILITY\_IAM and CAPABILITY\_NAMED\_IAM\. If you have IAM resources, you can specify either capability\. If you have IAM resources with custom names, you must specify CAPABILITY\_NAMED\_IAM\. If you don't specify this parameter, this operation returns an InsufficientCapabilities error\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-kms\-key\-id TEXT | The ID of an AWS Key Management Service \(AWS KMS\) key used to encrypt artifacts that are at rest in the Amazon S3 bucket\. | 
| \-\-force\-upload | Specify this flag to upload artifacts even if they match existing artifacts in the Amazon S3 bucket\. Matching artifacts are overwritten\. | 
| \-\-no\-execute\-changeset | Indicates whether to execute the changeset\. Specify this flag if you want to view your stack changes before executing the changeset\. This command creates an AWS CloudFormation changeset and then exits without executing the changeset\. To execute the changeset, run the same command without this flag\. | 
| \-\-role\-arn TEXT | The Amazon Resource Name \(ARN\) of an IAM role that AWS CloudFormation assumes when executing the changeset\. | 
| \-\-fail\-on\-empty\-changeset \| \-\-no\-fail\-on\-empty\-changeset | Specify whether to return a non\-zero exit code if there are no changes to be made to the stack\. The default behavior is to return a non\-zero exit code\. | 
| \-\-confirm\-changeset \| \-\-no\-confirm\-changeset | Prompt to confirm whether the AWS SAM CLI deploys the computed changeset\. | 
| \-\-use\-json | Output JSON for the AWS CloudFormation template\. The default output is YAML\. | 
| \-\-metadata | Optional\. A map of metadata to attach to all artifacts that are referenced in your template\. | 
| \-\-notification\-arns LIST | A list of Amazon Simple Notification Service \(Amazon SNS\) topic ARNs that AWS CloudFormation associates with the stack\. | 
| \-\-tags LIST | A list of tags to associate with the stack that is created or updated\. AWS CloudFormation also propagates these tags to resources in the stack if the resource supports it\. | 
| \-\-parameter\-overrides | A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Use the same format as the AWS Command Line Interface \(AWS CLI\)\. For example, ParameterKey=KeyPairName ParameterValue=MyKey ParameterKey=InstanceType ParameterValue=t1\.micro\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 

## Example<a name="examples"></a>

Here is an example object declared in the `Parameters` section, and the corresponding prompt that appears when using `sam deploy --guided`\.

**AWS SAM template:**

```
Parameters:
  MyPar:
    Type: String
    Default: MyParVal
```

**Corresponding `sam deploy --guided` prompt:**

```
Parameter MyPar [MyParVal]:
```