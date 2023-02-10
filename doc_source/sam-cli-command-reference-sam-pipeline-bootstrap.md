# sam pipeline bootstrap<a name="sam-cli-command-reference-sam-pipeline-bootstrap"></a>

This command generates the required AWS infrastructure resources to connect to your CI/CD system\. This step must be run for each deployment stage in your pipeline prior to running the sam pipeline init command\.

This command sets up the following AWS infrastructure resources:
+ Option of configuring pipeline permissions through:
  + A pipeline IAM user with access key ID and secret key access credentials to be shared with the CI/CD system\.
**Note**  
We recommend rotating access keys regularly\. For more information, see [ Rotate access keys regularly for use cases that require long\-term credentials ](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#rotate-credentials) in the *IAM User Guide*\.
  + Supported CI/CD platforms through OIDC\. For an introduction on using OIDC with AWS SAM pipeline, go to [Using OIDC authentication with AWS SAM pipeline](deploying-with-oidc.md)\.
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
| \-\-config\-env TEXT | The environment name that specifies the default parameter values in the configuration file to use\. The default value is default\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing the default parameter values to use\. The default value is samconfig\.toml in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-interactive \| \-\-no\-interactive | Disable interactive prompting for bootstrap parameters and fail if any required parameters are missing\. The default value is `--interactive`\. For this command, `--stage` is the only required parameter\. **Note:** If `--no-interactive` is specified along with `--use-oidc-provider`, all required parameters for your OIDC provider must be included\. | 
| \-\-stage TEXT | The name of the corresponding deployment stage\. It is used as a suffix for the created AWS infrastructure resources\. | 
| \-\-pipeline\-user TEXT | The Amazon Resource Name \(ARN\) of the IAM user having its access key ID and secret access key shared with the CI/CD system\. It is used to grant this IAM user permission to access the corresponding AWS account\. If not provided, the command will create an IAM user along with the access key ID and secret access key credentials\. | 
| \-\-pipeline\-execution\-role TEXT | The ARN of the IAM role to be assumed by the pipeline user to operate on this stage\. Provide only if you want to use your own role\. If not provided, this command will create a new role\. | 
| \-\-cloudformation\-execution\-role TEXT | The ARN of the IAM role to be assumed by AWS CloudFormation while deploying the application's stack\. Provide only if you want to use your own role\. Otherwise, the command will create a new role\. | 
| \-\-bucket TEXT | The ARN of the Amazon S3 bucket that holds the AWS SAM artifacts\. | 
| \-\-create\-image\-repository \| \-\-no\-create\-image\-repository | Specify whether to create an Amazon ECR image repository if none is provided\. The Amazon ECR repository holds the container images of Lambda functions, or layers having a package type of Image\. The default is \-\-no\-create\-image\-repository\. | 
| \-\-image\-repository TEXT | The ARN of an Amazon ECR image repository that holds the container images of Lambda functions, or layers that have a package type of Image\. If provided, the \-\-create\-image\-repository options is ignored\. If not provided and \-\-create\-image\-repository is specified, the command creates one\. | 
| \-\-confirm\-changeset \| \-\-no\-confirm\-changeset | Prompt to confirm the deployment of your resources\. | 
| \-\-permissions\-provider \[oidc \| iam\] | Choose a permissions provider to assume the pipeline execution role\. The default value is iam\. | 
| \-\-oidc\-provider\-url TEXT | The URL for the OIDC provider\. Value must begin with https://\. | 
| \-\-oidc\-client\-id TEXT | The client ID configured for use with your OIDC provider\. | 
| \-\-github\-org TEXT | The GitHub organization that the repository belongs to\. If no organization exists, enter the user name of the repository owner\. This option is specific to using GitHub Actions OIDC for permissions\. | 
| \-\-github\-repo TEXT | Name of the GitHub repository that deployments will occur from\. This option is specific to using GitHub Actions OIDC for permissions\. | 
| \-\-deployment\-branch TEXT | Name of the branch that deployments will occur from\. This option is specific to using GitHub Actions OIDC for permissions\. | 
| \-\-oidc\-provider \[github\-actions \| gitlab \| bitbucket\-pipelines\] | Name of the CI/CD provider that will be used for OIDC permissions\. GitLab, GitHub, and Bitbucket are supported\. | 
| \-\-gitlab\-group TEXT | The GitLab group that the repository belongs to\. This option is specific to using GitLab OIDC for permissions\. | 
| \-\-gitlab\-project TEXT | The GitLab project name\. This option is specific to using GitLab OIDC for permissions\. | 
| \-\-bitbucket\-repo\-uuid TEXT |   The UUID of the Bitbucket repository\. This option is specific to using Bitbucket OIDC for permissions\.   This value can be found at https://bitbucket\.org/*workspace*/*repository*/admin/addon/admin/pipelines/openid\-connect    | 
| cicd\-provider TEXT | The CI/CD platform for the AWS SAM pipeline\. | 
| \-\-debug | Turns on debug logging and prints debug messages that the AWS SAM CLI generates, and to display timestamps\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-h, \-\-help | Shows this message and exits\. | 

## Troubleshooting<a name="sam-cli-command-reference-sam-pipeline-bootstrap-troubleshooting"></a>

### Error: Missing required parameter<a name="sam-cli-command-reference-sam-pipeline-bootstrap-troubleshooting-example1"></a>

When `--no-interactive` is specified along with `--use-oidc-provider` and any of the required parameters are not provided, this error message will be displayed along with a description of the missing parameters\.