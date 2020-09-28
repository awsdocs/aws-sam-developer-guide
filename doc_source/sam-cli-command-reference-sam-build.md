# sam build<a name="sam-cli-command-reference-sam-build"></a>

Builds a serverless application, and prepares it for subsequent steps in your workflow, like locally testing the application, or deploying it to the AWS Cloud\.

The `sam build` command processes your AWS SAM template file, application code, and any applicable language\-specific files and dependencies, and copies build artifacts in the format and location expected by subsequent steps in your workflow\. You specify dependencies in a manifest file that you include in your application, such as `requirements.txt` for Python functions, or `package.json` for Node\.js functions\.

If a resource includes a `Metadata` resource attribute with a `BuildMethod` entry, `sam build` builds that resource according to the value of the `BuildMethod` entry\. Valid values for `BuildMethod` are identifiers for an [AWS Lambda runtime](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html), or `makefile`:
+ **AWS Lambda runtime identifier**\. Build the resource against a Lambda runtime\. For the list of supported runtime identifiers, see [AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html)\.
+ **`makefile`\. **You must have a `makefile` that includes a build target named `build-resource-logical-id`\. In this case, `sam build` executes the commands of the build target\.

You can use the `Metadata` resource attribute with a `BuildMethod` entry to build layers and custom runtimes\. For information about building layers, see [Building layers](building-layers.md)\. For information about building custom runtimes, see [Building custom runtimes](building-custom-runtimes.md)\.

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
| \-b, \-\-build\-dir DIRECTORY | The path to a folder where the built artifacts are stored\. This directory and all of its content is removed with this option\. | 
| \-s, \-\-base\-dir DIRECTORY | Resolves relative paths to the function's source code with respect to this folder\. Use this option if the AWS SAM template and your source code aren't in the same folder\. By default, relative paths are resolved with respect to the template's location\. | 
| \-u, \-\-use\-container | If your functions depend on packages that have natively compiled dependencies, use this flag to build your function inside an AWS Lambda\-like Docker container\. | 
| \-m, \-\-manifest PATH | The path to a custom dependency manifest file \(for example, package\.json\) to use instead of the default\. | 
| \-t, \-\-template\-file, \-\-template PATH | The path and file name of AWS SAM template file \[default: template\.\[yaml\|yml\]\]\. | 
| \-\-parameter\-overrides | Optional\. A string that contains AWS CloudFormation parameter overrides, encoded as key\-value pairs\. Use the same format as the AWS CLI—for example, 'ParameterKey=KeyPairName, ParameterValue=MyKey ParameterKey=InstanceType, ParameterValue=t1\.micro'\. | 
| \-\-skip\-pull\-image | Specifies whether the command should skip pulling down the latest Docker image for the Lambda runtime\. | 
| \-\-docker\-network TEXT | Specifies the name or ID of an existing Docker network that Lambda Docker containers should connect to, along with the default bridge network\. If not specified, the Lambda containers connect only to the default bridge Docker network\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging to print debug message generated by the AWS SAM CLI\. | 
| \-\-help | Shows this message and exits\. | 