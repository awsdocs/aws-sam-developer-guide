# sam publish<a name="sam-cli-command-reference-sam-publish"></a>

Publish an AWS SAM application to the AWS Serverless Application Repository\. Takes a packaged AWS SAM template and publishes the application to the specified AWS Region\.

The `sam publish` command expects the AWS SAM template to include a `Metadata` section that contains application metadata required for publishing\. In the `Metadata` section, the `LicenseUrl` and `ReadmeUrl` properties must refer to Amazon Simple Storage Service \(Amazon S3\) buckets, not local files\. For more information about the `Metadata` section of the AWS SAM template, see [Publishing serverless applications using the AWS SAM CLI](serverless-sam-template-publishing-applications.md)\.

By default, `sam publish` creates the application as private\. Before other AWS accounts are allowed to view and deploy your application, you must share it\. For information on sharing applications, see [AWS Serverless Application Repository Resource\-Based Policy Examples](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/security_iam_resource-based-policy-examples.html) in the *AWS Serverless Application Repository Developer Guide*\.

**Note**  
Currently `sam publish` doesn't support publishing nested applications that are specified locally\. If your application contains nested applications, you must publish them separately to the AWS Serverless Application Repository before publishing your parent application\.

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
| \-t, \-\-template PATH | The path of AWS SAM template file \[default: template\.\[yaml\|yml\]\]\. | 
| \-\-semantic\-version TEXT | \(Optional\) Use this option to provide a semantic version of your application that overrides the SemanticVersion property in the Metadata section of the template file\. For more information about semantic versioning, see the [Semantic Versioning specification](https://semver.org/)\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging to print debug messages that the AWS SAM CLI generates, and to display timestamps\. | 
| \-\-help | Shows this message and exits\. | 