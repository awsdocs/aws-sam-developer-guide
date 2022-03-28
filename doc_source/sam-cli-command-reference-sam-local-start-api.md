# sam local start\-api<a name="sam-cli-command-reference-sam-local-start-api"></a>

Allows you to run your serverless application locally for quick development and testing\. When you run this command in a directory that contains your serverless functions and your AWS SAM template, it creates a local HTTP server that hosts all of your functions\.

By default when you use this command, the AWS SAM CLI assumes that your current working directory is your project's root directory\. The AWS SAM CLI first tries to locate a template file built using the [sam build](sam-cli-command-reference-sam-build.md) command, located in the `.aws-sam` subfolder, and named `template.yaml` or `template.yml`\. Next, the AWS SAM CLI tries to locate a template file named `template.yaml` or `template.yml` in the current working directory\. If you specify the `--template` option, AWS SAM CLI's default behavior is overridden, and will load just that AWS SAM template and the local resources it points to\.

When it's accessed \(through a browser, CLI, and so on\), it starts a Docker container locally to invoke the function\. It reads the CodeUri property of the `AWS::Serverless::Function` resource to find the path in your file system that contains the Lambda function code\. This could be the project's root directory for interpreted languages like Node\.js and Python, or a build directory that stores your compiled artifacts or a Java Archive \(JAR\) file\. 

If you're using an interpreted language, local changes are available immediately in the Docker container on every invoke\. For more compiled languages or projects that require complex packing support, we recommend that you run your own building solution, and point AWS SAM to the directory or file that contains the build artifacts\.

To see an end\-to\-end example that uses this command, see [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md)\. The `sam local start-api` command is part of [Step 4: \(Optional\) Test your application locally](serverless-getting-started-hello-world.md#serverless-getting-started-hello-world-test-locally)\.

**Usage:**

```
sam local start-api [OPTIONS]
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-host TEXT | The local hostname or IP address to bind to \(default: '127\.0\.0\.1'\)\. | 
| \-p, \-\-port INTEGER | The local port number to listen on \(default: '3000'\)\. | 
| \-s, \-\-static\-dir TEXT | Any static asset \(for example, CSS/JavaScript/HTML\) files located in this directory are presented at /\. | 
| \-t, \-\-template PATH | The AWS SAM template file\.**Note:** If you specify this option, AWS SAM loads only the template and the local resources that it points to\. | 
| \-n, \-\-env\-vars PATH | The JSON file that contains values for the Lambda function's environment variables\. | 
| \-\-parameter\-overrides | Optional\. A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Use the same format as the AWS CLI—for example, 'ParameterKey=KeyPairName, ParameterValue=MyKey ParameterKey=InstanceType,ParameterValue=t1\.micro'\. | 
| \-d, \-\-debug\-port TEXT | When specified, starts the Lambda function container in debug mode and exposes this port on the local host\. | 
| \-\-debugger\-path TEXT | The host path to a debugger that will be mounted into the Lambda container\. | 
| \-\-debug\-args TEXT | Additional arguments to be passed to the debugger\. | 
| \-\-warm\-containers \[EAGER \| LAZY\] |  Optional\. Specifies how AWS SAM CLI manages containers for each function\. Two options are available:    `EAGER`: Containers for all functions are loaded at startup and persist between invocations\.    `LAZY`: Containers are only loaded when each function is first invoked\. Those containers persist for additional invocations\.  | 
| \-\-debug\-function |  Optional\. Specifies the Lambda function to apply debug options to when `--warm-containers` is specified\. This parameter applies to `--debug-port`, `--debugger-path`, and `--debug-args`\.  | 
| \-v, \-\-docker\-volume\-basedir TEXT | The location of the base directory where the AWS SAM file exists\. If Docker is running on a remote machine, you must mount the path where the AWS SAM file exists on the Docker machine, and modify this value to match the remote machine\. | 
| \-\-docker\-network TEXT | The name or ID of an existing Docker network that the Lambda Docker containers should connect to, along with the default bridge network\. If this isn't specified, the Lambda containers only connect to the default bridge Docker network\. | 
| \-\-container\-env\-vars | Optional\. Pass environment variables to image container when locally debugging\. | 
| \-l, \-\-log\-file TEXT | The log file to send runtime logs to\. | 
| \-\-layer\-cache\-basedir DIRECTORY | Specifies the location basedir where the Layers your template uses are downloaded to\. | 
| \-\-skip\-pull\-image | Specifies whether the CLI should skip pulling down the latest Docker image for the Lambda runtime\. | 
| \-\-force\-image\-build | Specifies whether CLI should rebuild the image used for invoking functions with layers\. | 
| \-\-invoke\-image TEXT |  The URI of the container image that you want to use for your Lambda functions\. By default, AWS SAM pulls the container image from Amazon ECR Public\. Use this option to pull the image from another location\. You can specify this option multiple times\. Each instance of this option can take either a string or a key\-value pair\. If you specify a string, it is the URI of the container image to use for all functions in your application\. For example, `sam local start-api --invoke-image public.ecr.aws/sam/emu-python3.8`\. If you specify a key\-value pair, the key is the resource name, and the value is the URI of the container image to use for that resource\. For example `sam local start-api --invoke-image public.ecr.aws/sam/emu-python3.8 --invoke-image Function1=amazon/aws-sam-cli-emulation-image-python3.8 `\. With key\-value pairs, you can specify different container images for different resources\.  | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-shutdown | Emulates a shutdown event after the invoke completes, in order to test extension handling of shutdown behavior\. | 
| \-\-container\-host TEXT | Host of locally emulated Lambda container\. The default value is localhost\. If you want to run AWS SAM CLI in a Docker container on macOS, you can specify host\.docker\.internal\. If you want to run the container on a different host than AWS SAM CLI, you can specify the IP address of the remote host\. | 
| \-\-container\-host\-interface TEXT | The IP address of the host network interface that container ports should bind to\. The default value is 127\.0\.0\.1\. Use 0\.0\.0\.0 to bind to all interfaces\.  | 
| \-\-debug | Turns on debug logging to print debug message generated by the AWS SAM CLI and display timestamps\. | 
| \-\-help | Shows this message and exits\. | 