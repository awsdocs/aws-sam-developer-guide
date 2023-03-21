# AWS SAM CLI troubleshooting<a name="sam-cli-troubleshooting"></a>

Troubleshoot error messages when using, installing, and managing the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\)\.

**Topics**
+ [Installation errors](#sam-cli-troubleshoot-install)
+ [Error messages](#sam-cli-troubleshoot-messages)

## Installation errors<a name="sam-cli-troubleshoot-install"></a>

### Linux<a name="sam-cli-troubleshoot-install-linux"></a>

#### Docker error: "Cannot connect to the Docker daemon\. Is the docker daemon running on this host?"<a name="serverless-sam-cli-install-linux-troubleshooting-docker-deamon"></a>

In some cases, to provide permissions for the `ec2-user` to access the Docker daemon, you might have to reboot your instance\. If you receive this error, try rebooting your instance\.

#### Shell error: "command not found"<a name="serverless-sam-cli-install-linux-troubleshooting-sam-cli-not-found"></a>

If you receive this error, your shell can't locate the AWS SAM CLI executable in the path\. Verify the location of the directory where you installed the AWS SAM CLI executable, and then verify that the directory is on your path\.

#### AWS SAM CLI error: "/lib64/libc\.so\.6: version `GLIBC\_2\.14' not found \(required by /usr/local/aws\-sam\-cli/dist/libz\.so\.1\)"<a name="serverless-sam-cli-install-linux-troubleshooting-sam-cli-missing-lib"></a>

If you receive this error, you're using an unsupported version of Linux, and the built\-in glibc version is out of date\. Try either of the following:
+ Upgrade your Linux host to the 64\-bit version of a recent distribution of CentOS, Fedora, Ubuntu, or Amazon Linux 2\.
+ Follow the instructions for [Installing the AWS SAM CLI](install-sam-cli.md)\.

### macOS<a name="sam-cli-troubleshoot-install-macos"></a>

#### The installation failed<a name="sam-cli-troubleshoot-install-macos-install-failed"></a>

![\[Image of the AWS SAM CLI installer showing an installation failed message\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/images/sam-cli-troubleshoot-install-macos-install-failed.jpg)

 If you are installing the AWS SAM CLI for your user and selected an installation directory that you don’t have write permissions for, this error could occur\. Try either of the following: 

1.  Select a different installation directory that you have write permissions for\. 

1.  Delete the installer\. Then, download and run it again\. 

## Error messages<a name="sam-cli-troubleshoot-messages"></a>

### Curl error: "curl: \(6\) Could not resolve: \.\.\."<a name="sam-cli-troubleshoot-messages-curl"></a>

When trying to invoke the API Gateway endpoint, you see the following error:

```
curl: (6) Could not resolve: endpointdomain (Domain name not found)
```

This means that you've attempted to send a request to a domain that's not valid\. This can happen if your serverless application failed to deploy successfully, or if you have a typo in your curl command\. Verify that the application deployed successfully by using the AWS CloudFormation console or the AWS CLI, and verify that your curl command is correct\.

### Error: Failed to create managed resources: Unable to locate credentials<a name="sam-cli-troubleshoot-messages-credentials"></a>

When running the sam deploy command, you see the following error:

```
Error: Failed to create managed resources: Unable to locate credentials
```

This means that you have not set up AWS credentials to enable the AWS SAM CLI to make AWS service calls\. To fix this, you must set up AWS credentials\. For more information, see [Setting up AWS credentials](serverless-getting-started-set-up-credentials.md)\.

### Error: Running AWS SAM projects locally requires Docker\. Have you got it installed?<a name="sam-cli-troubleshoot-messages-docker"></a>

When running the sam local start\-api command, you see the following error:

```
Error: Running AWS SAM projects locally requires Docker. Have you got it installed?
```

This means that you do not have Docker properly installed\. Docker is required to test your application locally\. To fix this, follow the instructions for installing Docker for your development host\. For more information, see [Installing Docker](install-docker.md)\.

### Error: Security Constraints Not Satisfied<a name="sam-cli-troubleshoot-messages-security-constraints"></a>

When running sam deploy \-\-guided, you're prompted with the question `Function may not have authorization defined, Is this okay? [y/N]`\. If you respond to this prompt with **N** \(the default response\), you see the following error:

```
Error: Security Constraints Not Satisfied
```

The prompt is informing you that the application you're about to deploy might have a publicly accessible Amazon API Gateway API configured without authorization\. By responding **N** to this prompt, you're saying that this is not OK\.

To fix this, you have the following options:
+ Configure your application with authorization\. For information about configuring authorization, see [Controlling access to API Gateway APIs](serverless-controlling-access-to-apis.md)\.
+ If your intention is to have a publicly accessible API endpoint without authorization, restart your deployment and respond to this question with **Y** to indicate that you're OK with deploying\.

### message: Missing Authentication Token<a name="sam-cli-troubleshoot-messages-auth-token"></a>

When trying to invoke the API Gateway endpoint, you see the following error:

```
{"message":"Missing Authentication Token"}
```

This means that you've attempted to send a request to the correct domain, but the URI isn't recognizable\. To fix this, verify the full URL, and update the curl command with the correct URL\.