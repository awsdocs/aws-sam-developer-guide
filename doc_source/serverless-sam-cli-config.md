# AWS SAM CLI Config<a name="serverless-sam-cli-config"></a>

The AWS SAM CLI now supports a project\-level configuration file that stores default parameters for AWS SAM commands\. This configuration file stores the parameters to use for command executions\. If the required parameters are available in the configuration file, you can run commands without providing all parameters each execution\.

For example, when executing the `sam deploy --guided` command, AWS SAM CLI automatically adds the required parameters into the configuration file\. You can subsequently execute `sam deploy` with no parameters, and the values will be retrieved from the configuration file\.

## Config Basics<a name="serverless-sam-cli-config-basics"></a>

The configuration file for a project should be created as `samconfig.toml` in your project's root directory\. If you run a command like `sam deploy --guided` this file will be created for you\. These files are written in TOML format: [https://github\.com/toml\-lang/toml](https://github.com/toml-lang/toml)\.

## Example<a name="serverless-sam-cli-config-example"></a>

Here is an example AWS SAM CLI config file that is created when using the `sam deploy --guided` command:

```
 
 version=0.1
 [default.deploy.parameters]
 region = "us-west-2"
 stack_name = "my-app-stack"
 capabilities = "CAPABILITY_IAM"
 s3_bucket = "my-source-bucket"
```

## Options<a name="serverless-sam-cli-config-options"></a>

`region`  
Set the region you want to deploy to\. If you omit region, then the AWS SAM CLI will try to resolve the region through AWS profiles and then environment variables\.

`stack_name`  
The name of the AWS CloudFormation stack you’re deploying to\.

`capabilities`  
In some cases, you must explicitly acknowledge that your stack template contains certain capabilities in order for AWS CloudFormation to create the stack\. For more information see [CreateChangeSet](https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/API_CreateChangeSet.html) in the *AWS CloudFormation API Reference*\.  
The valid values are the same as the [CreateChangeSet](https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/API_CreateChangeSet.html) AWS CloudFormation API\.  
Valid values: `CAPABILITY_IAM | CAPABILITY_NAMED_IAM | CAPABILITY_AUTO_EXPAND`  
Default value: `CAPABILITY_IAM`

`s3_bucket`  
The S3 bucket name used for deployment artifacts for the `sam deploy` command\. You may use your own Amazon S3 bucket by providing your own value here\.