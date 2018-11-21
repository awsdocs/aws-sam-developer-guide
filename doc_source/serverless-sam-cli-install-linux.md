# Installing AWS SAM CLI on Linux<a name="serverless-sam-cli-install-linux"></a>

You can install the AWS SAM CLI on Linux using pip, a package manager for Python\. For instructions on installing AWS SAM CLI using pip, see [Installing the AWS SAM CLI](serverless-sam-cli-install.md)\.

## Docker for Linux<a name="serverless-sam-cli-install-linux-docker"></a>

You need to have Docker installed and running to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\.

To install Docker on Linux, check your distro's package manager \(for example, `yum install docker`\)\.

For Centos 7\.5 the requirements are:

```
yum install gcc zip py-pip py-setuptools ca-certificates groff  python-dev g++ make docker epel-release python-pip python-devel\
            python-tools
 # run post install of above
 pip install --upgrade pip
 pip install --upgrade setuptools
 pip install --upgrade aws-sam-cli
```

If you want to use the lambda\-local option \(without running it as root\) you will need to add your user to the docker group

```
usermod -a -G docker yourUserName
```

Verify that Docker is working, and that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You do not need to install/fetch/pull any containers, because the AWS SAM CLI will do it automatically as required\.

## Install the AWS SAM CLI Using Linuxbrew<a name="serverless-sam-cli-install-linux-linuxbrew"></a>

**Prerequisites**
+ **** [Docker for Linux](#serverless-sam-cli-install-linux-docker)
+ [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)

**Steps**

1. Follow the instructions on the [ Linuxbrew website](http://linuxbrew.sh/) to install the Linuxbrew package manager\.

1. Upgrade brew, and update it to the latest version

   ```
   brew upgrade
   brew update
   ```

1. Add a brew tap from `https://github.com/aws/homebrew-tap`\.

   ```
   brew tap aws/tap
   ```

1. Install aws\-sam\-cli from the brew tap\.

   ```
   brew install aws-sam-cli
   ```

Now sam will be installed to following location:

```
/home/linuxbrew/.linuxbrew/bin/sam
```

You should be able to invoke sam from the command line\.

```
sam --version
```