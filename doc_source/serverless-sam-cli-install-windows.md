# Installing the AWS SAM CLI on Windows<a name="serverless-sam-cli-install-windows"></a>

Follow these steps to install and configure the prerequisites for using the AWS SAM command line interface \(CLI\) on your Windows host:

1. Create an AWS Identity and Access Management \(AWS\) account\.

1. Configure IAM permissions and AWS credentials\.

1. Install Docker\. **Note:** Docker is a prerequisite only for testing your application locally or using the `--use-container` option\.

1. Install the AWS SAM CLI\.

## Step 1: Create an AWS account<a name="serverless-sam-cli-install-windows-aws-account"></a>

If you don't already have an AWS account, see [aws\.amazon\.com](https://aws.amazon.com/) and choose **Create an AWS Account**\. For detailed instructions, see [Create and Activate an AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)\.

## Step 2: Configure IAM permissions and AWS credentials<a name="serverless-sam-cli-install-windows-iam-permissions"></a>

The IAM user that you use with AWS SAM must have sufficient permissions to make necessary AWS service calls and manage AWS resources\. The simplest way to ensure that a user has sufficient permissions is to grant administrator privileges to them\. For more information, see [Creating your first IAM admin user and group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

**Note**  
If you don't want to grant administrator privileges to users who use the AWS Command Line Interface \(AWS CLI\), you can grant restricted sets of permissions to them\. For more information, see [Permissions](sam-permissions.md)\.

In addition, to enable the AWS SAM CLI to make AWS service calls, you must set up AWS credentials\. For more information, see [Setting up AWS credentials](serverless-getting-started-set-up-credentials.md)\.

## Step 3: Install Docker \(optional\)<a name="serverless-sam-cli-install-windows-docker"></a>

**Note**  
Docker is a prerequisite only for testing your application locally and for building deployment packages using the `--use-container` option\. If you don't plan to use these features initially, you can skip this section or install Docker at a later time\.

Docker is an application that runs containers on your Linux machines\. AWS SAM provides a local environment that's similar to AWS Lambda to use as a Docker container\. You can use this container to build, test, and debug your serverless applications\.

To run serverless projects and functions locally with the AWS SAM CLI, you must have Docker installed and working\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\. The following steps describe how to install, configure, and verify a Docker installation to work with the AWS SAM CLI\.

1. Install Docker\.

   Docker Desktop supports the most recent Windows operating system\. For legacy versions of Windows, the Docker Toolbox is available\. Choose your version of Windows for the correct Docker installation steps:
   + To install Docker for Windows 10, see [Install Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/)\.
   + To install Docker for older versions of Windows, see [Install Docker Toolbox on Windows](https://docs.docker.com/toolbox/toolbox_install_windows/)\.

1. Configure your shared drives\.

   The AWS SAM CLI requires that the project directory, or any parent directory, is listed in a shared drive\. In some cases you must share your drive in order for Docker to function properly\.
   + If you're using Windows 10 in Hyper\-V mode, see [ Docker File Sharing](https://docs.docker.com/docker-for-windows/#file-sharing)\.
   + To share drives on older versions of Windows, see [Add Shared Directories](https://docs.docker.com/toolbox/toolbox_install_windows/#optional-add-shared-directories)\.

1. Verify the installation\.

   After Docker is installed, verify that it's working\. Also confirm that you can run Docker commands from the command line \(for example, `docker ps`\)\. You don't need to install, fetch, or pull any containers—the AWS SAM CLI does this automatically as required\.

If you run into issues installing Docker, see the [Logs and troubleshooting](https://docs.docker.com/docker-for-windows/troubleshoot/) section of the *Docker installation guide* for additional troubleshooting tips\.

## Step 4: Install the AWS SAM CLI<a name="serverless-sam-cli-install-windows-sam-cli"></a>

Windows Installer \(MSI\) files are the package installer files for the Windows operating system\.

Follow these steps to install the AWS SAM CLI using the MSI file\. 

1. Install the AWS SAM CLI [ 64\-bit](https://github.com/aws/aws-sam-cli/releases/latest/download/AWS_SAM_CLI_64_PY3.msi)\.
**Note**  
If you operate on 32\-bit system, see [Installing AWS SAM CLI on 32\-bit Windows](important-notes.md#important-notes-32-bit-windows)\.

1. Verify the installation\.

   After completing the installation, verify it by opening a new command prompt or PowerShell prompt\. You should be able to invoke `sam` from the command line\.

   ```
   sam --version
   ```

   You should see output like the following after successful installation of the AWS SAM CLI:

   ```
    
    SAM CLI, version 1.15.0
   ```

1. Install Git\.

   To download sample applications using the `sam init` command, you must also install Git\. For instructions, see [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)\.

You're now ready to start development\.

## Uninstalling<a name="serverless-sam-cli-install-windows-uninstalling"></a>

To uninstall the AWS SAM CLI using Windows Settings, follow these steps:

1. From the Start menu, search for "Add or remove programs"\.

1. Select the entry named **AWS SAM Command Line Interface** and choose **Uninstall** to launch the uninstaller\.

1. Confirm that you want to uninstall the AWS SAM CLI\.

## Nightly build<a name="serverless-sam-cli-install-windows-nightly-build"></a>

A nightly build of the AWS SAM CLI is available for you to install\. Once installed, you can use the nightly build using the `sam-nightly` command\. You can install and use both the production and nightly build versions of the AWS SAM CLI at the same time\.

The nightly build contains a pre\-release version of AWS SAM CLI code that may be less stable than the production version\. Note that the nightly build does not contain pre\-release version of the build image, so building a serverless application with the `--use-container` option uses the latest production version of the build image\.

The nightly build is available with this download link: [AWS SAM CLI nightly build](https://github.com/aws/aws-sam-cli/releases/download/sam-cli-nightly/AWS_SAM_CLI_64_PY3.msi)\. To install the nightly build version of the AWS SAM CLI, perform the same steps as in the [Step 4: Install the AWS SAM CLI](#serverless-sam-cli-install-windows-sam-cli) section earlier in this topic, but use the nightly build download link instead\.

To verify you have installed the nightly build version, run the `sam-nightly --version` command\. The output of this command is in the form `1.X.Y.dev<YYYYMMDDHHmm>`, for example:

```
SAM CLI, version 1.20.0.dev202103151200
```

## Next steps<a name="serverless-sam-cli-install-windows-next-steps"></a>

You're now ready to begin building your own serverless applications using AWS SAM\! If you want to start with sample serverless applications, choose one of the following links:
+ [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md) – Step\-by\-step instructions to download, build, and deploy a simple serverless application\.
+ [AWS SAM example applications in GitHub](https://github.com/aws-samples/serverless-app-examples) – Sample applications in the AWS SAM GitHub repository that you can further experiment with\.