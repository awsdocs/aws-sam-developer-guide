# sam build<a name="sam-cli-command-reference-sam-build"></a>

Builds a serverless application and prepares it for subsequent steps in your workflow, like locally testing the application or deploying it to the AWS Cloud\. If you provide a `RESOURCE_LOGICAL_ID`, then AWS SAM builds only that resource\. To build a resource of a nested application or stack, you can provide the application or stack logical ID along with the resource logical ID using the format `StackLogicalId/ResourceLogicalId`\.

The `sam build` command processes your AWS SAM template file, application code, and any applicable language\-specific files and dependencies\. The command also copies build artifacts in the format and location expected for subsequent steps in your workflow\. You specify dependencies in a manifest file that you include in your application, such as `requirements.txt` for Python functions, or `package.json` for Node\.js functions\.

The format of your application's build artifacts depends on its package type\. You specify your AWS Lambda function's package type with the `PackageType` property\. The options are:
+ **`Zip`** – A \.zip file archive, which contains your application code and its dependencies\. If you package your code as a \.zip file archive, you must specify a Lambda runtime for your function\.
+ **`Image`** – A container image, which includes the base operating system, runtime, and extensions, in addition to your application code and its dependencies\.

For more information about Lambda package types, see [Lambda deployment packages](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-package.html) in the *AWS Lambda Developer Guide*\.

If a resource includes a `Metadata` resource attribute with a `BuildMethod` entry, `sam build` builds that resource according to the value of the `BuildMethod` entry\. Valid values for `BuildMethod` are 1\) One of the identifiers for a Lambda runtime, or 2\) The `makefile` identifier\.
+ **Lambda runtime identifier** – Build the resource against a Lambda runtime\. For the list of supported runtime identifiers, see [Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) in the *AWS Lambda Developer Guide*\.
+ **`makefile`** identifier – Run the commands of the build target for the resource\. In this case, your makefile must be named `Makefile` and include a build target named `build-resource-logical-id`\.

To build layers and custom runtimes, you can also use the `Metadata` resource attribute with a `BuildMethod` entry\. For information about building layers, see [Building layers](building-layers.md)\. For information about building custom runtimes, see [Building custom runtimes](building-custom-runtimes.md)\.

