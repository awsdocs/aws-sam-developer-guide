# sam build<a name="sam-cli-command-reference-sam-build"></a>

Options for the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam build` command\.
+ For an introduction to the AWS SAM CLI, see [What is the AWS SAM CLI?](what-is-sam.md#what-is-sam-cli)\.
+ For documentation on using the AWS SAM CLI `sam build` command, see [Using sam build](using-sam-cli-build.md)\.

## Usage<a name="ref-sam-cli-build-usage"></a>

```
$ sam build <arguments> <options>
```

## Arguments<a name="ref-sam-cli-build-args"></a>


****  

| Argument | Description | 
| --- | --- | 
| RESOURCE\_LOGICAL\_ID | Optional\. Instructs AWS SAM to build a single resource declared in the AWS SAM template\. The build artifacts for the specified resource will be the only ones available for subsequent commands in the workflow, i\.e\. sam package and sam deploy\. | 

## Options<a name="ref-sam-cli-build-options"></a>


****  

| Option | Description | 
| --- | --- | 
| \-\-hook\-name TEXT |  The name of the hook that is used to extend AWS SAM CLI functionality\. Accepted values: `terraform`\.  | 
| \-\-skip\-prepare\-infra | Skips the preparation stage if no infrastructure changes have been made\. use with the \-\-hook\-name option\. | 
| \-b, \-\-build\-dir DIRECTORY | The path to a directory where the built artifacts are stored\. This directory and all of its content are removed with this option\. | 
| \-s, \-\-base\-dir DIRECTORY | Resolves relative paths to the function's or layer's source code with respect to this directory\. Use this option if you want to change how relative paths to source code folders are resolved\. By default, relative paths are resolved with respect to the AWS SAM template's location\.In addition to the resources in the root application or stack you are building, this option also applies nested applications or stacks\.This option applies to the following resource types and properties:[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-build.html) | 
| \-u, \-\-use\-container | If your functions depend on packages that have natively compiled dependencies, use this option to build your function inside a Lambda\-like Docker container\. | 
| \-e, \-\-container\-env\-var TEXT | Environment variables to pass to the build container\. You can specify this option multiple times\. Each instance of this option takes a key\-value pair, where the key is the resource and environment variable, and the value is the environment variable's value\. For example: \-\-container\-env\-var Function1\.GITHUB\_TOKEN=TOKEN1 \-\-container\-env\-var Function2\.GITHUB\_TOKEN=TOKEN2\.This option only applies if the `--use-container` option is specified, otherwise an error will result\. | 
| \-ef, \-\-container\-env\-var\-file PATH | The path and file name of a JSON file that contains values for the container's environment variables\. For more information about container environment variable files, see [Container environment variable file](serverless-sam-cli-using-build.md#serverless-sam-cli-using-container-environment-file)\.This option only applies if the `--use-container` option is specified, otherwise an error will result\. | 
| \-\-build\-image TEXT |  The URI of the container image that you want to pull for the build\. By default, AWS SAM pulls the container image from Amazon ECR Public\. Use this option to pull the image from another location\. You can specify this option multiple times\. Each instance of this option can take either a string or a key\-value pair\. If you specify a string, it is the URI of the container image to use for all resources in your application\. For example, `sam build --use-container --build-image amazon/aws-sam-cli-build-image-python3.8`\. If you specify a key\-value pair, the key is the resource name, and the value is the URI of the container image to use for that resource\. For example `sam build --use-container --build-image Function1=amazon/aws-sam-cli-build-image-python3.8`\. With key\-value pairs, you can specify different container images for different resources\. This option only applies if the `--use-container` option is specified, otherwise an error will result\.  | 
| \-m, \-\-manifest PATH | The path to a custom dependency manifest file \(for example, package\.json\) to use instead of the default\. | 
| \-t, \-\-template\-file, \-\-template PATH | The path and file name of AWS SAM template file \[default: template\.\[yaml\|yml\]\]\. This option is not compatible with \-\-hook\-name\. | 
| \-\-parameter\-overrides | \(Optional\) A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Uses the same format as the AWS Command Line Interface \(AWS CLI\)\. For example: 'ParameterKey=KeyPairName, ParameterValue=MyKey ParameterKey=InstanceType, ParameterValue=t1\.micro'\. This option is not compatible with \-\-hook\-name\. | 
| \-\-skip\-pull\-image | Specifies whether the command should skip pulling down the latest Docker image for the Lambda runtime\. | 
| \-\-docker\-network TEXT | Specifies the name or ID of an existing Docker network that Lambda Docker containers should connect to, along with the default bridge network\. If not specified, the Lambda containers connect only to the default bridge Docker network\. | 
| \-\-beta\-features \| \-\-no\-beta\-features | Allow or deny beta features\. | 
| \-\-parallel | Enabled parallel builds\. Use this option to build your AWS SAM template's functions and layers in parallel\. By default, the functions and layers are built in sequence\. | 
| \-\-cached \| \-\-no\-cached | Enable or disable cached builds\. Use this option to reuse build artifacts that haven't changed from previous builds\. AWS SAM evaluates whether you've changed any files in your project directory\. By default, builds are not cached\. If the \-\-no\-cached option is invoked, it overrides the cached = true setting in samcofig\.toml\. Note: AWS SAM doesn't evaluate whether you've changed third\-party modules that your project depends on, where you haven't provided a specific version\. For example, if your Python function includes a requirements\.txt file with the entry requests=1\.x, and the latest request module version changes from 1\.1 to 1\.2, then AWS SAM doesn't pull the latest version until you run a non\-cached build\. | 
| \-\-cache\-dir | The directory where the cache artifacts are stored when \-\-cached is specified\. The default cache directory is \.aws\-sam/cache\. | 
| \-x, \-\-exclude | The Name of the resource\(s\) to exclude from the SAM CLI build\. For example, if your template contains Function1, Function2, and Function3 and you run sam build \-\-exclude Function2, only Function1 and Function3 will be built\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging to print debug messages that the AWS SAM CLI generates, and to display timestamps\. | 
| \-\-help | Shows this message and exits\. | 