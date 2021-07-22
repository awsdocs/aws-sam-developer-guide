# sam pipeline init<a name="sam-cli-command-reference-sam-pipeline-init"></a>

This command generates a pipeline configuration file that your CI/CD system can use to deploy serverless applications using AWS SAM\.

Before using sam pipeline init, you must bootstrap the necessary resources for each stage in your pipeline\. You can do this by running sam pipeline init \-\-bootstrap to be guided through the setup and configuration file generation process, or refer to resources you have previously created with the sam pipeline bootstrap command\.

**Usage:**

```
sam pipeline init [OPTIONS]
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is default\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-file TEXT | The path and file name of the configuration file containing default parameter values to use\. The default value is samconfig\.toml in the project root directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-bootstrap | Enable interactive mode that walks the user through creating necessary AWS infrastructure resources\. | 
| \-\-debug | Turns on debug logging to print debug messages that the AWS SAM CLI generates, and to display timestamps\. | 
| \-h, \-\-help | Shows this message and exits\. | 