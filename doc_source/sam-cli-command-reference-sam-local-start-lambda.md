# sam local start\-lambda<a name="sam-cli-command-reference-sam-local-start-lambda"></a>

Enables you to programmatically invoke your Lambda function locally by using the AWS CLI or SDKs\. This command starts a local endpoint that emulates AWS Lambda\.

By default when you use this command, the AWS SAM CLI assumes that your current working directory is your project's root directory\. The AWS SAM CLI first tries to locate a template file built using the [sam build](sam-cli-command-reference-sam-build.md) command, located in the `.aws-sam` subfolder, and named `template.yaml` or `template.yml`\. Next, the AWS SAM CLI tries to locate a template file named `template.yaml` or `template.yml` in the current working directory\. If you specify the `--template` option, AWS SAM CLI's default behavior is overridden, and will load just that AWS SAM template and the local resources it points to\.

You can run your automated tests against this local Lambda endpoint\. When you send an invoke to this endpoint using the AWS CLI or SDK, it locally executes the Lambda function that's specified in the request\.

**Usage:**

```
sam local start-lambda [OPTIONS]
```

**Examples:**

```
# SETUP
# ------
# Start the local Lambda endpoint by running this command in the directory that contains your AWS SAM template.

sam local start-lambda

# USING AWS CLI
# -------------
# Then, you can invoke your Lambda function locally using the AWS CLI

aws lambda invoke --function-name "HelloWorldFunction" --endpoint-url "http://127.0.0.1:3001" --no-verify-ssl out.txt

# USING AWS SDK
# -------------
# You can also use the AWS SDK in your automated tests to invoke your functions programatically.
# Here is a Python example:
#
#     self.lambda_client = boto3.client('lambda',
#                                  endpoint_url="http://127.0.0.1:3001",
#                                  use_ssl=False,
#                                  verify=False,
#                                  config=Config(signature_version=UNSIGNED,
#                                                read_timeout=0,
#                                                retries={'max_attempts': 0}))
#    self.lambda_client.invoke(FunctionName="HelloWorldFunction")
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-host TEXT | The local hostname or IP address to bind to \(default: '127\.0\.0\.1'\)\. | 
| \-p, \-\-port INTEGER | The local port number to listen on \(default: '3001'\)\. | 
| \-t, \-\-template PATH | The AWS SAM template file\.**Note:** If you specify this option, AWS SAM loads only the template and the local resources that it points to\. | 
| \-n, \-\-env\-vars PATH | The JSON file that contains values for the Lambda function's environment variables\. | 
| \-\-parameter\-overrides | Optional\. A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Use the same format as the AWS CLI—for example, 'ParameterKey=KeyPairName, ParameterValue=MyKey ParameterKey=InstanceType,ParameterValue=t1\.micro'\. | 
| \-d, \-\-debug\-port TEXT | When specified, starts the Lambda function container in debug mode, and exposes this port on the local host\. | 
| \-\-debugger\-path TEXT | The host path to a debugger to be mounted into the Lambda container\. | 
| \-\-debug\-args TEXT | Additional arguments to be passed to the debugger\. | 
| \-\-warm\-containers \[EAGER \| LAZY\] |  Optional\. Specifies how AWS SAM CLI manages containers for each function\. Two options are available:  `EAGER`: Containers for all functions are loaded at startup and persist between invocations\.  `LAZY`: Containers are only loaded when each function is first invoked\. Those containers persist for additional invocations\.  | 
| \-\-debug\-function |  Optional\. Specifies the Lambda function to apply debug options to when `--warm-containers` is specified\. This parameter applies to `--debug-port`, `--debugger-path`, and `--debug-args`\.  | 
| \-v, \-\-docker\-volume\-basedir TEXT | The location of the base directory where the AWS SAM file exists\. If Docker is running on a remote machine, you must mount the path where the AWS SAM file exists on the Docker machine, and modify this value to match the remote machine\. | 
| \-\-docker\-network TEXT | The name or ID of an existing Docker network that Lambda Docker containers should connect to, along with the default bridge network\. If this is specified, the Lambda containers only connect to the default bridge Docker network\. | 
| \-\-container\-env\-vars | Optional\. Pass environment variables to image container when locally debugging\. | 
| \-l, \-\-log\-file TEXT | The log file to send runtime logs to\. | 
| \-\-layer\-cache\-basedir DIRECTORY | Specifies the location basedir where the layers your template uses are downloaded to\. | 
| \-\-skip\-pull\-image | Specifies whether the CLI should skip pulling down the latest Docker image for the Lambda runtime\. | 
| \-\-force\-image\-build | Specify whether the CLI should rebuild the image used for invoking functions with layers\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-shutdown | Emulates a shutdown event after the invoke completes, in order to test extension handling of shutdown behavior\. | 
| \-\-container\-host TEXT | Host of locally emulated Lambda container\. The default value is localhost\. If you want to run AWS SAM CLI in a Docker container on macOS, you can specify host\.docker\.internal\. If you want to run the container on a different host than AWS SAM CLI, you can specify the IP address of the remote host\. | 
| \-\-container\-host\-interface TEXT | The IP address of the host network interface that container ports should bind to\. The default value is 127\.0\.0\.1\. Use 0\.0\.0\.0 to bind to all interfaces\.  | 
| \-\-debug | Turns on debug logging to print debug message generated by the AWS SAM CLI and display timestamps\. | 
| \-\-help | Shows this message and exits\. | 