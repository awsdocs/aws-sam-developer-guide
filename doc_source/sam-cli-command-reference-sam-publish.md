# sam publish<a name="sam-cli-command-reference-sam-publish"></a>

Publish an AWS SAM application to the AWS Serverless Application Repository\. This command takes a packaged AWS SAM template and publishes the application to the specified region\.

This command expects the AWS SAM template to include a `Metadata` containing application metadata required for publishing\. Furthermore, these properties must include references to Amazon S3 buckets for `LicenseUrl` and `ReadmeUrl` values, and not references to local files\. For more details about the `Metadata` section of the AWS SAM template, see [Publishing Serverless Applications Using the AWS SAM CLI](serverless-sam-template-publishing-applications.md)\.

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
| \-\-profile TEXT | Select a specific profile from your credential file to get AWS credentials\. | 
| \-\-region TEXT | Sets the AWS Region of the service \(for example, us\-east\-1\)\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 