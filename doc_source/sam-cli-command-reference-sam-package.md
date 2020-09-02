# sam package<a name="sam-cli-command-reference-sam-package"></a>

Packages an AWS SAM application\. It creates a ZIP file of your code and dependencies, and uploads it to Amazon S3\. It then returns a copy of your AWS SAM template, replacing references to local artifacts with the Amazon S3 location where the command uploaded the artifacts\.

**Note**  
[sam deploy](sam-cli-command-reference-sam-deploy.md) now implicitly performs the functionality of `sam package`\. You can use the [sam deploy](sam-cli-command-reference-sam-deploy.md) command directly to package and deploy your application\. 

**Usage:**

```
sam package [OPTIONS] [ARGS]...
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-template\-file PATH | The path where your AWS SAM template is located\. Default: template\.\[yaml\|yml\]\. | 
| \-\-s3\-bucket TEXT | The name of the Amazon S3 bucket where this command uploads your AWS CloudFormation template\. Required\. | 
| \-\-s3\-prefix TEXT | Prefix added to the artifacts name that are uploaded to the Amazon S3 bucket\. The prefix name is a path name \(folder name\) for the Amazon S3 bucket\. | 
| \-\-kms\-key\-id TEXT | The ID of an AWS KMS key used to encrypt artifacts that are at rest in the Amazon S3 bucket\. | 
| \-\-output\-template\-file PATH | The path to the file where the command writes the packaged template\. If you don't specify a path, the command writes the template to the standard output\. | 
| \-\-use\-json | Output JSON for the AWS CloudFormation template\. YAML is used by default\. | 
| \-\-force\-upload | Override existing files in the Amazon S3 bucket\. Specify this flag to upload artifacts even if they match existing artifacts in the Amazon S3 bucket\. | 
| \-\-metadata | A map of metadata to attach to all artifacts that are referenced in your template\. Optional\. | 
| \-\-profile TEXT | Select a specific profile from your credential file to get AWS credentials\. | 
| \-\-region TEXT | Sets the AWS Region of the service \(for example, us\-east\-1\)\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 

**Note**  
If the AWS SAM template contains a `Metadata` section for ServerlessRepo, and the `LicenseUrl` or `ReadmeUrl` properties contain references to local files, you must update AWS CLI to version 1\.16\.77 or later\. For more information about the `Metadata` section of AWS SAM templates and publishing applications with AWS SAM CLI, see [Publishing Serverless Applications Using the AWS SAM CLI](serverless-sam-template-publishing-applications.md)\.