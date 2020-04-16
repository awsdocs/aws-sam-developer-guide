# AWS SAM CLI Config<a name="serverless-sam-cli-config"></a>

The AWS SAM CLI now supports a project\-level configuration file that stores default parameters for AWS SAM commands\. This configuration file stores the parameters to use for command executions\. If the required parameters are available in the configuration file, you can run commands without providing all parameters each execution\.

For example, when executing the `sam deploy --guided` command, AWS SAM CLI automatically adds the required parameters into the configuration file\. You can subsequently execute `sam deploy` with no parameters, and the values will be retrieved from the configuration file\.

## Config Basics<a name="serverless-sam-cli-config-basics"></a>

The configuration file for a project should be created as `samconfig.toml` in your project's root directory\. If you run a command like `sam deploy --guided` this file will be created for you\. These files are written in TOML format: [https://github\.com/toml\-lang/toml](https://github.com/toml-lang/toml)\.

## Example<a name="serverless-sam-cli-config-example"></a>

Here is an exampe AWS SAM CLI config file that is created when using the `sam deploy --guided` command:

```
 
 version=0.1
 [default.deploy.parameters]
 region = "us-west-2"
 stack_name = "my-app-stack"
 capabilites = "CAPABILITY_IAM"
 s3_bucket = "my-source-bucket"
```

## Options<a name="serverless-sam-cli-config-options"></a>

`region`  
Set the region you want to deploy to\. If you omit region, then the AWS SAM CLI will try to resolve the region through AWS profiles and then environment variables\.

`stack_name`  
The name of the AWS CloudFormation stack you’re deploying to\.

`capabilities`  
A list of capabilities that you must specify to allow AWS CloudFormation to create certain stacks\. Some stack templates might include resources that can affect permissions in your AWS account, for example, by creating new AWS Identity and Access Management \(IAM\) users\. For those stacks, you must explicitly acknowledge their capabilities by specifying this parameter\.  
The only valid values are `CAPABILITY_IAM` and `CAPABILITY_NAMED_IAM`\. If you have IAM resources, you can specify either capability\. If you have IAM resources with custom names, you must specify `CAPABILITY_NAMED_IAM`\. If you don't specify this parameter, this action returns an `InsufficientCapabilities` error\.  
Allowed values: `CAPABILITY_IAM`, `CAPABILITY_NAMED_IAM`  
Default value: `CAPABILITY_IAM`

`s3_bucket`  
The S3 bucket name used for deployment artifacts for the `sam deploy` command\. You may use your own Amazon S3 bucket by providing your own value here\.