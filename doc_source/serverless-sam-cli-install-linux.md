# Installing the AWS SAM CLI on Linux<a name="serverless-sam-cli-install-linux"></a>

The AWS SAM command line interface \(CLI\) is supported on 64\-bit versions of recent distributions of CentOS, Fedora, Ubuntu, and Amazon Linux 2\. To install the AWS SAM CLI, you must extract or "unzip" the downloaded package\. If your operating system doesn't have the built\-in unzip command, use an equivalent\.

To install and configure the prerequisites for using the AWS SAM CLI on your Linux host, follow these steps:

1. Create an AWS account\.

1. Configure AWS Identity and Access Management \(IAM\) permissions and AWS credentials\.

1. Install Docker\. **Note:** Docker is a prerequisite only for testing your application locally or using the `--use-container` option\.

1. Install the AWS SAM CLI\.

## Step 1: Create an AWS account<a name="serverless-sam-cli-install-linux-aws-account"></a>

If you don't already have an AWS account, see [aws\.amazon\.com](https://aws.amazon.com/) and choose **Create an AWS Account**\. For detailed instructions, see [How do I create and activate a new AWS account?](http://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)

## Step 2: Configure IAM permissions and AWS credentials<a name="serverless-sam-cli-install-linux-iam-permissions"></a>

