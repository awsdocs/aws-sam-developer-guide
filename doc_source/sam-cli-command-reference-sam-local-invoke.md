# sam local invoke<a name="sam-cli-command-reference-sam-local-invoke"></a>

Invokes a local Lambda function once and quits after invocation completes\.

This is useful for developing serverless functions that handle asynchronous events \(such as Amazon S3 or Amazon Kinesis events\)\. It can also be useful if you want to compose a script of test cases\. The event body can be passed in either by `stdin` \(default\), or by using the `--event` parameter\. The runtime output \(logs etc\) is output to `stderr`, and the Lambda function result is output to `stdout`\.

**Usage:**

```
sam local invoke [OPTIONS] [FUNCTION_IDENTIFIER]
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-e, \-\-event PATH | The JSON file that contains event data that's passed to the Lambda function when it's invoked\. If you don't specify this option, the default is reading the JSON from stdin\. | 
| \-t, \-\-template PATH | The AWS SAM template file \[default: template\.\[yaml\|yml\]\]\. | 
| \-n, \-\-env\-vars PATH | The JSON file that contains values for the Lambda function's environment variables\. | 
| \-d, \-\-debug\-port TEXT | When specified, starts the Lambda function container in debug mode and exposes this port on the local host\. | 
| \-\-debug\-args TEXT | Additional arguments to be passed to the debugger\. | 
| \-v, \-\-docker\-volume\-basedir TEXT | The location of the base directory where the AWS SAM file exists\. If Docker is running on a remote machine, you must mount the path where the AWS SAM file exists on the Docker machine, and modify this value to match the remote machine\. | 
| \-\-docker\-network TEXT | The name or ID of an existing Docker network that Lambda Docker containers should connect to, along with the default bridge network\. If this isn't specified, the Lambda containers only connect to the default bridge Docker network\. | 
| \-l, \-\-log\-file TEXT | The log file to send runtime logs to\. | 
| \-\-skip\-pull\-image | Specifies whether the CLI should skip pulling down the latest Docker image for the Lambda runtime\. | 
| \-\-profile TEXT | The AWS credentials profile to use\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 