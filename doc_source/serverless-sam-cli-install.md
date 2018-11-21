# Installing the AWS SAM CLI<a name="serverless-sam-cli-install"></a>

The primary distribution method for the AWS SAM CLI on Linux, Windows, and macOS is pip, a package manager for Python that provides an easy way to install, upgrade, and remove Python packages and their dependencies\.

If you want to install AWS SAM CLI using pip, first make sure the prerequisites listed below are met, then follow the instructions in [Install the AWS SAM CLI Using Pip](serverless-sam-cli-install-using-pip.md)\. Otherwise, see the subtopic for your platform for other installation options\.

## Prerequisites<a name="serverless-sam-cli-install-prerequisites"></a>
+ [Docker](https://www.docker.com/)
+ [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/)
+ \(Pip only\) Python 2\.7 or Python 3\.6

**Installing Docker**

You need to have Docker installed and running to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\.

For platform\-specific instructions for installing Docker, see the following:
+ **Linux:** [Docker for Linux](serverless-sam-cli-install-linux.md#serverless-sam-cli-install-linux-docker)
+ **Windows:** [ Docker For Windows](https://www.docker.com/docker-windows)
+ **macOS:** [ Docker for macOS](https://store.docker.com/editions/community/docker-ce-desktop-mac)

Verify that Docker is working, and that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You do not need to install/fetch/pull any containers, because the AWS SAM CLI will do it automatically as required\.

**Installing the AWS CLI**

To install the AWS CLI see [ Installing the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)\.

## Upgrading<a name="serverless-sam-cli-install-upgrading"></a>

You can upgrade `sam` by using pip:

```
$ pip install --user --upgrade aws-sam-cli
```

You must first uninstall previous versions of the AWS SAM CLI \(0\.2\.11 or earlier\)\. Then follow the earlier installation steps\. To uninstall, use this command:

```
$ npm uninstall -g aws-sam-local
```

## Troubleshooting<a name="serverless-sam-cli-install-troubleshooting"></a>

### macOS Issues<a name="serverless-sam-cli-install-troubleshooting-mac"></a>

**TLSV1\_ALERT\_PROTOCOL\_VERSION**

If you get an error similar to the following, then you're probably using the default version of Python that came with your macOS\. This is outdated\. 

```
Could not fetch URL https://pypi.python.org/simple/click/: There was a problem confirming the ssl certificate: [SSL: TLSV1_ALERT_PROTOCOL_VERSION] tlsv1 alert protocol version (_ssl.c:590) - skipping
```

Make sure that you install Python again using Homebrew and try again:

```
$ brew install python
```

After it's installed, then repeat the installation process\.