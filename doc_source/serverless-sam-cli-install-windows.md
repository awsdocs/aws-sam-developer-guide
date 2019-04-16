# Installing the AWS SAM CLI on Windows<a name="serverless-sam-cli-install-windows"></a>

To install the AWS SAM CLI on Windows, first make sure that you've installed the [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) and [Docker for Windows](#serverless-sam-cli-install-windows-docker)\.

## Docker for Windows<a name="serverless-sam-cli-install-windows-docker"></a>

You need to have Docker installed and running to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\.

To install Docker for Windows, see [Docker For Windows](https://www.docker.com/docker-windows)\.

**Note**  
For Windows users: The AWS SAM CLI requires that the project directory \(or any parent directory\) is listed in [ Docker Shared Drives](https://docs.docker.com/docker-for-windows/#shared-drives)\.

Verify that Docker is working, and that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You don't need to install/fetch/pull any containers because the AWS SAM CLI does it automatically, as required\.

## Install the AWS SAM CLI Using the MSI File<a name="serverless-sam-cli-install-windows-msi"></a>

Install the MSI file from one of these locations:
+ [ 64\-bit](https://github.com/awslabs/aws-sam-cli/releases/download/v0.15.0/AWS_SAM_CLI_64_PY3.msi)
+ [ 32\-bit](https://github.com/awslabs/aws-sam-cli/releases/download/v0.15.0/AWS_SAM_CLI_32_PY3.msi)

After completing the installation by using one of these links, open a new command prompt or PowerShell prompt\. You should be able to invoke sam from the command line\.

```
sam --version
```

## Install the AWS SAM CLI Using Pip<a name="serverless-sam-cli-install-windows-pip"></a>

An alternate method of installing the AWS SAM CLI is using pip\. For details on how to do this, see [Installing Using Pip](serverless-sam-cli-install-additional.md#serverless-sam-cli-install-using-pip)\.

## Troubleshooting<a name="serverless-sam-cli-install-troubleshooting-windows"></a>

**Python Not Installed**

If you get an error similar to the following, then you may not have Python installed\.

```
'""' is not recognized as an internal or external command, operable program or batch file.
```

Make sure that you install Python, and try again\. To install Python for Windows see [Python Releases for Windows](https://www.python.org/downloads/windows/)\.
