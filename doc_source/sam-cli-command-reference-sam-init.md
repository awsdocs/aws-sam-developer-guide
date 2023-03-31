# sam init<a name="sam-cli-command-reference-sam-init"></a>

Options for the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam init` command\.
+ For an introduction to the AWS SAM CLI, see [What is the AWS SAM CLI?](what-is-sam.md#what-is-sam-cli)\.
+ For documentation on using the AWS SAM CLI `sam init` command, see [Using sam init](using-sam-cli-init.md)\.

## Usage<a name="sam-cli-command-reference-sam-init-usage"></a>

```
$ sam init <options>
```

## Options<a name="sam-cli-command-reference-sam-init-options"></a>


****  

| Option | Description | 
| --- | --- | 
| \-a, \-\-architecture \[x86\_64 \| arm64\] |  The instruction set architecture for your application's Lambda functions\. Specify one of `x86_64` or `arm64`\.  | 
| \-\-app\-template TEXT |  The identifier of the managed application template that you want to use\. If you're not sure, call `sam init` without options for an interactive workflow\. This parameter is required if `--no-interactive` is specified and `--location` is not provided\. This parameter is available only in AWS SAM CLI version 0\.30\.0 and later\. Specifying this parameter with an earlier version results in an error\.  | 
| \-\-application\-insights \| \-\-no\-application\-insights |   Activate Amazon CloudWatch Application Insights monitoring for your application\. To learn more, see [Monitor your serverless applications with CloudWatch Application Insights](monitor-app-insights.md)\.   The default option is `--no-application-insights`\.   | 
| \-\-base\-image \[amazon/nodejs18\.x\-base \| amazon/nodejs16\.x\-base \| amazon/nodejs14\.x\-base \| amazon/nodejs12\.x\-base \| amazon/python3\.10\-base \| amazon/python3\.9\-base \| amazon/python3\.8\-base \| amazon/python3\.7\-base \| amazon/ruby2\.7\-base \| amazon/go1\.x\-base \| amazon/java11\-base \| amazon/java8\.al2\-base \| amazon/java8\-base \| amazon/dotnet6\-base \| amazon/dotnet5\.0\-base \| amazon/dotnetcore3\.1\-base \] |  The base image of your application\. This option applies only when the package type is `Image`\. This parameter is required if `--no-interactive` is specified, `--package-type` is specified as `Image`, and `--location` is not specified\.  | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-d, \-\-dependency\-manager \[gradle \| mod \| maven \| bundler \| npm \| cli\-package \| pip\] | The dependency manager of your Lambda runtime\. | 
| \-\-debug | Turns on debug logging to print debug messages that the AWS SAM CLI generates, and to display timestamps\. | 
| \-\-extra\-content | Override any custom parameters in the template's cookiecutter\.json configuration, for example, \{"customParam1": "customValue1", "customParam2":"customValue2"\} | 
| \-h, \-\-help | Shows this message and exits\. | 
| \-l, \-\-location TEXT |  The template or application location \(Git, Mercurial, HTTP/HTTPS, \.zip file, path\)\. This parameter is required if `--no-interactive` is specified and `--runtime`, `--name`, and `--app-template` are not provided\. For Git repositories, you must use the location of the root of the repository\. For local paths, the template must be in either \.zip file or [Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/README.html) format\.  | 
| \-n, \-\-name TEXT |  The name of your project to be generated as a directory\. This parameter is required if `--no-interactive` is specified and `--location` is not provided\.  | 
| \-\-no\-input | Disables Cookiecutter prompting and accepts the vcfdefault values that are defined in the template configuration\. | 
| \-\-no\-interactive | Disable interactive prompting for init parameters, and fail if any required values are missing\. | 
| \-o, \-\-output\-dir PATH | The location where the initialized application is output\. | 
| \-\-package\-type \[Zip \| Image\] | The package type of the example application\. Zip creates a \.zip file archive, and Image creates a container image\. | 
| \-r, \-\-runtime \[ruby2\.7 \| java8 \| java8\.al2 \| java11 \| nodejs12\.x \| nodejs14\.x \| nodejs16\.x \| nodejs18\.x \| dotnet6 \| dotnet5\.0 \| dotnetcore3\.1 \| python3\.10 \| python3\.9 \| python3\.8 \| python3\.7 \| go1\.x\] |  The Lambda runtime of your application\. This option applies only when the package type is `Zip`\. This parameter is required if `--no-interactive` is specified, `--package-type` is specified as `Zip`, and `--location` is not specified\.  | 
| \-\-tracing \| \-\-no\-tracing | Activate AWS X\-Ray tracing for your Lambda functions\. | 