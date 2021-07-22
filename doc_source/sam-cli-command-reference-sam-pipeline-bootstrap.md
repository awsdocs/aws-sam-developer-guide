# sam pipeline bootstrap<a name="sam-cli-command-reference-sam-pipeline-bootstrap"></a>

This command generates the required AWS infrastructure resources to connect to your CI/CD system\. This step must be run for each deployment stage in your pipeline, prior to running the sam pipeline init command\.

This command sets up the following AWS infrastructure resources:
+ A pipeline IAM user with access key ID and secret key access credentials to be shared with the CI/CD system\.
+ A pipeline execution IAM role assumed by the pipeline user to obtain access to the AWS account\.
+ An AWS CloudFormation execution IAM role assumed by AWS CloudFormation to deploy the AWS SAM application\.
+ An Amazon S3 bucket to hold the AWS SAM artifacts\.
+ Optionally, an Amazon ECR image repository to hold container image Lambda deployment packages \(if you have a resource that is of package type `Image`\)\.

**Usage:**

```
sam pipeline bootstrap [OPTIONS]
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-no\-interactive | Disable interactive prompting for bootstrap parameters, and fail if any required parameters are missing\. For this command \-\-stage is the only required parameter\. | 
| \-\-stage TEXT | The name of the corresponding deployment stage\. It is used as a suffix for the created AWS infrastructure resources\. | 
| \-\-pipeline\-user TEXT | The Amazon Resource Name \(ARN\) of the IAM user having its access key ID and secret access key shared with the CI/CD system\. It is used to grant this IAM user permission to access the corresponding AWS account\. If not provided, the command will create one along with the access key ID and secret access key credentials\. | 
| \-\-pipeline\-execution\-role TEXT | The ARN of the IAM role to be assumed by the pipeline user to operate on this stage\. Provide it only if you want to use your own role, otherwise this command will create one\. | 
| \-\-cloudformation\-execution\-role TEXT | The ARN of the IAM role to be assumed by the AWS CloudFormation service while deploying the application's stack\. Provide only if you want to use your own role, otherwise the command will create one\. | 
| \-\-bucket TEXT | The ARN of the Amazon S3 bucket to hold the AWS SAM artifacts\. | 
| \-\-create\-image\-repository / \-\-no\-create\-image\-repository | Specify whether to create an Amazon ECR image repository if none is provided\. The Amazon ECR repository holds the container images of Lambda functions or layers having a package type of Image\. The default is \-\-no\-create\-image\-repository\. | 
| \-\-image\-repository TEXT | The ARN of an Amazon ECR image repository to hold the container images of Lambda functions or layers that have a package type of Image\. If provided, the \-\-create\-image\-repository options is ignored\. If not provided and \-\-create\-image\-repository is specified, the command will create one\. | 
| \-\-confirm\-changeset / \-\-no\-confirm\-changeset | Prompt to confirm if the resources are to be deployed\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-debug | Turns on debug logging to print debug messages that the AWS SAM CLI generates, and to display timestamps\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-h, \-\-help | Shows this message and exits\. | 