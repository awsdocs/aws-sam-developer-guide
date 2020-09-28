# sam publish<a name="sam-cli-command-reference-sam-publish"></a>

Publish an AWS SAM application to the AWS Serverless Application Repository\. This command takes a packaged AWS SAM template and publishes the application to the specified region\.

This command expects the AWS SAM template to include a `Metadata` containing application metadata required for publishing\. Furthermore, these properties must include references to Amazon S3 buckets for `LicenseUrl` and `ReadmeUrl` values, and not references to local files\. For more details about the `Metadata` section of the AWS SAM template, see [Publishing serverless applications using the AWS SAM CLI](serverless-sam-template-publishing-applications.md)\.

This command creates the application as private by default, so you must share the application before other AWS accounts are allowed to view and deploy the application\. For more information on sharing applications see [Using Resource\-Based Policies for the AWS Serverless Application Repository](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/access-control-resource-based.html)\.

**Usage:**

```
sam publish [OPTIONS]
```

**Examples:**

```
# To publish an application
sam publish --template packaged.yaml --region us-east-1
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-t, \-\-template PATH | AWS SAM template file \[default: template\.\[yaml\|yml\]\]\. | 
| \-\-semantic\-version TEXT | Optional\. The semantic version of the application provided by this parameter overrides SemanticVersion in the Metadata section of the template file\. [https://semver\.org/](https://semver.org/) | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 