For serverless function resources that have the `Image` package type, use the `Metadata` resource attribute to configure Docker image settings that are required to build a container image\. For more information about building container images, see [Building a container image](serverless-sam-cli-using-build.md#build-container-image)\.

For a complete example that uses this command, including locally testing and deploying to the AWS Cloud, see [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md)\. The `sam build` command is part of [Step 2: Build your application](serverless-getting-started-hello-world.md#serverless-getting-started-hello-world-build)\.

**Usage:**

```
sam build [OPTIONS] [RESOURCE_LOGICAL_ID]
```

**Examples:**

```
To use these commands, update your SAM template to specify the path
to your function's source code in the resource's Code or CodeUri property.

To build on your workstation, run this command in the directory containing your
SAM template. Built artifacts are written to the .aws-sam/build directory.
$ sam build
 
To build inside a Lambda-like Docker container
$ sam build --use-container

To build with environment variables passed to the build container from the command line
$ sam build --use-container --container-env-var Function1.GITHUB_TOKEN=<token1> --container-env-var GLOBAL_ENV_VAR=<global-token>

To build with environment variables passed to the build container from a file
$ sam build --use-container --container-env-var-file <env-file.json>

Build a Node.js 12 application using a container image pulled from DockerHub
$ sam build --use-container --build-image amazon/aws-sam-cli-build-image-nodejs12.x

Build a function resource using the Python 3.8 container image pulled from DockerHub
$ sam build --use-container --build-image Function1=amazon/aws-sam-cli-build-image-python3.8 
  
To build and run your functions locally
$ sam build && sam local invoke
  
To build and package for deployment
$ sam build && sam package --s3-bucket <bucketname>

To build the 'MyFunction' resource
$ sam build MyFunction

To build the 'MyFunction' resource of the 'MyNestedStack' nested stack
$ sam build MyNestedStack/MyFunction
```

**Arguments:**


****  

| Argument | Description | 
| --- | --- | 
| RESOURCE\_LOGICAL\_ID | Optional\. Instructs AWS SAM to build a single resource declared in the AWS SAM template\. The build artifacts for the specified resource will be the only ones available for subsequent commands in the workflow, i\.e\. sam package and sam deploy\. | 

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-b, \-\-build\-dir DIRECTORY | The path to a directory where the built artifacts are stored\. This directory and all of its content are removed with this option\. | 
| \-s, \-\-base\-dir DIRECTORY | Resolves relative paths to the function's or layer's source code with respect to this directory\. Use this option if you want to change how relative paths to source code folders are resolved\. By default, relative paths are resolved with respect to the AWS SAM template's location\.In addition to the resources in the root application or stack you are building, this option also applies nested applications or stacks\.This option applies to the following resource types and properties:[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-build.html) | 
| \-u, \-\-use\-container | If your functions depend on packages that have natively compiled dependencies, use this option to build your function inside a Lambda\-like Docker container\. | 
| \-e, \-\-container\-env\-var TEXT | Environment variables to pass to the build container\. You can specify this option multiple times\. Each instance of this option takes a key\-value pair, where the key is the resource and environment variable, and the value is the environment variable's value\. For example: \-\-container\-env\-var Function1\.GITHUB\_TOKEN=TOKEN1 \-\-container\-env\-var Function2\.GITHUB\_TOKEN=TOKEN2\.This option only applies if the `--use-container` option is specified, otherwise an error will result\. | 
| \-ef, \-\-container\-env\-var\-file PATH | The path and file name of a JSON file that contains values for the container's environment variables\. For more information about container environment variable files, see [Container environment variable file](serverless-sam-cli-using-build.md#serverless-sam-cli-using-container-environment-file)\.This option only applies if the `--use-container` option is specified, otherwise an error will result\. | 
| \-\-build\-image TEXT |  The URI of the container image that you want to pull for the build\. By default, AWS SAM pulls the container image from Amazon ECR Public\. Use this option to pull the image from another location\. You can specify this option multiple times\. Each instance of this option can take either a string or a key\-value pair\. If you specify a string, it is the URI of the container image to use for all resources in your application\. For example, `sam build --use-container --build-image amazon/aws-sam-cli-build-image-python3.8`\. If you specify a key\-value pair, the key is the resource name, and the value is the URI of the container image to use for that resource\. For example `sam build --use-container --build-image Function1=amazon/aws-sam-cli-build-image-python3.8`\. With key\-value pairs, you can specify different container images for different resources\. This option only applies if the `--use-container` option is specified, otherwise an error will result\.  | 
| \-m, \-\-manifest PATH | The path to a custom dependency manifest file \(for example, package\.json\) to use instead of the default\. | 
| \-t, \-\-template\-file, \-\-template PATH | The path and file name of AWS SAM template file \[default: template\.\[yaml\|yml\]\]\. | 
| \-\-parameter\-overrides | \(Optional\) A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Uses the same format as the AWS Command Line Interface \(AWS CLI\)\. For example: 'ParameterKey=KeyPairName, ParameterValue=MyKey ParameterKey=InstanceType, ParameterValue=t1\.micro'\. | 
| \-\-skip\-pull\-image | Specifies whether the command should skip pulling down the latest Docker image for the Lambda runtime\. | 
| \-\-docker\-network TEXT | Specifies the name or ID of an existing Docker network that Lambda Docker containers should connect to, along with the default bridge network\. If not specified, the Lambda containers connect only to the default bridge Docker network\. | 
| \-\-parallel | Enabled parallel builds\. Use this option to build your AWS SAM template's functions and layers in parallel\. By default, the functions and layers are built in sequence\. | 
| \-\-cached | Enable cached builds\. Use this option to reuse build artifacts that haven't changed from previous builds\. AWS SAM evaluates whether you've changed any files in your project directory\. Note: AWS SAM doesn't evaluate whether you've changed third\-party modules that your project depends on, where you haven't provided a specific version\. For example, if your Python function includes a requirements\.txt file with the entry requests=1\.x, and the latest request module version changes from 1\.1 to 1\.2, then AWS SAM doesn't pull the latest version until you run a non\-cached build\. | 
| \-\-cache\-dir | The directory where the cache artifacts are stored when \-\-cached is specified\. The default cache directory is \.aws\-sam/cache\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging to print debug messages that the AWS SAM CLI generates, and to display timestamps\. | 
| \-\-help | Shows this message and exits\. | 

## Examples<a name="examples"></a>

### Building a resource using a Lambda runtime identifier<a name="examples-runtime-identifier"></a>

Here's an example AWS SAM template showing how to build a resource using a Lambda runtime identifier:

```
Resources:
  MyLayer:
    Type: AWS::Serverless::LayerVersion
    Properties:
      ContentUri: my_layer
      CompatibleRuntimes:
        - python3.6
    Metadata:
      BuildMethod: python3.6
```

With this template, the following command will build the `MyLayer` resource against the Python 3\.6 runtime environment:

```
sam build MyLayer
```

### Building a resource using the `makefile` identifier<a name="examples-makefile-identifier"></a>

Here's an example AWS SAM showing how to build a resource using the `makefile` identifier:

```
Resources:
  MyLayer:
    Type: AWS::Serverless::LayerVersion
    Properties:
      ContentUri: my_layer
      CompatibleRuntimes:
        - python3.8
    Metadata:
      BuildMethod: makefile
```

This is an example of an associated makefile\. The file must be named `Makefile`, and include a build target with the commands you want to run:

```
build-MyLayer:
    mkdir -p "$(ARTIFACTS_DIR)/python"
    cp *.py "$(ARTIFACTS_DIR)/python"
    python -m pip install -r requirements.txt -t "$(ARTIFACTS_DIR)/python"
```

With this template and makefile, the following command will execute the commands for the `build-MyLayer` target:

```
sam build MyLayer
```

### Passing environment variables to a build container<a name="examples-parameters"></a>

Here's an example showing how to pass environment variables to a build container using a file\.

First, create a file named `env.json` with the following contents:

```
{
  "MyFunction1": {
    "GITHUB_TOKEN": "TOKEN1"
  },
  "MyFunction2": {
    "GITHUB_TOKEN": "TOKEN2"
  }
}
```

Then, run the following command:

```
sam build --use-container --container-env-var-file env.json
```

For more information about container environment variable files, see [Container environment variable file](serverless-sam-cli-using-build.md#serverless-sam-cli-using-container-environment-file)\.