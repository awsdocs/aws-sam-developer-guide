# Setting up AWS credentials<a name="serverless-getting-started-set-up-credentials"></a>

The AWS SAM command line interface \(CLI\) requires you to set AWS credentials so that it can make calls to AWS services on your behalf\. For example, the AWS SAM CLI makes calls to Amazon S3 and AWS CloudFormation\.

You might have already set AWS credentials to work with AWS tools, like one of the AWS SDKs or the AWS CLI\. If you haven't, this topic shows you the recommended approaches for setting AWS credentials\.

To set AWS credentials, you must have the *access key ID* and your *secret access key* for the IAM user you want to configure\. For information about access key IDs and secret access keys, see [Managing Access Keys for IAM Users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) in the *IAM User Guide*\.

Next, determine whether you have the AWS CLI installed\. Then follow the instructions in one of the following sections:

## Using the AWS CLI<a name="serverless-getting-started-set-up-credentials-cli"></a>

If you have the AWS CLI installed, use the **aws configure** command and follow the prompts:

```
$ aws configure
AWS Access Key ID [None]: your_access_key_id
AWS Secret Access Key [None]: your_secret_access_key
Default region name [None]: 
Default output format [None]:
```

For information about the **aws configure** command, see [Quickly Configuring the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html#cli-quick-configuration) in the *AWS Command Line Interface User Guide*\.

## Not using the AWS CLI<a name="serverless-getting-started-set-up-credentials-no-cli"></a>

If you don't have the AWS CLI installed, you can either create a credentials file or set environment variables:
+ **Credentials file** – You can set credentials in the AWS credentials file on your local system\. This file must be located in one of the following locations:
  + `~/.aws/credentials` on Linux or macOS
  + `C:\Users\USERNAME\.aws\credentials` on Windows

  This file should contain lines in the following format:

  ```
  [default]
  aws_access_key_id = your_access_key_id
  aws_secret_access_key = your_secret_access_key
  ```

   
+ **Environment variables** – You can set the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables\.

  To set these variables on Linux or macOS, use the **export** command:

  ```
  export AWS_ACCESS_KEY_ID=your_access_key_id
  export AWS_SECRET_ACCESS_KEY=your_secret_access_key
  ```

  To set these variables on Windows, use the **set** command:

  ```
  set AWS_ACCESS_KEY_ID=your_access_key_id
  set AWS_SECRET_ACCESS_KEY=your_secret_access_key
  ```