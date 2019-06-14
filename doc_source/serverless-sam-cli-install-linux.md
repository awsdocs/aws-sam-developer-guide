# Installing the AWS SAM CLI on Linux<a name="serverless-sam-cli-install-linux"></a>

The [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) and Docker are required to install the AWS SAM CLI on Linux\. The following steps describe how to successfully install Docker, and how to install the AWS SAM CLI using either Homebrew or Pip\.

**Topics**
+ [Install Docker for Linux](#serverless-sam-cli-install-linux-docker)
+ [Install the AWS SAM CLI Using Homebrew](#serverless-sam-cli-install-linux-homebrew)
+ [Install the AWS SAM CLI Using Pip](#serverless-sam-cli-install-linux-pip)

## Install Docker for Linux<a name="serverless-sam-cli-install-linux-docker"></a>

Docker is an application that runs containers on your Linux machines\. AWS SAM provides a local environment similar to AWS Lambda to use as a Docker container\. You can use this container to build, test, and debug your Lambda functions\.

You must have Docker installed and working to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\. The following steps describe how to install, configure, and verify a Docker installation to work with the AWS SAM CLI\.

1\. Install Docker\.

Docker supports several common Linux distributions\. Choose your version of Linux for the correct Docker installation steps: 
+ To install Docker for CentOS, see [Get Docker CE for CentOS](https://docs.docker.com/install/linux/docker-ce/centos/)\.
+ To install Docker for Debian, see [Get Docker CE for Debian](https://docs.docker.com/install/linux/docker-ce/debian/)\.
+ To install Docker for Fedora, see [Get Docker CE for Fedora](https://docs.docker.com/install/linux/docker-ce/fedora/)\.
+ To install Docker for Ubuntu, see [Get Docker CE for Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)\.
+ To install Docker for other unsupported platforms, see [Install Docker CE from binaries](https://docs.docker.com/install/linux/docker-ce/binaries/)\.

2\. Verify the installation\.

Verify that Docker is working, and that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You don't need to install, fetch, or pull any containers––the AWS SAM CLI does this automatically as required\.

## Install the AWS SAM CLI Using Homebrew<a name="serverless-sam-cli-install-linux-homebrew"></a>

Homebrew is a package manager available for Linux\. Homebrew is required for this installation\.

Follow these steps to install the AWS SAM CLI using Homebrew:

1. To install the Homebrew package manager, see [Homebrew on Linux](https://docs.brew.sh/Homebrew-on-Linux)\.

1. Add a brew tap from [GitHub](https://github.com/aws/homebrew-tap)\.

   ```
   brew tap aws/tap
   ```

1. Install aws\-sam\-cli from the brew tap\.

   ```
   brew install aws-sam-cli
   ```

1. Verify `sam` is installed to the following location\.

   ```
   /home/homebrew/.homebrew/bin/sam
   ```

1. Verify the installation\. You should be able to invoke `sam` from the command line\.

   ```
   sam --version
   ```

## Install the AWS SAM CLI Using Pip<a name="serverless-sam-cli-install-linux-pip"></a>

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