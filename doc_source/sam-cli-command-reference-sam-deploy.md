# sam deploy<a name="sam-cli-command-reference-sam-deploy"></a>

Deploys an AWS SAM application\.

This command comes with a guided interactive mode, which you can enable by specifying the `--guided` parameter\. The interactive mode walks you through the parameters required for deployment, provides default options, and optionally saves these options in a configuration file in your project directory\. When you perform subsequent deployments of your application using `sam deploy`, the AWS SAM CLI retrieves the required parameters from the configuration file\.

Objects declared in the `Parameters` section of the AWS SAM template file appear as additional interactive mode prompts\. You're prompted to provide values for each parameter\. For examples of these objects and the corresponding prompts, see the [Examples of additional interactive prompts](#examples) section later in this topic\.

Serverless applications that you configure with code signing generate more interactive mode prompts\. You're asked whether you want your code to be signed, and if so, you're prompted to enter signing profile names and owners\. For examples of these prompts, see the [Examples of additional interactive prompts](#examples) section later in this topic\.

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
| \-\-stack\-name TEXT | \(Required\) The name of the AWS CloudFormation stack that you're deploying to\. If you specify an existing stack, the command updates the stack\. If you specify a new stack, the command creates it\. | 
| \-\-s3\-bucket TEXT | The URI of the Amazon S3 bucket where this command uploads your AWS CloudFormation template\. This is required to deploy templates that are larger than 51,200 bytes\. | 
| \-\-s3\-prefix TEXT | The prefix added to the names of the artifacts that are uploaded to the Amazon S3 bucket\. The prefix name is a path name \(folder name\) for the Amazon S3 bucket\. | 
| \-\-image\-repository TEXT | The name of the Amazon Elastic Container Registry \(Amazon ECR\) repository where this command uploads your function's image\. Required for functions declared with the Image package type\. | 
| \-\-signing\-profiles LIST | \(Optional\) The list of signing profiles to sign your deployment packages with\. This parameter takes a list of key\-value pairs, where the key is the name of the function or layer to sign, and the value is the signing profile, with an optional profile owner delimited with :\. For example, FunctionNameToSign=SigningProfileName1 LayerNameToSign=SigningProfileName2:SigningProfileOwner\. | 
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
| \-\-metadata | \(Optional\) A map of metadata to attach to all artifacts that are referenced in your template\. | 
| \-\-notification\-arns LIST | A list of Amazon Simple Notification Service \(Amazon SNS\) topic ARNs that AWS CloudFormation associates with the stack\. | 
| \-\-tags LIST | A list of tags to associate with the stack that is created or updated\. AWS CloudFormation also propagates these tags to resources in the stack if the resource supports it\. | 
| \-\-parameter\-overrides | A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Use the same format as the AWS Command Line Interface \(AWS CLI\)\. For example, ParameterKey=ParameterValue InstanceType=t1\.micro\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-no\-progressbar | Do not display a progress bar when uploading artifacts to Amazon S3\. | 
| \-\-debug | Turns on debug logging to print debug message generated by the AWS SAM CLI and display timestamps\. | 
| \-\-help | Shows this message and exits\. | 

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