The IAM user that you use with AWS SAM must have sufficient permissions to make necessary AWS service calls and manage AWS resources\. The simplest way to ensure that a user has sufficient permissions is to grant administrator privileges to them\. For more information, see [Creating your first IAM admin user and group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

**Note**  
If you don't want to grant administrator privileges to users who use the AWS Command Line Interface \(AWS CLI\), you can grant restricted sets of permissions to them\. For more information, see [Permissions](sam-permissions.md)\.

In addition, to enable the AWS SAM CLI to make AWS service calls, you must set up AWS credentials\. For more information, see [Setting up AWS credentials](serverless-getting-started-set-up-credentials.md)\.

## Step 3: Install Docker \(optional\)<a name="serverless-sam-cli-install-linux-docker"></a>

**Note**  
Docker is a prerequisite only for testing your application locally and for building deployment packages using the \-\-use\-container option\. If you don't plan to use these features initially, you can skip this section or install Docker at a later time\.

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

1. Add the `ec2-user` to the `docker` group so that you can run Docker commands without using sudo\.

   ```
   sudo usermod -a -G docker ec2-user
   ```

1. Pick up the new `docker` group permissions by logging out and logging back in again\. To do this, close your current SSH terminal window and reconnect to your instance in a new one\. Your new SSH session should have the appropriate `docker` group permissions\.

1. Verify that the `ec2-user` can run Docker commands without using sudo\.

   ```
   docker ps
   ```

   You should see the following output, confirming that Docker is installed and running:

   ```
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
   ```

**Note**  
On Linux, to build and run Lambda functions with a different instruction set architecture than your host machine, you must take additional steps to configure Docker\. For example, to run `arm64` functions on an `x86_64` machine, you can run the following command to configure the Docker daemon: `docker run --rm --privileged multiarch/qemu-user-static --reset -p yes`\.

If you run into issues installing Docker, see the [Troubleshooting](#serverless-sam-cli-install-linux-troubleshooting) section later in this guide\. Or, see the [Troubleshooting](https://docs.docker.com/engine/install/linux-postinstall/#troubleshooting) section of **Post\-installation steps for Linux** on the Docker Docs website\.

## Step 4: Install the AWS SAM CLI<a name="serverless-sam-cli-install-linux-sam-cli"></a>

To install the AWS SAM CLI, on follow these steps:

------
#### [ x86\_64  ]

1. Download the [AWS SAM CLI zip file](https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-linux-x86_64.zip) to a directory of your choice\.

1. Verify the integrity and authenticity of the downloaded installer files by generating a hash value using the following command:

   ```
   sha256sum aws-sam-cli-linux-x86_64.zip
   ```

   The output should look like the following example:

   ```
    <64-character SHA256 hash value> aws-sam-cli-linux-x86_64.zip
   ```

   Compare the 64\-character SHA256 hash value with the one for your desired AWS SAM CLI version in the [AWS SAM CLI release notes](https://github.com/aws/aws-sam-cli/releases/latest) on GitHub\.

1. Unzip the installation files into the `sam-installation/` subdirectory\.

   ```
   unzip aws-sam-cli-linux-x86_64.zip -d sam-installation
   ```

1. Install the AWS SAM CLI\.

   ```
   sudo ./sam-installation/install
   ```

1. Verify the installation\.

   ```
   sam --version
   ```

   On successful installation, you should see output like the following:

   ```
    SAM CLI, version 1.18.0
   ```

------
#### [ ARM ]

1. Use `pip` to install the AWS SAM CLI\.

   ```
   pip install aws-sam-cli
   ```

1. Verify the installation\.

   ```
   sam --version
   ```

   On successful installation, you should see output like the following:

   ```
    SAM CLI, version 1.18.0
   ```

------

You're now ready to start development\.

## Upgrading<a name="serverless-sam-cli-install-linux-upgrading"></a>

To upgrade the AWS SAM CLI, perform the same steps as in the **Install the AWS SAM CLI** section earlier in this topic, but add the \-\-update option to the install command, as follows:

```
sudo ./sam-installation/install --update
```

## Uninstalling<a name="serverless-sam-cli-install-linux-uninstalling"></a>

To uninstall the AWS SAM CLI, you must delete the symlink and installation directory by running the following commands:

1. Locate the symlink and install paths\.
   + Find the symlink using the which command:

     ```
     which sam
     ```

     The output shows the path where the AWS SAM binaries are located, for example:

     ```
      /usr/local/bin/sam
     ```
   + Find the directory that the symlink points to using the ls command:

     ```
     ls -l /usr/local/bin/sam
     ```

     In the following example, the installation directory is `/usr/local/aws-sam-cli`\.

     ```
      lrwxrwxrwx 1 ec2-user ec2-user 49 Oct 22 09:49 /usr/local/bin/sam -> /usr/local/aws-sam-cli/current/bin/sam
     ```

1. Delete the symlink\.

   ```
   sudo rm /usr/local/bin/sam
   ```

1. Delete the installation directory\.

   ```
   sudo rm -rf /usr/local/aws-sam-cli
   ```

## Nightly build<a name="serverless-sam-cli-install-linux-nightly-build"></a>

A nightly build of the AWS SAM CLI is available for you to install\. Once installed, you can use the nightly build using the `sam-nightly` command\. You can install and use both the production and nightly build versions of the AWS SAM CLI at the same time\.

The nightly build contains a pre\-release version of AWS SAM CLI code that may be less stable than the production version\. Note that the nightly build does not contain pre\-release version of the build image, so building a serverless application with the `--use-container` option uses the latest production version of the build image\.

The nightly build is available with this download link: [AWS SAM CLI nightly build](https://github.com/aws/aws-sam-cli/releases/download/sam-cli-nightly/aws-sam-cli-linux-x86_64.zip)\. To install the nightly build version of the AWS SAM CLI, perform the same steps as in the [Step 4: Install the AWS SAM CLI](#serverless-sam-cli-install-linux-sam-cli) section earlier in this topic, but use the nightly build download link instead\. You can find the hash values for the nightly build installer files in the [AWS SAM CLI release notes for nightly builds](https://github.com/aws/aws-sam-cli/releases/tag/sam-cli-nightly) on GitHub\.

To verify you have installed the nightly build version, run the `sam-nightly --version` command\. The output of this command is in the form `1.X.Y.dev<YYYYMMDDHHmm>`, for example:

```
SAM CLI, version 1.20.0.dev202103151200
```

## Troubleshooting<a name="serverless-sam-cli-install-linux-troubleshooting"></a>

### Docker error: "Cannot connect to the Docker daemon\. Is the docker daemon running on this host?"<a name="serverless-sam-cli-install-linux-troubleshooting-docker-deamon"></a>

In some cases, to provide permissions for the `ec2-user` to access the Docker daemon, you might have to reboot your instance\. If you receive this error, try rebooting your instance\.

### Shell error: "command not found"<a name="serverless-sam-cli-install-linux-troubleshooting-sam-cli-not-found"></a>

If you receive this error, your shell can't locate the AWS SAM CLI executable in the path\. Verify the location of the directory where you installed the AWS SAM CLI executable, and then verify that the directory is on your path\.

### AWS SAM CLI error: "/lib64/libc\.so\.6: version `GLIBC\_2\.14' not found \(required by /usr/local/aws\-sam\-cli/dist/libz\.so\.1\)"<a name="serverless-sam-cli-install-linux-troubleshooting-sam-cli-missing-lib"></a>

If you receive this error, you're using an unsupported version of Linux, and the built\-in glibc version is out of date\. Try either of the following:
+ Upgrade your Linux host to the 64\-bit version of a recent distribution of CentOS, Fedora, Ubuntu, or Amazon Linux 2\.
+ Follow the instructions for [Installing the AWS SAM CLI on Linux using Homebrew](sam-cli-install-linux-alt.md)\.

## Next steps<a name="serverless-sam-cli-install-linux-next-steps"></a>

You're now ready to begin building your own serverless applications using AWS SAM\. To start with a sample serverless application, choose one of the following links:
+ [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md) – Step\-by\-step instructions to download, build, and deploy a simple serverless application\.
+ [AWS SAM example applications in GitHub](https://github.com/aws-samples/serverless-app-examples) – Sample applications in the AWS SAM GitHub repository that you can further experiment with\.