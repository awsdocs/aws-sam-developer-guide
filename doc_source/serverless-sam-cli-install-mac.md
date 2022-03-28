# Installing the AWS SAM CLI on macOS<a name="serverless-sam-cli-install-mac"></a>

Follow these steps to install and configure the prerequisites for using the AWS SAM command line interface \(CLI\) on your macOS host:

1. Create an AWS account\.

1. Configure AWS Identity and Access Management \(IAM\) permissions and AWS credentials\.

1. Install Docker\. **Note:** Docker is a prerequisite only for testing your application locally or using the `--use-container` option

1. Install Homebrew\.

1. Install the AWS SAM CLI\.

## Step 1: Create an AWS account<a name="serverless-sam-cli-install-mac-aws-account"></a>

If you don't already have an AWS account, see [aws\.amazon\.com](https://aws.amazon.com/) and choose **Create an AWS Account**\. For detailed instructions, see [How do I create and activate a new AWS account?](http://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)

## Step 2: Configure IAM permissions and AWS credentials<a name="serverless-sam-cli-install-mac-iam-permissions"></a>

The IAM user that you use with AWS SAM must have sufficient permissions to make necessary AWS service calls and manage AWS resources\. The simplest way to ensure that a user has sufficient permissions is to grant administrator privileges to them\. For more information, see [Creating your first IAM admin user and group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

**Note**  
If you don't want to grant administrator privileges to users who use the AWS Command Line Interface \(AWS CLI\), you can grant restricted sets of permissions to them\. For more information, see [Permissions](sam-permissions.md)\.

In addition, to enable the AWS SAM CLI to make AWS service calls, you must set up AWS credentials\. For more information, see [Setting up AWS credentials](serverless-getting-started-set-up-credentials.md)\.

## Step 3: Install Docker \(optional\)<a name="serverless-sam-cli-install-mac-docker"></a>

**Note**  
Docker is a prerequisite only for testing your application locally and for building deployment packages using the `--use-container` option\. If you don't plan to use these features initially, you can skip this section or install Docker at a later time\.

Docker is an application that runs containers on your macOS machines\. AWS SAM provides a local environment that's similar to AWS Lambda to use as a Docker container\. You can use this container to build, test, and debug your serverless applications\.

To run serverless projects and functions locally with the AWS SAM CLI, you must have Docker installed and working\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\. The following steps describe how to install, configure, and verify a Docker installation to work with the AWS SAM CLI\.

1. Install Docker

   The AWS SAM CLI supports Docker running on macOS Sierra 10\.12 or above\. To install Docker see [Install Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/)\.

1. Configure your shared drives

   The AWS SAM CLI requires that the project directory, or any parent directory, is listed in a shared drive\. To share drives on macOS, see [ File sharing](https://docs.docker.com/docker-for-mac/#file-sharing)\.

1. Verify the installation

   After Docker is installed, verify that it's working\. Also confirm that you can run Docker commands from the command line \(for example, `docker ps`\)\. You don't need to install, fetch, or pull any containers––the AWS SAM CLI does this automatically as required\.

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
 
 Homebrew 2.5.7
 Homebrew/homebrew-core (git revision 1be3ad; last commit 2020-10-29)
 Homebrew/homebrew-cask (git revision a0cf3; last commit 2020-10-29)
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
 
 SAM CLI, version 1.35.0
```

You're now ready to start development\.

## Upgrading<a name="serverless-sam-cli-install-mac-upgrading"></a>

To upgrade the AWS SAM CLI, using Homebrew, run the following command:

```
brew upgrade aws-sam-cli
```

## Uninstalling<a name="serverless-sam-cli-install-mac-uninstalling"></a>

To uninstall the AWS SAM CLI, using Homebrew, run the following command:

```
brew uninstall aws-sam-cli
```

## Nightly build<a name="serverless-sam-cli-install-mac-nightly-build"></a>

A nightly build of the AWS SAM CLI is available for you to install\. Once installed, you can use the nightly build using the `sam-nightly` command\. You can install and use both the production and nightly build versions of the AWS SAM CLI at the same time\.

The nightly build contains a pre\-release version of AWS SAM CLI code that may be less stable than the production version\. Note that the nightly build does not contain pre\-release version of the build image, so building a serverless application with the `--use-container` option uses the latest production version of the build image\.

To install the nightly build version of the AWS SAM CLI, run the following commands:

```
brew tap aws/tap
brew install aws-sam-cli-nightly
```

To verify you have installed the nightly build version, run the `sam-nightly --version` command\. The output of this command is in the form `1.X.Y.dev<YYYYMMDDHHmm>`, for example:

```
SAM CLI, version 1.20.0.dev202103151200
```

## Next steps<a name="serverless-sam-cli-install-mac-next-steps"></a>

You're now ready to begin building your own serverless applications using AWS SAM\! If you want to start with sample serverless applications, choose one of the following links:
+ [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md) – Step\-by\-step instructions to download, build, and deploy a simple serverless application\.
+ [AWS SAM example applications and patterns](https://serverlessland.com/patterns?framework=SAM) – Sample applications and patterns from community authors that you can further experiment with\.