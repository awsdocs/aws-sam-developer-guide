# Installing the AWS SAM CLI on macOS<a name="serverless-sam-cli-install-mac"></a>

The following steps help you to install and configure the required prerequisites for using the AWS SAM CLI on your macOS host:

1. Create an AWS account\.

1. Configure IAM permissions\.

1. Install Docker\. Note: Docker is only a prerequisite for testing your application locally\.

1. Install Homebrew\.

1. Install the AWS SAM CLI\.

## Step 1: Create an AWS account<a name="serverless-sam-cli-install-mac-aws-account"></a>

If you don't already have an AWS account, see [aws\.amazon\.com](https://aws.amazon.com/) and choose **Create an AWS Account**\. For detailed instructions, see [Create and Activate an AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)\.

## Step 2: Create an IAM user with administrator permissions<a name="serverless-sam-cli-install-mac-iam-permissions"></a>

If you don't already have an IAM user with administrator permissions, see [Creating Your First IAM Admin User and Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

In addition, you must set up AWS credentials to enable the AWS SAM CLI to make AWS service calls\. For example, the AWS SAM CLI makes calls to Amazon S3 and AWS CloudFormation\. For more information about setting up AWS credentials, see [Setting up AWS credentials](serverless-getting-started-set-up-credentials.md)\.

## Step 3: Install Docker<a name="serverless-sam-cli-install-mac-docker"></a>

**Note**  
Docker is only a prerequisite for testing your application locally and to build deployment packages using the `--use-container` flag\. You may skip this section or install Docker at a later time if you do not plan to use these features initially\.

Docker is an application that runs containers on your macOS machines\. AWS SAM provides a local environment that's similar to AWS Lambda to use as a Docker container\. You can use this container to build, test, and debug your serverless applications\.

You must have Docker installed and working to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\. The following steps describe how to install, configure, and verify a Docker installation to work with the AWS SAM CLI\.

1. Install Docker

   The AWS SAM CLI supports Docker running on macOS Sierra 10\.12 or above\. To install Docker see [Install Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/)\.

1. Configure your shared drives

   The AWS SAM CLI requires that the project directory, or any parent directory, is listed in a shared drive\. To share drives on macOS, see [ File sharing](https://docs.docker.com/docker-for-mac/#file-sharing)\.

1. Verify the installation

   After Docker is installed, verify that it's working\. Also confirm that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You don't need to install, fetch, or pull any containers––the AWS SAM CLI does this automatically as required\.

If you run into issues installing Docker, see the [Logs and troubleshooting](https://docs.docker.com/docker-for-mac/troubleshoot/) section of the *Docker installation guide* for additional troubleshooting tips\.

## Step 4: Install Homebrew<a name="serverless-sam-cli-install-mac-homebrew"></a>

The recommended approach for installing the AWS SAM CLI on macOS is to use the Homebrew package manager\. For more information about Homebrew, see [Homebrew Documentation](https://docs.brew.sh)\.

To install Homebrew, you must first install Git\. For more information about Git, see [Git Documentation](https://git-scm.com)\. Git is available on many different operating systems, including macOS\. For instructions about installing Git on your particular operating system, see [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)\.

Once you have successfully installed Git, run the following to install Homebrew, making sure to follow the prompts:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Verify that Homebrew is installed:

```
brew --version
```

You should see output like the following on successful installation of Homebrew:

```
 
 Homebrew 2.4.11
 Homebrew/homebrew-core (git revision 54246b; last commit 2020-08-13)
 Homebrew/homebrew-cask (git revision 4fd7ce; last commit 2020-08-14)
```

## Step 5: Install the AWS SAM CLI<a name="serverless-sam-cli-install-mac-sam-cli"></a>

Follow these steps to install the AWS SAM CLI using Homebrew:

```
brew tap aws/tap
brew install aws-sam-cli
```

Verify the installation:

```
sam --version
```

You should see output like the following after successful installation of the AWS SAM CLI:

```
 
 SAM CLI, version 1.3.0
```

You're now ready to start development\.

## Upgrading<a name="serverless-sam-cli-install-mac-upgrading"></a>

To upgrade the AWS SAM CLI, you still use Homebrew, but replace `install` with `upgrade` as follows:

```
brew upgrade aws-sam-cli
```

## Next steps<a name="serverless-sam-cli-install-mac-next-steps"></a>

You're now ready to begin building your own serverless applications using AWS SAM\! If you want to start with sample serverless applications, choose one of the following links:
+ [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md) – Step\-by\-step instructions to download, build, and deploy a simple serverless application\.
+ [AWS SAM example applications in GitHub](https://github.com/aws-samples/serverless-app-examples) – Sample applications in the AWS SAM GitHub repository that you can further experiment with\.