# AWS SAM CLI troubleshooting<a name="sam-cli-troubleshooting"></a>

Troubleshoot error messages when using, installing, and managing the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\)\.

**Topics**
+ [Troubleshooting installation errors](#sam-cli-troubleshoot-install)

## Troubleshooting installation errors<a name="sam-cli-troubleshoot-install"></a>

### Linux<a name="sam-cli-troubleshoot-install-linux"></a>

#### Docker error: "Cannot connect to the Docker daemon\. Is the docker daemon running on this host?"<a name="serverless-sam-cli-install-linux-troubleshooting-docker-deamon"></a>

In some cases, to provide permissions for the `ec2-user` to access the Docker daemon, you might have to reboot your instance\. If you receive this error, try rebooting your instance\.

#### Shell error: "command not found"<a name="serverless-sam-cli-install-linux-troubleshooting-sam-cli-not-found"></a>

If you receive this error, your shell can't locate the AWS SAM CLI executable in the path\. Verify the location of the directory where you installed the AWS SAM CLI executable, and then verify that the directory is on your path\.

#### AWS SAM CLI error: "/lib64/libc\.so\.6: version `GLIBC\_2\.14' not found \(required by /usr/local/aws\-sam\-cli/dist/libz\.so\.1\)"<a name="serverless-sam-cli-install-linux-troubleshooting-sam-cli-missing-lib"></a>

If you receive this error, you're using an unsupported version of Linux, and the built\-in glibc version is out of date\. Try either of the following:
+ Upgrade your Linux host to the 64\-bit version of a recent distribution of CentOS, Fedora, Ubuntu, or Amazon Linux 2\.
+ Follow the instructions for [Installing the AWS SAM CLI](install-sam-cli.md)\.

### macOS<a name="sam-cli-troubleshoot-install-macos"></a>

#### The installation failed<a name="sam-cli-troubleshoot-install-macos-install-failed"></a>

![\[Image of the AWS SAM CLI installer showing an installation failed message\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/images/sam-cli-troubleshoot-install-macos-install-failed.jpg)

 If you are installing the AWS SAM CLI for your user and selected an installation directory that you don’t have write permissions for, this error could occur\. Try either of the following: 

1.  Select a different installation directory that you have write permissions for\. 

1.  Delete the installer\. Then, download and run it again\. 