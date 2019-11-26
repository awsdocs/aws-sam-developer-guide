# Installing the AWS SAM CLI on Windows<a name="serverless-sam-cli-install-windows"></a>

The following steps help you to install and configure the required prerequisites for using the AWS SAM CLI on your Windows host:

1. Create an AWS account\.

1. Configure IAM permissions\.

1. Install Docker\. Note: Docker is only a prerequisite for testing your application locally\.

1. Install the AWS SAM CLI\.

## Step 1: Create an AWS Account<a name="serverless-sam-cli-install-windows-aws-account"></a>

If you don't already have an AWS account, see [aws\.amazon\.com](https://aws.amazon.com/) and choose **Create an AWS Account**\. For detailed instructions, see [Create and Activate an AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)\.

## Step 2: Create an IAM User with Administrator Permissions<a name="serverless-sam-cli-install-windows-iam-permissions"></a>

If you don't already have an IAM user with administrator permissions, see [Creating Your First IAM Admin User and Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

## Step 3: Install Docker<a name="serverless-sam-cli-install-windows-docker"></a>

**Note**  
Docker is only a prerequisite for testing your application locally and building deployment packages using the `--use-container` flag\. You can skip this section or install Docker at a later time if you don't plan to use these features initially\.

Docker is an application that runs containers on your Linux machines\. AWS SAM provides a local environment that's similar to AWS Lambda to use as a Docker container\. You can use this container to build, test, and debug your serverless applications\.

You must have Docker installed and working to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\. The following steps describe how to install, configure, and verify a Docker installation to work with the AWS SAM CLI\.

1. Install Docker\.

   Docker Desktop supports the most recent Windows operating system\. For legacy versions of Windows, the Docker Toolbox is available\. Choose your version of Windows for the correct Docker installation steps:
   + To install Docker for Windows 10, see [Install Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/)\.
   + To install Docker for older versions of Windows, see [Install Docker Toolbox on Windows](https://docs.docker.com/toolbox/toolbox_install_windows/)\.

1. Configure your shared drives\.

   The AWS SAM CLI requires that the project directory, or any parent directory, is listed in a shared drive\. Choose your version of Windows below for the correct shared drive instructions:
   + To share drives on Windows 10, see [ Docker Shared Drives](https://docs.docker.com/docker-for-windows/#shared-drives)\.
   + To share drives on older versions of Windows, see [Add Shared Directories](https://docs.docker.com/toolbox/toolbox_install_windows/#optional-add-shared-directories)\.

1. Verify the installation\.

   After Docker is installed, verify that it's working\. Also confirm that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You don't need to install, fetch, or pull any containers—the AWS SAM CLI does this automatically as required\.

If you run into issues installing Docker, see the [Docker installation guide](https://docs.docker.com/engine/installation/#installation) for troubleshooting tips\.

## Step 4: Install the AWS SAM CLI<a name="serverless-sam-cli-install-windows-sam-cli"></a>

Windows Installer \(MSI\) files are the package installer files for the Windows operating system\.

Follow these steps to install the AWS SAM CLI using the MSI file\. 

1. Install the AWS SAM CLI [ 64\-bit](https://github.com/awslabs/aws-sam-cli/releases/latest/download/AWS_SAM_CLI_64_PY3.msi)\.
**Note**  
If you operate on 32\-bit machine, execute the following command: `pip install aws-sam-cli`

1. Verify the installation\.

   After completing the installation, verify it by opening a new command prompt or PowerShell prompt\. You should be able to invoke `sam` from the command line\.

   ```
   sam --version
   ```

   You should see output like the following after successful installation of the AWS SAM CLI:

   ```
    
    SAM CLI, version 0.33.0
   ```

You're now ready to start development\.

## Next Steps<a name="serverless-sam-cli-install-windows-next-steps"></a>

You're now ready to begin building your own serverless applications using AWS SAM\! If you want to start with sample serverless applications, choose one of the following links:
+ [Tutorial: Deploying a Hello World Application](serverless-getting-started-hello-world.md) – Step\-by\-step instructions to download, build, and deploy a simple serverless application\.
+ [AWS SAM example applications in GitHub](https://github.com/awslabs/serverless-application-model/tree/master/examples/apps) – Sample applications in the AWS SAM GitHub repository that you can further experiment with\.