# sam local invoke<a name="sam-cli-command-reference-sam-local-invoke"></a>

Invokes a local Lambda function once and quits after invocation completes\.

This is useful for developing serverless functions that handle asynchronous events \(such as Amazon S3 or Amazon Kinesis events\)\. It can also be useful if you want to compose a script of test cases\. The event body can be passed in using the `--event` parameter\. The runtime output \(logs etc\) is output to `stderr`, and the Lambda function result is output to `stdout`\.

**Usage:**

```
sam local invoke [OPTIONS] [FUNCTION_IDENTIFIER]
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-e, \-\-event PATH | The JSON file that contains event data that's passed to the Lambda function when it's invoked\. If you don't specify this option, no event is assumed\. To input JSON from stdin you must pass in the value '\-'\. | 
| \-\-no\-event | Invokes the function with an empty event\. | 
| \-t, \-\-template PATH | The AWS SAM template file \[default: template\.\[yaml\|yml\]\]\. | 
| \-n, \-\-env\-vars PATH | The JSON file that contains values for the Lambda function's environment variables\. For more information about environment variables files, see [Environment Variable File](serverless-sam-cli-using-invoke.md#serverless-sam-cli-using-invoke-environment-file)\. | 
| \-\-parameter\-overrides | Optional\. A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Use the same format as the AWS CLI—for example, 'ParameterKey=KeyPairName, ParameterValue=MyKey ParameterKey=InstanceType,ParameterValue=t1\.micro'\. | 
| \-d, \-\-debug\-port TEXT | When specified, starts the Lambda function container in debug mode and exposes this port on the local host\. | 
| \-\-debugger\-path TEXT | The host path to a debugger that will be mounted into the Lambda container\. | 
| \-\-debug\-args TEXT | Additional arguments to be passed to the debugger\. | 
| \-v, \-\-docker\-volume\-basedir TEXT | The location of the base directory where the AWS SAM file exists\. If Docker is running on a remote machine, you must mount the path where the AWS SAM file exists on the Docker machine, and modify this value to match the remote machine\. | 
| \-\-docker\-network TEXT | The name or ID of an existing Docker network that Lambda Docker containers should connect to, along with the default bridge network\. If this isn't specified, the Lambda containers only connect to the default bridge Docker network\. | 
| \-l, \-\-log\-file TEXT | The log file to send runtime logs to\. | 
| \-\-layer\-cache\-basedir DIRECTORY | Specifies the location basedir where the layers your template uses are downloaded to\. | 
| \-\-skip\-pull\-image | Specifies whether the CLI should skip pulling down the latest Docker image for the Lambda runtime\. | 
| \-\-force\-image\-build | Specifies whether the CLI should rebuild the image used for invoking functions with layers\. | 
| \-\-profile TEXT | The AWS credentials profile to use\. | 
| \-\-region TEXT | Sets the AWS Region of the service \(for example, us\-east\-1\)\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 