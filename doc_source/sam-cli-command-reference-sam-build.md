# sam build<a name="sam-cli-command-reference-sam-build"></a>

Builds a serverless application, and prepares it for subsequent steps in your workflow, like locally testing the application, or deploying it to the AWS Cloud\.

The `sam build` command processes your AWS SAM template file, application code, and any applicable language\-specific files and dependencies, and copies build artifacts in the format and location expected by subsequent steps in your workflow\. You specify dependencies in a manifest file that you include in your application, such as `requirements.txt` for Python functions, or `package.json` for Node\.js functions\.

The format of your application's build artifacts depends on its package type\. You specify your AWS Lambda function's package type with the `PackageType` property\. The options are:
+ **`Zip`** – A \.zip file archive, which contains your application code and its dependencies\. If you package your code as a \.zip file archive, you must specify a Lambda runtime for your function\.
+ **`Image`** – A container image, which includes the base operating system, the runtime, and extensions, in addition to your application code and its dependencies\.

For more information about Lambda package types, see [Lambda deployment packages](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-package.html) in the *AWS Lambda Developer Guide*\.

If a resource includes a `Metadata` resource attribute with a `BuildMethod` entry, `sam build` builds that resource according to the value of the `BuildMethod` entry\. Valid values for `BuildMethod` are identifiers for a Lambda runtime or `makefile`:
+ **Lambda runtime identifier**\. Build the resource against a Lambda runtime\. For the list of supported runtime identifiers, see [AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html)\.
+ **`makefile`**\. You must have a `makefile` that includes a build target named `build-resource-logical-id`\. In this case, `sam build` executes the commands of the build target\.

To build layers and custom runtimes, you can also use the `Metadata` resource attribute with a `BuildMethod` entry\. For information about building layers, see [Building layers](building-layers.md)\. For information about building custom runtimes, see [Building custom runtimes](building-custom-runtimes.md)\.

For serverless function resources that have the `Image` package type, use the `Metadata` resource attribute to configure Docker image settings that are required to build a container image\. For more information about building container images, see [Building applications](serverless-sam-cli-using-build.md)\.

To see an end\-to\-end example that uses this command, including locally testing and deploying to the AWS Cloud, see [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md)\. The `sam build` command is part of [Step 2: Build your application](serverless-getting-started-hello-world.md#serverless-getting-started-hello-world-build)\.

**Usage:**

```
sam build [OPTIONS] [RESOURCE_LOGICAL_ID]
```

**Examples:**

```
To use this command, update your SAM template to specify the path
to your function's source code in the resource's Code or CodeUri property.

To build on your workstation, run this command in folder containing
SAM template. Built artifacts will be written to .aws-sam/build folder
$ sam build
 
To build inside a AWS Lambda like Docker container
$ sam build --use-container
  
To build & run your functions locally
$ sam build && sam local invoke
  
To build and package for deployment
$ sam build && sam package --s3-bucket <bucketname>

To build the 'MyFunction' resource
$ sam build MyFunction
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-b, \-\-build\-dir DIRECTORY | The path to a folder where the built artifacts are stored\. This directory and all of its content are removed with this option\. | 
| \-s, \-\-base\-dir DIRECTORY | Resolves relative paths to the Lambda function's source code with respect to this folder\. Use this option if the AWS SAM template and your source code aren't in the same folder\. By default, relative paths are resolved with respect to the template's location\. | 
| \-u, \-\-use\-container | If your functions depend on packages that have natively compiled dependencies, use this flag to build your function inside a Lambda\-like Docker container\. | 
| \-m, \-\-manifest PATH | The path to a custom dependency manifest file \(for example, package\.json\) to use instead of the default\. | 
| \-t, \-\-template\-file, \-\-template PATH | The path and file name of AWS SAM template file \[default: template\.\[yaml\|yml\]\]\. | 
| \-\-parameter\-overrides | \(Optional\) A string that contains AWS CloudFormation parameter overrides, encoded as key\-value pairs\. Uses the same format as the AWS Command Line Interface \(AWS CLI\)\. For example: 'ParameterKey=KeyPairName, ParameterValue=MyKey ParameterKey=InstanceType, ParameterValue=t1\.micro' | 
| \-\-skip\-pull\-image | Specifies whether the command should skip pulling down the latest Docker image for the Lambda runtime\. | 
| \-\-docker\-network TEXT | Specifies the name or ID of an existing Docker network that Lambda Docker containers should connect to, along with the default bridge network\. If not specified, the Lambda containers connect only to the default bridge Docker network\. | 
| \-\-parallel | Enabled parallel builds\. Use this flag to build your AWS SAM template's functions and layers in parallel\. By default, the functions and layers are built in sequence\. | 
| \-\-cached | Enable cached builds\. Use this flag to reuse build artifacts that have not changed from previous builds\. AWS SAM evaluates whether you have made any changes to files in your project directory\. Note: AWS SAM does not evaluate whether changes have been made to third party modules that your project depends on, where you have not provided a specific version\. For example, if your Python function includes a requirements\.txt file with the entry requests=1\.x, and the latest request module version changes from 1\.1 to 1\.2, AWS SAM does not pull the latest version until you run a non\-cached build\. | 
| \-\-cache\-dir | The folder where the cache artifacts are stored when \-\-cached is specified\. The default cache directory is \.aws\-sam/cache\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging to print debug messages that the AWS SAM CLI generates, and to display timestamps\. | 
| \-\-help | Shows this message and exits\. | 