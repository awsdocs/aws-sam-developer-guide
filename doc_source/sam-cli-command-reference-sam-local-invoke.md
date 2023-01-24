# sam local invoke<a name="sam-cli-command-reference-sam-local-invoke"></a>

Invokes a local AWS Lambda function once and quits after invocation completes\.

By default when you use this command, the AWS SAM CLI assumes that your current working directory is your project's root directory\. The AWS SAM CLI first tries to locate a template file built using the [sam build](sam-cli-command-reference-sam-build.md) command, located in the `.aws-sam` subfolder, and named `template.yaml` or `template.yml`\. Next, the AWS SAM CLI tries to locate a template file named `template.yaml` or `template.yml` in the current working directory\. If you specify the `--template` option, AWS SAM CLI's default behavior is overridden, and will load just that AWS SAM template and the local resources it points to\.



To invoke a function of a nested application or stack, you can provide the application or stack logical ID along with the function logical ID using the format `StackLogicalId/FunctionLogicalId`\.

The `sam local invoke` command is useful for developing serverless functions that handle asynchronous events, such as Amazon Simple Storage Service \(Amazon S3\) or Amazon Kinesis events\. It can also be useful if you want to compose a script of test cases\. You can pass in the event body using the `--event` parameter\. For more information about events, see [Event](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-concepts.html#gettingstarted-concepts-event) in the *AWS Lambda Developer Guide*\. For details about event message formats from different AWS services, see [Working with other services](https://docs.aws.amazon.com/lambda/latest/dg/lambda-services.html) in the *AWS Lambda Developer Guide*\.

The runtime output \(for example, logs\) is output to `stderr`, and the Lambda function result is output to `stdout`\.

**Note**  
If there is more than one function defined in your AWS SAM template, you must provide the `FUNCTION_LOGICAL_ID` of the function you want to invoke\.

**Usage:**

```
sam local invoke [OPTIONS] [FUNCTION_LOGICAL_ID]
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-hook\-name TEXT |  The name of the hook that is used to extend AWS SAM CLI functionality\. Accepted values: `terraform`\.  | 
| \-\-skip\-prepare\-infra | Skips the preparation stage if no infrastructure changes have been made\. use with the \-\-hook\-name option\. | 
| \-e, \-\-event PATH | The JSON file that contains event data that's passed to the Lambda function when it's invoked\. If you don't specify this option, no event is assumed\. To input JSON from stdin, you must pass in the value '\-'\. For details about event message formats from different AWS services, see [Working with other services](https://docs.aws.amazon.com/lambda/latest/dg/lambda-services.html) in the AWS Lambda Developer Guide\. | 
| \-\-no\-event | Invokes the function with an empty event\. | 
| \-t, \-\-template PATH | The AWS SAM template file\.**Note:** If you specify this option, AWS SAM loads only the template and the local resources that it points to\. This option is not compatible with `--hook-name`\. | 
| \-n, \-\-env\-vars PATH | The JSON file that contains values for the Lambda function's environment variables\. For more information about environment variable files, see [Environment variable file](serverless-sam-cli-using-invoke.md#serverless-sam-cli-using-invoke-environment-file)\. | 
| \-\-parameter\-overrides | \(Optional\) A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Uses the same format as the AWS Command Line Interface \(AWS CLI\)\. For example: 'ParameterKey=KeyPairName, ParameterValue=MyKey ParameterKey=InstanceType, ParameterValue=t1\.micro'\. This option is not compatible with \-\-hook\-name\. | 
| \-d, \-\-debug\-port TEXT | When specified, starts the Lambda function container in debug mode and exposes this port on the local host\. | 
| \-\-debugger\-path TEXT | The host path to a debugger that's mounted into the Lambda container\. | 
| \-\-debug\-args TEXT | Additional arguments to pass to the debugger\. | 
| \-v, \-\-docker\-volume\-basedir TEXT | The location of the base directory where the AWS SAM file exists\. If Docker is running on a remote machine, you must mount the path where the AWS SAM file exists on the Docker machine and modify this value to match the remote machine\. | 
| \-\-docker\-network TEXT | The name or ID of an existing Docker network that Lambda Docker containers should connect to, along with the default bridge network\. If this isn't specified, the Lambda containers connect only to the default bridge Docker network\. | 
| \-\-container\-env\-vars | \(Optional\) Pass environment variables to the Lambda function image container when debugging locally\. | 
| \-l, \-\-log\-file TEXT | The log file to send runtime logs to\. | 
| \-\-layer\-cache\-basedir DIRECTORY | Specifies the location of the base directory where the layers that your template uses are downloaded to\. | 
| \-\-skip\-pull\-image |  By default, the AWS SAM CLI checks Lambda's latest remote runtime environment and updates your local image automatically to keep in sync\. Specify this option to skip pulling down the latest Docker image for your Lambda runtime environment\.  | 
| \-\-beta\-features \| \-\-no\-beta\-features | Allow or deny beta features\. | 
| \-\-force\-image\-build | Specifies whether the AWS SAM CLI should rebuild the image used for invoking Lambda functions with layers\. | 
| \-\-invoke\-image TEXT |  The URI of the container image that you want to use for the local function invocation\. By default, AWS SAM pulls the container image from Amazon ECR Public\. Use this option to pull the image from another location\. For example, `sam local invoke MyFunction --invoke-image amazon/aws-sam-cli-emulation-image-python3.8`\.  | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-shutdown | Emulates a shutdown event after the invoke completes, in order to test extension handling of shutdown behavior\. | 
| \-\-container\-host TEXT | Host of locally emulated Lambda container\. The default value is localhost\. If you want to run AWS SAM CLI in a Docker container on macOS, you can specify host\.docker\.internal\. If you want to run the container on a different host than AWS SAM CLI, you can specify the IP address of the remote host\. | 
| \-\-container\-host\-interface TEXT | The IP address of the host network interface that container ports should bind to\. The default value is 127\.0\.0\.1\. Use 0\.0\.0\.0 to bind to all interfaces\.  | 
| \-\-debug | Turns on debug logging to print debug messages that the AWS SAM CLI generates, and to display timestamps\. | 
| \-\-help | Shows this message and exits\. | 