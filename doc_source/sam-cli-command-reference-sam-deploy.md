# sam deploy<a name="sam-cli-command-reference-sam-deploy"></a>

Deploys an AWS SAM application\.

By default when you use this command, the AWS SAM CLI assumes that your current working directory is your project's root directory\. The AWS SAM CLI first tries to locate a template file built using the [sam build](sam-cli-command-reference-sam-build.md) command, located in the `.aws-sam` subfolder, and named `template.yaml`\. Next, the AWS SAM CLI tries to locate a template file named `template.yaml` or `template.yml` in the current working directory\. If you specify the `--template` option, AWS SAM CLI's default behavior is overridden, and will deploy just that AWS SAM template and the local resources it points to\.

This command comes with a guided interactive mode, which you can enable by specifying the `--guided` option\. The interactive mode walks you through the parameters required for deployment, provides default options, and optionally saves these options in a configuration file in your project directory\. When you perform subsequent deployments of your application using `sam deploy`, the AWS SAM CLI retrieves the required parameters from the configuration file\.

Objects declared in the `Parameters` section of the AWS SAM template file appear as additional interactive mode prompts\. You're prompted to provide values for each parameter\. For examples of these objects and the corresponding prompts, see the [Examples](#examples) section later in this topic\.

Serverless applications that you configure with code signing generate more interactive mode prompts\. You're asked whether you want your code to be signed, and if so, you're prompted to enter signing profile names and owners\. For examples of these prompts, see the [Examples](#examples) section later in this topic\.

For more information about settings that are optionally stored when specifying the `--guided` option, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\.

Deploying AWS Lambda functions through AWS CloudFormation requires an Amazon Simple Storage Service \(Amazon S3\) bucket for the Lambda deployment package\. The AWS SAM CLI creates and manages this Amazon S3 bucket for you\. AWS SAM enables encryption for all files stored in Amazon S3\.

If your application includes any function or layer resources declared with `PackageType: Image`, then you can instruct the AWS SAM CLI to automatically create the required Amazon ECR repositories for you, using either the `--resolve-image-repos` option, or the `--guided` option and responding to prompt "Create managed ERC respositories for all functions?" with `Y`\.

**Usage:**

```
sam deploy [OPTIONS] [ARGS]...
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-g, \-\-guided |  Specify this option to have AWS SAM use prompts to guide you through the deployment\.  | 
| \-t, \-\-template\-file, \-\-template PATH | The path and file name where your AWS SAM template is located\.**Note:** If you specify this option, AWS SAM deploys only the template and the local resources that it points to\. | 
| \-\-stack\-name TEXT | \(Required\) The name of the AWS CloudFormation stack that you're deploying to\. If you specify an existing stack, the command updates the stack\. If you specify a new stack, the command creates it\. | 
| \-\-s3\-bucket TEXT | The name of the Amazon S3 bucket where this command uploads your AWS CloudFormation template\. If your template is larger than 51,200 bytes, then either the \-\-s3\-bucket or the \-\-resolve\-s3 option is required\. If you specify both the \-\-s3\-bucket and \-\-resolve\-s3 options, then an error will result\. | 
| \-\-s3\-prefix TEXT | The prefix added to the names of the artifacts that are uploaded to the Amazon S3 bucket\. The prefix name is a path name \(folder name\) for the Amazon S3 bucket\. | 
| \-\-image\-repository TEXT | The name of the Amazon Elastic Container Registry \(Amazon ECR\) repository where this command uploads your function's image\. Required for functions declared with the Image package type\. | 
| \-\-signing\-profiles LIST | The list of signing profiles to sign your deployment packages with\. This option takes a list of key\-value pairs, where the key is the name of the function or layer to sign, and the value is the signing profile, with an optional profile owner delimited with :\. For example, FunctionNameToSign=SigningProfileName1 LayerNameToSign=SigningProfileName2:SigningProfileOwner\. | 
| \-\-capabilities LIST | A list of capabilities that you must specify to allow AWS CloudFormation to create certain stacks\. Some stack templates might include resources that can affect permissions in your AWS account, for example, by creating new AWS Identity and Access Management \(IAM\) users\. For those stacks, you must explicitly acknowledge their capabilities by specifying this option\. The only valid values are CAPABILITY\_IAM and CAPABILITY\_NAMED\_IAM\. If you have IAM resources, you can specify either capability\. If you have IAM resources with custom names, you must specify CAPABILITY\_NAMED\_IAM\. If you don't specify this option, the operation returns an InsufficientCapabilities error\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-kms\-key\-id TEXT | The ID of an AWS Key Management Service \(AWS KMS\) key used to encrypt artifacts that are at rest in the Amazon S3 bucket\. If this option is not specified, then AWS SAM uses Amazon S3\-managed encryption keys\. | 
| \-\-force\-upload | Specify this option to upload artifacts even if they match existing artifacts in the Amazon S3 bucket\. Matching artifacts are overwritten\. | 
| \-\-no\-execute\-changeset | Indicates whether to execute the changeset\. Specify this option if you want to view your stack changes before executing the changeset\. This command creates an AWS CloudFormation changeset and then exits without executing the changeset\. To execute the changeset, run the same command without this option\. | 
| \-\-role\-arn TEXT | The Amazon Resource Name \(ARN\) of an IAM role that AWS CloudFormation assumes when executing the changeset\. | 
| \-\-fail\-on\-empty\-changeset \| \-\-no\-fail\-on\-empty\-changeset | Specify whether to return a non\-zero exit code if there are no changes to be made to the stack\. The default behavior is to return a non\-zero exit code\. | 
| \-\-confirm\-changeset \| \-\-no\-confirm\-changeset | Prompt to confirm whether the AWS SAM CLI deploys the computed changeset\. | 
| \-\-use\-json | Output JSON for the AWS CloudFormation template\. The default output is YAML\. | 
| \-\-resolve\-s3 | Automatically create an Amazon S3 bucket to use for packaging and deploying for non\-guided deployments\. If you specify the \-\-guided option, then \-\-resolve\-s3 is ignored\. If you specify both the \-\-s3\-bucket and \-\-resolve\-s3 options, then an error will result\. | 
| \-\-resolve\-image\-repos | Automatically create Amazon ECR repositories to use for packaging and deploying for non\-guided deployments\. This option applies only to functions and layers with PackageType: Image specified\. If you specify the \-\-guided option, then \-\-resolve\-image\-repos is ignored\. Note: If AWS SAM automatically creates any Amazon ECR repositories for functions or layers with this option, and you later delete those functions or layers from your AWS SAM template, the corresponding Amazon ECR repositories will be automatically deleted\. | 
| \-\-metadata | A map of metadata to attach to all artifacts that are referenced in your template\. | 
| \-\-notification\-arns LIST | A list of Amazon Simple Notification Service \(Amazon SNS\) topic ARNs that AWS CloudFormation associates with the stack\. | 
| \-\-tags LIST | A list of tags to associate with the stack that is created or updated\. AWS CloudFormation also propagates these tags to resources in the stack that support it\. | 
| \-\-parameter\-overrides | A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Use the same format as the AWS Command Line Interface \(AWS CLI\)\. For example, ParameterKey=ParameterValue InstanceType=t1\.micro\. | 
| \-\-disable\-rollback \| \-\-no\-disable\-rollback | Specify whether to rollback your AWS CloudFormation stack if an error occurs during a deployment\. By default, your AWS CloudFormation stack rolls back to the last stable state if there's an error during a deployment\. If you specify \-\-disable\-rollback and an error occurs during a deployment, resources that have been created or updated before the error occurs aren't rolled back\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is samconfig\.toml in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is default\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-no\-progressbar | Do not display a progress bar when uploading artifacts to Amazon S3\. | 
| \-\-debug | Turns on debug logging to print the debug message that the AWS SAM CLI generates and to display timestamps\. | 
| \-\-help | Shows this message and exits\. | 

**Environment variables:**


****  

| Environment variable | Description | 
| --- | --- | 
| SAM\_CLI\_POLL\_DELAY |  Specify a delay, in seconds, between `DesbribeStack` API calls\.  | 

## Examples<a name="examples"></a>

### Parameters<a name="examples-parameters"></a>

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

### Code signing<a name="examples-code-signing"></a>

Here is an example function configured with code signing\.

**AWS SAM template:**

```
Resources:
  HelloWorld:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: hello_world/
      Handler: app.lambda_handler
      Runtime: python3.7
      CodeSigningConfigArn: arn:aws:lambda:us-east-1:111122223333:code-signing-config:csc-12e12345db1234567
```

**Corresponding `sam deploy --guided` prompts:**

```
#Found code signing configurations in your function definitions
Do you want to sign your code? [Y/n]: 
#Please provide signing profile details for the following functions & layers
#Signing profile details for function 'HelloWorld'
Signing Profile Name: 
Signing Profile Owner Account ID (optional):
#Signing profile details for layer 'MyLayer', which is used by functions {'HelloWorld'}
Signing Profile Name: 
Signing Profile Owner Account ID (optional):
```

### SAM\_CLI\_POLL\_DELAY<a name="examples-delay"></a>

Here is an example `sam deploy` call using the `SAM_CLI_POLL_DELAY` variable to set a 5 second delay between `DescribeStack` API calls\.

```
SAM_CLI_POLL_DELAY=5 sam deploy
```