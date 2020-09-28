# sam init<a name="sam-cli-command-reference-sam-init"></a>

Initializes a serverless application with an AWS SAM template\. The template provides a folder structure for your Lambda functions, and is connected to an event source such as APIs, S3 buckets, or DynamoDB tables\. This application includes everything you need to get started and to eventually extend it into a production\-scale application\.

**Usage:**

```
sam init [OPTIONS]
```

**Note**  
With AWS SAM version 0\.30\.0 or later, you can initialize your application using one of two modes: 1\) Interactive workflow, or 2\) Providing all required parameters\.  
*Interactive Workflow:* Through the interactive initialize workflow you can input either 1\) your project name, preferred runtime, and template file, or 2\) the location of a custom template\.  
 
*Providing Parameters: * Provide all required parameters\.
If you provide a subset of required parameters, you will be prompted for the additional required information\.

**Examples:**

```
Initializes a new SAM project with required parameters passed as parameters

sam init --runtime python3.7 --dependency-manager pip --app-template hello-world --name sam-app

Initializes a new SAM project using custom template in a Git/Mercurial repository

# gh being expanded to github url
sam init --location gh:aws-samples/cookiecutter-aws-sam-python

sam init --location git+ssh://git@github.com/aws-samples/cookiecutter-aws-sam-python.git

sam init --location hg+ssh://hg@bitbucket.org/repo/template-name

# Initializes a new SAM project using custom template in a Zipfile

sam init --location /path/to/template.zip

sam init --location https://example.com/path/to/template.zip

# Initializes a new SAM project using custom template in a local path

sam init --location /path/to/template/folder
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-no\-interactive | Disable interactive prompting for init parameters, and fail if any required values are missing\. | 
| \-l, \-\-location TEXT |  The template or application location \(Git, Mercurial, HTTP/HTTPS, ZIP, path\)\. This parameter is required if `--no-interactive` is specified and `--runtime`, `--name`, and `--app-template` are not provided\. For Git repositories, you must use location of the root of the repository\.  | 
| \-r, \-\-runtime \[python2\.7 \| nodejs6\.10 \| ruby2\.5 \| java8 \| python3\.7 \| nodejs8\.10 \| dotnetcore2\.0 \| nodejs10\.x \| dotnetcore2\.1 \| dotnetcore1\.0 \| python3\.6 \| go1\.x\] |  The Lambda runtime of your application\. This parameter is required if `--no-interactive` is specified and `--location` is not provided\.  | 
| \-d, \-\-dependency\-manager \[gradle \| mod \| maven \| bundler \| npm \| cli\-package \| pip\] | Dependency manager of your Lambda runtime | 
| \-o, \-\-output\-dir PATH | The location where the initialized application is output\. | 
| \-n, \-\-name TEXT |  The name of your project to be generated as a folder\. This parameter is required if `--no-interactive` is specified and `--location` is not provided\.  | 
| \-\-app\-template TEXT |  Identifier of the managed application template you want to use\. If not sure, call 'sam init' without options for an interactive workflow\. This parameter is required if `--no-interactive` is specified and `--location` is not provided\. This parameter is only available in SAM CLI version 0\.30\.0 or later\. Specifying this parameter with an earlier version will result in an error\.  | 
| \-\-no\-input | Disables Cookiecutter prompting and accept default values that are defined in the template configuration\. | 
| \-\-extra\-content | Override any custom parameters in the template's cookiecutter\.json configuration, for example, \{"customParam1": "customValue1", "customParam2":"customValue2"\} | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging\. | 
| \-h, \-\-help | Shows this message and exits\. | 