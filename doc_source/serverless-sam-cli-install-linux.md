# Installing the AWS SAM CLI on Linux<a name="serverless-sam-cli-install-linux"></a>

The following steps help you to install and configure the required prerequisites for using the AWS SAM CLI on your Linux host:

1. Create an AWS account\.

1. Configure IAM permissions\.

1. Install the AWS CLI\.

1. Create an Amazon S3 bucket\.

1. Install Docker\. Note: Docker is only a prerequisite for testing your application locally\.

1. Install Homebrew\.

1. Install the AWS SAM CLI\.

## Step 1: Create an AWS Account<a name="serverless-sam-cli-install-linux-aws-account"></a>

If you don't already have an AWS account, see [aws\.amazon\.com](https://aws.amazon.com/) and choose **Create an AWS Account**\. For detailed instructions, see [Create and Activate an AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)\.

## Step 2: Create an IAM User with Administrator Permissions<a name="serverless-sam-cli-install-linux-iam-permissions"></a>

If you don't already have an IAM user with administrator permissions, see [Creating Your First IAM Admin User and Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

## Step 3: Install and Configure the AWS CLI<a name="serverless-sam-cli-install-linux-aws-cli"></a>

If you don't already have the AWS CLI installed, this step shows you how install and configure it\. You can check whether you have the AWS CLI installed by executing `aws --version` at a command line\.

This section has two substeps: a\) Install the AWS CLI using a bundled installer, and b\) Configure the AWS CLI to use your credentials, default AWS Region, and desired output format\.

### Step 3a: Install the AWS CLI<a name="serverless-sam-cli-install-linux-aws-cli-install"></a>

We recommend that you use a bundled installer to avoid issues with existing Python installations when you have multiple versions\.

The following commands assume that you want to install the AWS CLI for all users of a development host using sudo, and that the system default version of Python should be used\. For alternative installation options, see [Installing the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)\.

```
curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
unzip awscli-bundle.zip
sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
```

You should see the following output as the last line of a successful installation:

```
 
 You can now run: /usr/local/bin/aws --version
```

### Step 3b: Configure the AWS CLI<a name="serverless-sam-cli-install-linux-aws-cli-configure"></a>

After you've verified installing the AWS CLI, you can configure it with your credentials, default AWS Region, and desired output format\. To do this, you first create the necessary access keys by following these steps:

1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Users**\.

1. Choose the name of the user whose access keys you want to create, and then choose the **Security credentials** tab\.

1. In the **Access keys** section, choose **Create access key**\.

1. To view the new access key pair, choose **Show**\. You will not have access to the secret access key again after this dialog box closes\. Your credentials will look something like this:
   + Access key ID: AKIAIOSFODNN7EXAMPLE
   + Secret access key: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

1. To download the key pair, choose **Download \.csv file**\. Store the keys in a secure location\. You will not have access to the secret access key again after this dialog box closes\.

   Keep the keys confidential in order to protect your AWS account and never email them\. Do not share them outside your organization, even if an inquiry appears to come from AWS or Amazon\.com\. No one who legitimately represents Amazon will ever ask you for your secret key\.

1. After you download the `.csv` file, choose **Close**\. When you create an access key, the key pair is active by default, and you can use the pair right away\.

Configure the AWS CLI with your using the access keys you just created by executing the following command:

```
aws configure
```

When you're prompted, replace the following examples with your access keys:

```
 
 AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE                         # Enter your access key
 AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY # Enter your secret key
 Default region name [None]: us-east-1                                  # Example regions: us-east-1, ap-east-1, eu-central-1, sa-east-1
 Default output format [None]: json                                     # Or 'text'
```

Additional configuration options are available in [configuring the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)\.

## Step 4: Create an Amazon S3 Bucket<a name="serverless-sam-cli-install-linux-s3-bucket"></a>

AWS SAM uses an Amazon S3 bucket in your AWS account as a repository to store deployment artifacts\. To use the package and deployment functionality of AWS SAM, you must have an Amazon S3 bucket in the Region that you're working in\.

If you need to create an Amazon S3 bucket, you can run the following command:

```
aws s3 mb s3://bucketname --region region # Example regions: us-east-1, ap-east-1, eu-central-1, sa-east-1
```

You should see the following output for a successfully created Amazon S3 bucket:

```
 
 make_bucket: bucketname
```

Remember to keep track of your Amazon S3 bucket name, because you need it to package your serverless application\.

## Step 5: Install Docker<a name="serverless-sam-cli-install-linux-docker"></a>

**Note**  
Docker is only a prerequisite for testing your application locally and to build deployment packages using the `--use-container` flag\. You may skip this section or install Docker at a later time if you do not plan to use these features initially\.

Docker is an application that runs containers on your Linux machines\. AWS SAM provides a local environment that's similar to AWS Lambda to use as a Docker container\. You can use this container to build, test, and debug your serverless applications\.

You must have Docker installed and working to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\. The following steps describe how to install, configure, and verify a Docker installation to work with the AWS SAM CLI\.

Docker is available on many different operating systems, including most modern Linux distributions, like CentOS, Debian, Ubuntu, etc\. For more information about how to install Docker on your particular operating system, go to the [Docker installation guide](https://docs.docker.com/engine/installation/#installation)\.

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

If you run into issues installing Docker, see the [Troubleshooting](#serverless-sam-cli-install-linux-troubleshooting) section later in this guide, or the [Docker installation guide](https://docs.docker.com/engine/installation/#installation) for additional troubleshooting tips\.

## Step 6: Install Homebrew<a name="serverless-sam-cli-install-linux-homebrew"></a>

The recommended approach for installing the AWS SAM CLI on Linux is to use the Homebrew package manager\. For more information about Homebrew, see [Homebrew Documentation](https://docs.brew.sh/Homebrew-on-Linux)\.

To install Homebrew, run the following:

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install.sh)"
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

## Step 7: Install the AWS SAM CLI<a name="serverless-sam-cli-install-linux-sam-cli"></a>

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
 
 SAM CLI, version 0.19.0
```

You're now ready to start development\.

## Troubleshooting<a name="serverless-sam-cli-install-linux-troubleshooting"></a>

### Docker Error: "Cannot connect to the Docker daemon\. Is the docker daemon running on this host?"<a name="serverless-sam-cli-install-linux-troubleshooting-docker-deamon"></a>

In some cases, you may need to reboot your instance to provide permissions for the `ec2-user` to access the Docker daemon\. If you receive this error, try rebooting your instance\.

### Shell error: "command not found"<a name="serverless-sam-cli-install-linux-troubleshooting-sam-cli-not-found"></a>

Your shell is not able to locate the AWS SAM CLI executable in the path\. If you receive this error, verify the location of directory where the AWS SAM CLI executable was installed, and verify that directory is on your path\.

For example, if you used the instructions in this topic to both 1\) Install Homebrew, and 2\) Use Homebrew to install the AWS SAM CLI, then the AWS SAM CLI executable will be installed to the following location:

```
  
 /home/homebrew/.homebrew/bin/sam
```

## Next Steps<a name="serverless-sam-cli-install-linux-next-steps"></a>

You're now ready to begin building your own serverless applications using AWS SAM\! If you want to start with sample serverless applications, choose one of the following links:
+ [Tutorial: Deploying a Hello World Application](serverless-getting-started-hello-world.md) – Step\-by\-step instructions to download, build, and deploy a simple serverless application\.
+ [AWS SAM example applications in GitHub](https://github.com/awslabs/serverless-application-model/tree/master/examples/apps) – Sample applications in the AWS SAM GitHub repository that you can further experiment with\.