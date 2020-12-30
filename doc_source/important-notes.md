# Important notes<a name="important-notes"></a>

This section contains important notes and known issues for AWS Serverless Application Model\.

## Installing AWS SAM CLI on 32\-bit Windows<a name="important-notes-32-bit-windows"></a>

Support for AWS SAM CLI on 32\-bit Windows will soon be deprecated\. If you operate on a 32\-bit system, we recommend that you upgrade to a 64\-bit system and follow the instructions found in [Installing the AWS SAM CLI on Windows](serverless-sam-cli-install-windows.md)\.

If you cannot upgrade to a 64\-bit system, you can use the [Legacy Docker Toolbox](https://docs.docker.com/toolbox/overview/) with AWS SAM CLI on a 32\-bit system\. However, this will cause you to encounter certain limitations with the AWS SAM CLI\. For example, you cannot run 64\-bit Docker containers on a 32\-bit system\. So, if your Lambda function depends on a 64\-bit natively compiled container, you will not be able to test it locally on a 32\-bit system\.

To install AWS SAM CLI on a 32\-bit system, execute the following command:

```
pip install aws-sam-cli
```

**Important**  
Although the `pip install aws-sam-cli` command also works on 64\-bit Windows, we recommend that you use the [64\-bit MSI](https://github.com/aws/aws-sam-cli/releases/latest/download/AWS_SAM_CLI_64_PY3.msi) to install AWS SAM CLI on 64\-bit systems\.