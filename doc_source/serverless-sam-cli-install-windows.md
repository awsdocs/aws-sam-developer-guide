# Installing the AWS SAM CLI on Windows<a name="serverless-sam-cli-install-windows"></a>

The [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) and Docker are required to install the AWS SAM CLI on Windows\. The following steps describe how to successfully install the correct version of Docker, and how to install the AWS SAM CLI using either an MSI file or Pip\. 

**Topics**
+ [Install Docker for Windows](#serverless-sam-cli-install-windows-docker)
+ [Install the AWS SAM CLI Using the MSI File](#serverless-sam-cli-install-windows-msi)
+ [Install the AWS SAM CLI Using Pip](#serverless-sam-cli-install-windows-pip)
+ [Troubleshooting](#serverless-sam-cli-install-troubleshooting-windows)

## Install Docker for Windows<a name="serverless-sam-cli-install-windows-docker"></a>

Docker is an application that runs containers on your Windows or macOS machines\. AWS SAM provides a local environment similar to AWS Lambda to use as a Docker container\. You can use this container to build, test, and debug your Lambda functions\.

You must have Docker installed and working to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\. The following steps describe how to install, configure, and verify a Docker installation to work with the AWS SAM CLI\.

1\. Install Docker\.

Docker Desktop supports the most recent Windows operating system\. For legacy versions of Windows, the Docker Toolbox is available\. Choose your version of Windows for the correct Docker installation steps:
+ To install Docker for Windows 10, see [Install Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/)\.
+ To install Docker for older versions of Windows, see [Install Docker Toolbox on Windows](https://docs.docker.com/toolbox/toolbox_install_windows/)\.

2\. Configure your shared drives\.

The AWS SAM CLI requires that the project directory, or any parent directory, is listed in a shared drive\. Choose your version of Windows below for the correct shared drive instructions:
+ To share drives on Windows 10, see [ Docker Shared Drives](https://docs.docker.com/docker-for-windows/#shared-drives)\.
+ To share drives on older versions of Windows, see [Add Shared Directories](https://docs.docker.com/toolbox/toolbox_install_windows/#optional-add-shared-directories)\.

3\. Verify the installation\.

After Docker is installed, verify that it's working\. Aso confirm that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You don't need to install, fetch, or pull any containers––the AWS SAM CLI does this automatically as required\.

## Install the AWS SAM CLI Using the MSI File<a name="serverless-sam-cli-install-windows-msi"></a>

Windows Installer \(MSI\) files are the package installer files for the Windows operating system\.

Follow these steps to install the CLI using the MSI file\. 

1\. Install the AWS SAM CLI\.

Choose your version of Windows for the correct MSI file:
+ [ 64\-bit](https://github.com/awslabs/aws-sam-cli/releases/latest/download/AWS_SAM_CLI_64_PY3.msi)
+ [ 32\-bit](https://github.com/awslabs/aws-sam-cli/releases/latest/download/AWS_SAM_CLI_32_PY3.msi)

2\. Verify the installation\.

After completing the installation, verify it by opening a new command prompt or PowerShell prompt\. You should be able to invoke `sam` from the command line\.

```
sam --version
```

## Install the AWS SAM CLI Using Pip<a name="serverless-sam-cli-install-windows-pip"></a>

Pip is a package installer for Python\. Python is required for this installation\.

Follow these steps to install the AWS SAM CLI by using pip:

1. Verify that the Python version is 2\.7 or 3\.6\.

   ```
   $ python --version
   ```

   If it isn't installed, [download and install Python](https://www.python.org/downloads/)\.

1. Verify that pip is installed\.

   ```
   $ pip --version
   ```

   If it isn't installed, [download and install pip](https://pip.pypa.io/en/stable/installing/)\.

1. Install `aws-sam-cli`\.

   ```
   pip install --user aws-sam-cli
   ```

1. Adjust your `PATH` to include the Python scripts that are installed under the user's home directory\.
   + **Linux:** [Adjusting Your Path on Linux](serverless-sam-cli-install-linux-path.md)
   + **Windows:** [Adjusting Your Path on Windows](serverless-sam-cli-install-windows-path.md)
   + **macOS:** [Adjusting Your Path on macOS](serverless-sam-cli-install-mac-path.md)

1. Verify that `sam` is installed\.

   Restart or open a new terminal, and verify that the installation worked\.

   ```
   # Restart current shell
   $ sam --version
   ```

## Troubleshooting<a name="serverless-sam-cli-install-troubleshooting-windows"></a>

**Python Not Installed**

If you receive an error similar to the following, you might not have Python installed\.

```
'""' is not recognized as an internal or external command, operable program or batch file.
```

Make sure that you have installed Python, and try again\. To install Python for Windows, see [Python Releases for Windows](https://www.python.org/downloads/windows/)\.