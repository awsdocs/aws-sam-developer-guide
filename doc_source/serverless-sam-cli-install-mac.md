# Installing the AWS SAM CLI on macOS<a name="serverless-sam-cli-install-mac"></a>

To install the AWS SAM CLI on macOS, first make sure that you've installed the [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) and [Docker for macOS](#serverless-sam-cli-install-mac-docker)\.

## Docker for macOS<a name="serverless-sam-cli-install-mac-docker"></a>

You need to have Docker installed and running to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\.

To install Docker on macOS, see [Docker for macOS](https://store.docker.com/editions/community/docker-ce-desktop-mac)\.

**Note**  
For macOS users: The AWS SAM CLI requires that the project directory \(or any parent directory\) is listed in [Docker File System Sharing](https://docs.docker.com/docker-for-mac/osxfs/)\.

Verify that Docker is working, and that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You don't need to install/fetch/pull any containers because the AWS SAM CLI does it automatically, as required\.

## Install the AWS SAM CLI Using Homebrew<a name="serverless-sam-cli-install-mac-homebrew"></a>

Follow these steps to install the AWS SAM CLI by using Homebrew:

1. To install the Homebrew package manager, follow the instructions on the [ Homebrew website](http://brew.sh/) \.

1. Upgrade Homebrew, and update it to the latest version\.

   ```
   brew upgrade
   brew update
   ```

1. Add a brew tap from [GitHub](https://github.com/aws/homebrew-tap)\.

   ```
   brew tap aws/tap
   ```

1. Install aws\-sam\-cli from the brew tap\.

   ```
   brew install aws-sam-cli
   ```

Now sam is installed to following location:

```
/usr/local/bin/sam
```

You should be able to invoke sam from the command line\.

```
sam --version
```

## Install the AWS SAM CLI Using Pip<a name="serverless-sam-cli-install-mac-pip"></a>

An alternate method of installing the AWS SAM CLI is by using pip\. For details on how to do this, see [Installing Using Pip](serverless-sam-cli-install-additional.md#serverless-sam-cli-install-using-pip)\.

## Troubleshooting<a name="serverless-sam-cli-install-troubleshooting-mac"></a>

**TLSV1\_ALERT\_PROTOCOL\_VERSION**

If you get an error similar to the following, then you're probably using the default version of Python that came with your macOS\. This is outdated\. 

```
Could not fetch URL https://pypi.python.org/simple/click/: There was a problem confirming the ssl certificate: [SSL: TLSV1_ALERT_PROTOCOL_VERSION] tlsv1 alert protocol version (_ssl.c:590) - skipping
```

Make sure that you install Python again using Homebrew, and try again:

```
$ brew install python
```

After it's installed, repeat the installation process\.
