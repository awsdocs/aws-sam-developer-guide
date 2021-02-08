# Installing the AWS SAM CLI on Linux<a name="serverless-sam-cli-install-linux"></a>

Follow these steps to install and configure the prerequisites for using the AWS SAM command line interface \(CLI\) on your Linux host:

1. Create an AWS account\.

1. Configure AWS Identity and Access Management \(IAM\) permissions and AWS credentials\.

1. Install Docker\. **Note:** Docker is a prerequisite only for testing your application locally\.

1. Install Homebrew\.

1. Install the AWS SAM CLI\.

**Note**  
Following these instructions changes your environment's default Python version to the one that Homebrew installs\. This change occurs in [Step 4: Install Homebrew](#serverless-sam-cli-install-linux-homebrew)\.

## Step 1: Create an AWS account<a name="serverless-sam-cli-install-linux-aws-account"></a>

If you don't already have an AWS account, see [aws\.amazon\.com](https://aws.amazon.com/) and choose **Create an AWS Account**\. For detailed instructions, see [How do I create and activate a new AWS account?](http://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)

## Step 2: Configure IAM permissions and AWS credentials<a name="serverless-sam-cli-install-linux-iam-permissions"></a>

The IAM user that you use with AWS SAM must have sufficient permissions to make necessary AWS service calls and manage AWS resources\. The simplest way to ensure that a user has sufficient permissions is to grant administrator privileges to them\. For more information, see [Creating your first IAM admin user and group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

**Note**  
If you don't want to grant administrator privileges to users who use the AWS Command Line Interface \(AWS CLI\), you can grant restricted sets of permissions to them\. For more information, see [Permissions](sam-permissions.md)\.

In addition, to enable the AWS SAM CLI to make AWS service calls, you must set up AWS credentials\. For more information, see [Setting up AWS credentials](serverless-getting-started-set-up-credentials.md)\.

## Step 3: Install Docker<a name="serverless-sam-cli-install-linux-docker"></a>

**Note**  
Docker is a prerequisite only for testing your application locally and for building deployment packages using the `--use-container` flag\. If you don't plan to use these features initially, you can skip this section or install Docker at a later time\.

Docker is an application that runs containers on your Linux machines\. AWS SAM provides a local environment that's similar to AWS Lambda to use as a Docker container\. You can use this container to build, test, and debug your serverless applications\.

To run serverless projects and functions locally with the AWS SAM CLI, you must have Docker installed and working\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\. The following steps describe how to install, configure, and verify a Docker installation to work with the AWS SAM CLI\.

Docker is available on many different operating systems, including most modern Linux distributions, for example, CentOS, Debian, and Ubuntu\. For information about installing Docker on your particular operating system, see [Get Docker](https://docs.docker.com/get-docker/) on the Docker Docs website\.

If you're using Amazon Linux 2, follow these steps to install Docker:

1. Update the installed packages and package cache on your instance\.

   ```
   sudo yum update -y
   ```

1. Install the most recent Docker Community Edition package\.

   ```
   sudo amazon-linux-extras install docker
   ```

1. Start the Docker service\.

   ```
   sudo service docker start
   ```

1. Add the `ec2-user` to the `docker` group so that you can run Docker commands without using `sudo`\.

   ```
   sudo usermod -a -G docker ec2-user
   ```

1. Log out and log back in again to pick up the new `docker` group permissions\. You can do this by closing your current SSH terminal window and reconnecting to your instance in a new one\. Your new SSH session will have the appropriate `docker` group permissions\.

1. Verify that the `ec2-user` can run Docker commands without using `sudo`\.

   ```
   docker ps
   ```

   You should see the following output, confirming that Docker is installed and running:

   ```
    
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
   ```

If you run into issues installing Docker, see the [Troubleshooting](#serverless-sam-cli-install-linux-troubleshooting) section later in this guide\. Or, see the [Troubleshooting](https://docs.docker.com/engine/install/linux-postinstall/#troubleshooting) section of **Post\-installation steps for Linux** on the Docker Docs website\.

## Step 4: Install Homebrew<a name="serverless-sam-cli-install-linux-homebrew"></a>

**Note**  
This step changes your environment's default Python version to the one that Homebrew installs\.

To install the AWS SAM CLI on Linux, we recommend using the Homebrew package manager\. For more information about Homebrew, see [Homebrew on Linux](https://docs.brew.sh/Homebrew-on-Linux) on the Homebrew Documentation website\.

To install Homebrew, you must first install Git\. Git is available on many different operating systems, including most modern Linux distributions\. For instructions about installing Git on your particular operating system, see [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) on the Git website\.

After successfully installing Git, to install Homebrew, run the following command:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Next, add Homebrew to your PATH by running the following commands\. These commands work on all major flavors of Linux by adding either `~/.profile` on Debian and Ubuntu, or `~/.bash_profile` on CentOS, Fedora, and RedHat\.

```
test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile
```

Verify that Homebrew is installed\.

```
brew --version
```

On successful installation of Homebrew, you should see output like the following:

```
 
 Homebrew 2.1.6 
 Homebrew/homebrew-core (git revision ef21; last commit 2019-06-19)
```

## Step 5: Install the AWS SAM CLI<a name="serverless-sam-cli-install-linux-sam-cli"></a>

To install the AWS SAM CLI using Homebrew, run the following commands:

```
brew tap aws/tap
brew install aws-sam-cli
```

Verify the installation\.

```
sam --version
```

On successful installation of the AWS SAM CLI, you should see output like the following:

```
 
 SAM CLI, version 1.15.0
```

You're now ready to start development\.

## Upgrading<a name="serverless-sam-cli-install-linux-upgrading"></a>

To upgrade the AWS SAM CLI, you still use Homebrew, but replace `install` with `upgrade` as follows:

```
brew upgrade aws-sam-cli
```

## Troubleshooting<a name="serverless-sam-cli-install-linux-troubleshooting"></a>

### Docker error: "Cannot connect to the Docker daemon\. Is the docker daemon running on this host?"<a name="serverless-sam-cli-install-linux-troubleshooting-docker-deamon"></a>

In some cases, to provide permissions for the `ec2-user` to access the Docker daemon, you might need to reboot your instance\. If you receive this error, try rebooting your instance\.

### Shell error: "command not found"<a name="serverless-sam-cli-install-linux-troubleshooting-sam-cli-not-found"></a>

If you receive this error, your shell is unable to locate the AWS SAM CLI executable in the path\. Verify the location of the directory where you installed the AWS SAM CLI executable, and then verify that the directory is on your path\.

For example, if you used the instructions in this topic to both install Homebrew and use Homebrew to install the AWS SAM CLI, then the AWS SAM CLI executable is installed to the following location:

```
  
 /home/linuxbrew/.linuxbrew/bin/sam
```

### Installing Homebrew message: "Enter your password to install to /home/linuxbrew/\.linuxbrew"<a name="serverless-sam-cli-install-linux-troubleshooting-homebrew-enter-password"></a>

During **Step 4: Install Homebrew**, by default you are prompted to provide a password\. However, you may not want to set up a password for the current user, for example when you are setting up a non\-interactive environment like CI/CD systems\.

If you do not want to set up a password for the current user, you can install Homebrew in non\-interactive mode by setting the environmentment variable `CI=1`\. For example:

```
CI=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

### Installing AWS SAM CLI error: "The following formulae cannot be installed from bottles and must be built from source\. pkg\-config, gdbm, openssl@1\.1, ncurses, xz and python@3\.8<a name="serverless-sam-cli-install-linux-troubleshooting-build-from-sourced"></a>

During **Step 5: Install the AWS SAM CLI**, if you see this error, it is because you don't have the `gcc` module installed\. Installing the gcc module depends on your Linux distribution, as follows:

```
# for Amazon Linux, Amazon Linux 2, CentOS and RedHat:
sudo yum install gcc
# for Debian and Ubuntu:
sudo apt-get update
sudo apt-get install gcc
```

After installing the `gcc` module, run the commands in **Step 5: Install the AWS SAM CLI** again\.

## Next steps<a name="serverless-sam-cli-install-linux-next-steps"></a>

You're now ready to begin building your own serverless applications using AWS SAM\. To start with a sample serverless application, choose one of the following links:
+ [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md) – Step\-by\-step instructions to download, build, and deploy a simple serverless application\.
+ [AWS SAM example applications in GitHub](https://github.com/aws-samples/serverless-app-examples) – Sample applications in the AWS SAM GitHub repository that you can further experiment with\.