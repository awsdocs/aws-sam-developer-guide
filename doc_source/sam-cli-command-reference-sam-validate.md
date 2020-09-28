# sam validate<a name="sam-cli-command-reference-sam-validate"></a>

Verifies whether an AWS SAM template file is valid\.

**Usage:**

```
sam validate [OPTIONS]
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-t, \-\-template, \-\-template\-file PATH | The AWS SAM template file \[default: template\.\[yaml\|yml\]\]\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
|  \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 