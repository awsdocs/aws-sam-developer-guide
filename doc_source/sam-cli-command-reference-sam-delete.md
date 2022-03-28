# sam delete<a name="sam-cli-command-reference-sam-delete"></a>

Deletes an AWS SAM application by deleting the AWS CloudFormation stack, the artifacts that were packaged and deployed to Amazon S3 and Amazon ECR, and the AWS SAM template file\.

Also checks whether there is an Amazon ECR companion stack deployed, and if so prompts the user about deleting that stack and Amazon ECR repositories\. If `--no-prompts` is specified, then companion stacks and Amazon ECR repositories are deleted by default\.

**Usage:**

```
sam delete [OPTIONS]
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-stack\-name TEXT | The name of the AWS CloudFormation stack that you want to delete\.  | 
| \-\-no\-prompts |  Specify this option to have AWS SAM operate in non\-interactive mode\. The stack name must be provided, either with the `--stack-name` option, or in the configuration `toml` file\.  | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is samconfig\.toml in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is default\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging to print the debug message that the AWS SAM CLI generates and to display timestamps\. | 
| \-\-help | Shows this message and exits\. | 