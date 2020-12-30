# sam init<a name="sam-cli-command-reference-sam-init"></a>

Initializes a serverless application with an AWS SAM template\. The template provides a folder structure for your AWS Lambda functions, and is connected to a event sources such as APIs, Amazon Simple Storage Service \(Amazon S3\) buckets, or Amazon DynamoDB tables\. This application includes everything that you need to get started and to eventually extend it into a production\-scale application\.

For some sample applications, you can choose the package type of the application, either `Zip` or `Image`\. For more information about Lambda package types, see [Lambda deployment packages](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-package.html) in the *AWS Lambda Developer Guide*\.

**Usage:**

```
sam init [OPTIONS]
```

**Note**  
With AWS SAM version 0\.30\.0 or later, you can initialize your application using one of two modes: 1\) interactive workflow, or 2\) providing all required parameters\.  
*Interactive workflow:* Through the interactive initialize workflow, you can input either 1\) your project name, preferred runtime, and template file, or 2\) the location of a custom template\.
*Providing parameters: * Provide all required parameters\.
If you provide a subset of required parameters, you are prompted for the additional required information\.

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

# Initializes a new SAM project using cookiecutter template in a local path

sam init --location /path/to/template/folder
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-no\-interactive | Disable interactive prompting for init parameters, and fail if any required values are missing\. | 
| \-l, \-\-location TEXT |  The template or application location \(Git, Mercurial, HTTP/HTTPS, \.zip file, path\)\. This parameter is required if `--no-interactive` is specified and `--runtime`, `--name`, and `--app-template` are not provided\. For Git repositories, you must use the location of the root of the repository\. For local paths, the template must be in either \.zip file or [Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/README.html) format\.  | 
| \-\-package\-type \[Zip \| Image\] | The package type of the example application\. Zip creates a \.zip file archive, and Image creates a container image\. | 
| \-r, \-\-runtime \[python2\.7 \| nodejs6\.10 \| ruby2\.5 \| ruby2\.7 \| java8 \| python3\.7 \| nodejs8\.10 \| dotnetcore2\.0 \| nodejs10\.x \| dotnetcore2\.1 \| dotnetcore1\.0 \| python3\.6 \| go1\.x\] |  The Lambda runtime of your application\. This option applies only when the package type is `Zip`\. This parameter is required if `--no-interactive` is specified, `--image-type` is specified as `Zip`, and `--location` is not specified\.  | 
| \-\-base\-image \[amazon/nodejs12\.x\-base \| amazon/nodejs10\.x\-base \| amazon/python3\.8\-base \| amazon/python3\.7\-base \| amazon/python3\.6\-base \| amazon/python2\.7\-base \| amazon/ruby2\.7\-base \| amazon/ruby2\.5\-base \| amazon/go1\.x\-base \| amazon/java11\-base \| amazon/java8\.al2\-base \| amazon/java8\-base \| amazon/dotnetcore3\.1\-base \| amazon/dotnetcore2\.1\-base\] |  The base image of your application\. This option applies only when the package type is `Image`\. This parameter is required if `--no-interactive` is specified, `--image-type` is specified as `Image`, and `--location` is not specified\.  | 
| \-d, \-\-dependency\-manager \[gradle \| mod \| maven \| bundler \| npm \| cli\-package \| pip\] | The dependency manager of your Lambda runtime\. | 
| \-o, \-\-output\-dir PATH | The location where the initialized application is output\. | 
| \-n, \-\-name TEXT |  The name of your project to be generated as a directory\. This parameter is required if `--no-interactive` is specified and `--location` is not provided\.  | 
| \-\-app\-template TEXT |  The identifier of the managed application template that you want to use\. If you're not sure, call `sam init` without options for an interactive workflow\. This parameter is required if `--no-interactive` is specified and `--location` is not provided\. This parameter is available only in AWS SAM CLI version 0\.30\.0 and later\. Specifying this parameter with an earlier version results in an error\.  | 
| \-\-no\-input | Disables Cookiecutter prompting and accepts the vcfdefault values that are defined in the template configuration\. | 
| \-\-extra\-content | Override any custom parameters in the template's cookiecutter\.json configuration, for example, \{"customParam1": "customValue1", "customParam2":"customValue2"\} | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging to print debug messages that the AWS SAM CLI generates, and to display timestamps\. | 
| \-h, \-\-help | Shows this message and exits\. | 
