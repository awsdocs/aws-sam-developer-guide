# Installing the AWS SAM CLI on Linux<a name="serverless-sam-cli-install-linux"></a>

The following steps help you to install and configure the required prerequisites for using the AWS SAM CLI on your Linux host:

1. Create an AWS account\.

1. Configure IAM permissions\.

1. Install Docker\. Note: Docker is only a prerequisite for testing your application locally\.

1. Install Homebrew\.

1. Install the AWS SAM CLI\.

**Note**  
These instructions cause your environment's default Python version to be the one installed by Homebrew\. The change in default Python version occurs in [Step 4: Install Homebrew](#serverless-sam-cli-install-linux-homebrew)\.

## Step 1: Create an AWS account<a name="serverless-sam-cli-install-linux-aws-account"></a>

If you don't already have an AWS account, see [aws\.amazon\.com](https://aws.amazon.com/) and choose **Create an AWS Account**\. For detailed instructions, see [Create and Activate an AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)\.

## Step 2: Create an IAM user with administrator permissions<a name="serverless-sam-cli-install-linux-iam-permissions"></a>

If you don't already have an IAM user with administrator permissions, see [Creating Your First IAM Admin User and Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

In addition, you must set up AWS credentials to enable the AWS SAM CLI to make AWS service calls\. For example, the AWS SAM CLI makes calls to Amazon S3 and AWS CloudFormation\. For more information about setting up AWS credentials, see [Setting up AWS credentials](serverless-getting-started-set-up-credentials.md)\.

## Step 3: Install Docker<a name="serverless-sam-cli-install-linux-docker"></a>

**Note**  
Docker is only a prerequisite for testing your application locally and to build deployment packages using the `--use-container` flag\. You may skip this section or install Docker at a later time if you do not plan to use these features initially\.

Docker is an application that runs containers on your Linux machines\. AWS SAM provides a local environment that's similar to AWS Lambda to use as a Docker container\. You can use this container to build, test, and debug your serverless applications\.

You must have Docker installed and working to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\. The following steps describe how to install, configure, and verify a Docker installation to work with the AWS SAM CLI\.

Docker is available on many different operating systems, including most modern Linux distributions, like CentOS, Debian, Ubuntu, etc\. For more information about how to install Docker on your particular operating system, go to the [Docker installation guide](https://docs.docker.com/install/)\.

If you are using Amazon Linux 2, follow these steps to install Docker:

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

1. Add the `ec2-user` to the `docker` group so you can execute Docker commands without using `sudo`\.

   ```
   sudo usermod -a -G docker ec2-user
   ```

1. Log out and log back in again to pick up the new `docker` group permissions\. You can accomplish this by closing your current SSH terminal window and reconnecting to your instance in a new one\. Your new SSH session will have the appropriate `docker` group permissions\.

1. Verify that the `ec2-user` can run Docker commands without `sudo`\.

   ```
   docker ps
   ```

   You should see the following output, showing Docker is installed and running:

   ```
    
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
   ```
**Note**  
In some cases, you may need to reboot your instance to provide permissions for the `ec2-user` to access the Docker daemon\. Try rebooting your instance if you see the following error:  

   ```
   Cannot connect to the Docker daemon. Is the docker daemon running on this host?
   ```

If you run into issues installing Docker, see the [Troubleshooting](#serverless-sam-cli-install-linux-troubleshooting) section later in this guide, or the [Troubleshooting](https://docs.docker.com/install/linux/linux-postinstall/#troubleshooting) section of the *Docker installation guide* for additional troubleshooting tips\.

## Step 4: Install Homebrew<a name="serverless-sam-cli-install-linux-homebrew"></a>

**Note**  
This step causes your environment's default Python version to be the one installed by Homebrew\.

The recommended approach for installing the AWS SAM CLI on Linux is to use the Homebrew package manager\. For more information about Homebrew, see [Homebrew Documentation](https://docs.brew.sh/Homebrew-on-Linux)\.

To install Homebrew, you must first install Git\. For more information about Git, see [Git Documentation](https://git-scm.com)\. Git is available on many different operating systems, including most modern Linux distributions\. For instructions about installing Git on your particular operating system, see [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)\.

Once you have successfully installed Git, run the following to install Homebrew:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Next, add Homebrew to your PATH by running the following commands\. These commands work on all major flavors of Linux by adding either `~/.profile` on Debian/Ubuntu or `~/.bash_profile` on CentOS/Fedora/RedHat:

```
test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile
```

Verify that Homebrew is installed:

```
brew --version
```

You should see output like the following on successful installation of Homebrew:

```
 
 Homebrew 2.1.6 
 Homebrew/homebrew-core (git revision ef21; last commit 2019-06-19)
```

## Step 5: Install the AWS SAM CLI<a name="serverless-sam-cli-install-linux-sam-cli"></a>

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

## Upgrading<a name="serverless-sam-cli-install-linux-upgrading"></a>

To upgrade the AWS SAM CLI, you still use Homebrew, but replace `install` with `upgrade` as follows:

```
brew upgrade aws-sam-cli
```

## Troubleshooting<a name="serverless-sam-cli-install-linux-troubleshooting"></a>

### Docker error: "Cannot connect to the Docker daemon\. Is the docker daemon running on this host?"<a name="serverless-sam-cli-install-linux-troubleshooting-docker-deamon"></a>

In some cases, you may need to reboot your instance to provide permissionst for the `ec2-user` to access the Docker daemon\. If you receive this error, try rebooting your instance\.

### Shell error: "command not found"<a name="serverless-sam-cli-install-linux-troubleshooting-sam-cli-not-found"></a>

Your shell is not able to locate the AWS SAM CLI executable in the path\. If you receive this error, verify the location of directory where the AWS SAM CLI executable was installed, and verify that directory is on your path\.

For example, if you used the instructions in this topic to both 1\) Install Homebrew, and 2\) Use Homebrew to install the AWS SAM CLI, then the AWS SAM CLI executable will be installed to the following location:

```
  
 /home/linuxbrew/.linuxbrew/bin/sam
```

### Error: "AWS SAM CLI no longer supports installations on Python 2\.7\."<a name="serverless-sam-cli-install-linux-troubleshooting-sam-cli-old-python"></a>

Your system is using an old installation of Python that is not compatible with the AWS SAM CLI\. If you receive this error, follow the instructions in [Installing the AWS SAM CLI on Linux](#serverless-sam-cli-install-linux) to install a version of Python compatible with the AWS SAM CLI\.

## Next steps<a name="serverless-sam-cli-install-linux-next-steps"></a>

You're now ready to begin building your own serverless applications using AWS SAM\! If you want to start with sample serverless applications, choose one of the following links:
+ [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md) – Step\-by\-step instructions to download, build, and deploy a simple serverless application\.
+ [AWS SAM example applications in GitHub](https://github.com/aws-samples/serverless-app-examples) – Sample applications in the AWS SAM GitHub repository that you can further experiment with\.