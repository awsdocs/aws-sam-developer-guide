# sam local start\-api<a name="sam-cli-command-reference-sam-local-start-api"></a>

Allows you to run your serverless application locally for quick development and testing\. When you run this command in a directory that contains your serverless functions and your AWS SAM template, it creates a local HTTP server that hosts all of your functions\. 

When it's accessed \(through a browser, CLI, and so on\), it starts a Docker container locally to invoke the function\. It reads the CodeUri property of the `AWS::Serverless::Function` resource to find the path in your file system that contains the Lambda function code\. This could be the project's root directory for interpreted languages like Node\.js and Python, or a build directory that stores your compiled artifacts or a Java Archive \(JAR\) file\. 

If you're using an interpreted language, local changes are available immediately in the Docker container on every invoke\. For more compiled languages or projects that require complex packing support, we recommend that you run your own building solution, and point AWS SAM to the directory or file that contains the build artifacts\.

To see an end\-to\-end example that uses this command, see [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md)\. The `sam local start-api` command is part of [Step 4: Testing your application locally \(optional\)](serverless-getting-started-hello-world.md#serverless-getting-started-hello-world-test-locally)\.

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
| \-t, \-\-template PATH | The AWS SAM template file \[default: template\.\[yaml\|yml\]\]\. | 
| \-n, \-\-env\-vars PATH | The JSON file that contains values for the Lambda function's environment variables\. | 
| \-\-parameter\-overrides | Optional\. A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Use the same format as the AWS CLI—for example, 'ParameterKey=KeyPairName, ParameterValue=MyKey ParameterKey=InstanceType,ParameterValue=t1\.micro'\. | 
| \-d, \-\-debug\-port TEXT | When specified, starts the Lambda function container in debug mode and exposes this port on the local host\. | 
| \-\-debugger\-path TEXT | The host path to a debugger that will be mounted into the Lambda container\. | 
| \-\-debug\-args TEXT | Additional arguments to be passed to the debugger\. | 
| \-v, \-\-docker\-volume\-basedir TEXT | The location of the base directory where the AWS SAM file exists\. If Docker is running on a remote machine, you must mount the path where the AWS SAM file exists on the Docker machine, and modify this value to match the remote machine\. | 
| \-\-docker\-network TEXT | The name or ID of an existing Docker network that the Lambda Docker containers should connect to, along with the default bridge network\. If this isn't specified, the Lambda containers only connect to the default bridge Docker network\. | 
| \-l, \-\-log\-file TEXT | The log file to send runtime logs to\. | 
| \-\-layer\-cache\-basedir DIRECTORY | Specifies the location basedir where the Layers your template uses are downloaded to\. | 
| \-\-skip\-pull\-image | Specifies whether the CLI should skip pulling down the latest Docker image for the Lambda runtime\. | 
| \-\-force\-image\-build | Specifies whether CLI should rebuild the image used for invoking functions with layers\. | 
| \-\-profile TEXT | The specific profile from your credential file that gets AWS credentials\. | 
| \-\-region TEXT | The AWS Region to deploy to\. For example, us\-east\-1\. | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 