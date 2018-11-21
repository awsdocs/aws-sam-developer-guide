# Installing AWS SAM CLI on Windows<a name="serverless-sam-cli-install-windows"></a>

You can install the AWS SAM CLI on Windows using pip, a package manager for Python, or using MSI\. For instructions on installing AWS SAM CLI using pip, see [Installing the AWS SAM CLI](serverless-sam-cli-install.md)\. For instructions on installing AWS SAM CLI using MSI see [Install the AWS SAM CLI Using MSI](#serverless-sam-cli-install-windows-msi) below\.

## Docker for Windows<a name="serverless-sam-cli-install-windows-docker"></a>

You need to have Docker installed and running to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\.

To install Docker for Windows, see [Docker For Windows](https://www.docker.com/docker-windows)\.

**Note**  
For Windows users: The AWS SAM CLI requires that the project directory \(or any parent directory\) is listed in [ Docker Shared Drives](https://docs.docker.com/docker-for-windows/#shared-drives)\.

Verify that Docker is working, and that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You do not need to install/fetch/pull any containers, because the AWS SAM CLI will do it automatically as required\.

## Install the AWS SAM CLI Using MSI<a name="serverless-sam-cli-install-windows-msi"></a>

**Prerequisites**
+ [Docker](https://www.docker.com/docker-windows)
+ [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)

**Steps**

Install the MSI from one of these locations:
+ [ 64\-bit](https://github.com/awslabs/aws-sam-cli/releases/download/v0.7.0/AWS_SAM_CLI_64_PY3.msi)\.
+ [ 32\-bit](https://github.com/awslabs/aws-sam-cli/releases/download/v0.7.0/AWS_SAM_CLI_32_PY3.msi)\.

After completing the installation using one of the links above, open a new command prompt/powershell\. You should be able to invoke sam from the command line\.

```
sam --version
```