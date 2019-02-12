# sam package<a name="sam-cli-command-reference-sam-package"></a>

Packages an AWS SAM application\. This is an alias for [ `aws cloudformation package`](http://docs.aws.amazon.com/cli/latest/reference/cloudformation/package.html)\.

**Note**  
If the AWS SAM template contains a `Metadata` section for ServerlessRepo, and the `LicenseUrl` or `ReadmeUrl` properties contain references to local files, you must update AWS CLI to version 1\.16\.77 or later\. For more information about the `Metadata` section of AWS SAM templates and publishing applications with AWS SAM CLI, see [Publishing Applications Using the AWS SAM CLI](serverless-sam-template-publishing-applications.md)\.

**Usage:**

```
sam package [OPTIONS] [ARGS]...
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-template\-file PATH | The path where your AWS SAM template is located\. | 
| \-\-s3\-bucket BUCKET | The name of the S3 bucket where this command uploads the artifacts that are referenced in your template\. | 
| \-\-output\-template\-file PATH | The path to the file where the command writes the packaged template\. If you don't specify a path, the command writes the template to the standard output\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 