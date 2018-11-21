# Installing AWS SAM CLI on macOS<a name="serverless-sam-cli-install-mac"></a>

You can install the AWS SAM CLI on macOS using pip, a package manager for Python, or using Homebrew\. For instructions on installing AWS SAM CLI using pip, see [Installing the AWS SAM CLI](serverless-sam-cli-install.md)\. For instructions on installing AWS SAM CLI using Homebrew see [Install the AWS SAM CLI Using Homebrew](#serverless-sam-cli-install-mac-homebrew) below\.

## Docker for macOS<a name="serverless-sam-cli-install-mac-docker"></a>

You need to have Docker installed and running to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\.

To install Docker on macOS, see [Docker for macOS](https://store.docker.com/editions/community/docker-ce-desktop-mac)\.

**Note**  
For macOS users: The AWS SAM CLI requires that the project directory \(or any parent directory\) is listed in [Docker File System Sharing](https://docs.docker.com/docker-for-mac/osxfs/)\.

Verify that Docker is working, and that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You do not need to install/fetch/pull any containers, because the AWS SAM CLI will do it automatically as required\.

## Install the AWS SAM CLI Using Homebrew<a name="serverless-sam-cli-install-mac-homebrew"></a>

**Prerequisites**
+ [Docker for macOS](https://store.docker.com/editions/community/docker-ce-desktop-mac)
+ [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)

**Steps**

1. Follow the instructions on the [ Homebrew website](http://brew.sh/) to install the Homebrew package manager\.

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
/usr/local/bin/sam
```

You should be able to invoke sam from the command line\.

```
sam --version
```