# sam local start\-api<a name="sam-cli-command-reference-sam-local-start-api"></a>

Allows you to run your serverless application locally for quick development and testing\. When you run it in a directory that contains your serverless functions and your AWS SAM template, it creates a local HTTP server that hosts all of your functions\. 

When it's accessed \(through a browser, CLI, and so on\), it starts a Docker container locally to invoke the function\. It reads the CodeUri property of the AWS::Serverless::Function resource to find the path in your file system that contains the Lambda function code\. This could be the project's root directory for interpreted languages like Node\.js and Python, or a build directory that stores your compiled artifacts or a Java archive \(JAR\) file\. If you're using an interpreted language, local changes are available immediately in the Docker container on every invoke\. For more compiled languages or projects that require complex packing support, we recommend that you run your own building solution, and point AWS SAM to the directory or file that contains the build artifacts\.

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
| \-n, \-\-env\-vars PATH | JSON file containing values for Lambda function's environment variables\. | 
| \-d, \-\-debug\-port TEXT | When specified, starts the Lambda function container in debug mode and exposes this port on the local host\. | 
| \-\-debug\-args TEXT | Additional arguments to be passed to the debugger\. | 
| \-v, \-\-docker\-volume\-basedir TEXT | The location of the base directory where the AWS SAM file exists\. If Docker is running on a remote machine, you must mount the path where the AWS SAM file exists on the Docker machine, and modify this value to match the remote machine\. | 
| \-\-docker\-network TEXT | The name or ID of an existing Docker network that the Lambda Docker containers should connect to, along with the default bridge network\. If this isn't specified, the Lambda containers only connect to the default bridge Docker network\. | 
| \-l, \-\-log\-file TEXT | The log file to send runtime logs to\. | 
| \-\-skip\-pull\-image | Specifies whether the CLI should skip pulling down the latest Docker image for the Lambda runtime\. | 
| \-\-profile TEXT | The AWS credentials profile to use\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 