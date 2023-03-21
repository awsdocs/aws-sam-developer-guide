# AWS SAM prerequisites<a name="prerequisites"></a>

Complete the following prerequisites before installing and using the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\)\.

To use the AWS SAM CLI, you need the following:
+ An AWS account, AWS Identity and Access Management \(IAM\) credentials, and an IAM access key pair\.
+ The AWS Command Line Interface \(AWS CLI\) to configure AWS credentials\.

**Topics**
+ [Step 1: Sign up for an AWS account](#prerequisites-sign-up)
+ [Step 2: Create an IAM user account](#prerequisites-create-user)
+ [Step 3: Create an access key ID and secret access key](#prerequisites-create-keys)
+ [Step 4: Install the AWS CLI](#prerequisites-install-cli)
+ [Step 5: Use the AWS CLI to configure AWS credentials](#prerequisites-configure-credentials)
+ [Next steps](#prerequisites-next-steps)

## Step 1: Sign up for an AWS account<a name="prerequisites-sign-up"></a>

If you do not have an AWS account, complete the following steps to create one\.

**To sign up for an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

   When you sign up for an AWS account, an *AWS account root user* is created\. The root user has access to all AWS services and resources in the account\. As a security best practice, [assign administrative access to an administrative user](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html), and use only the root user to perform [tasks that require root user access](https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html)\.

## Step 2: Create an IAM user account<a name="prerequisites-create-user"></a>

To create an administrator user, choose one of the following options\.


****  

| Choose one way to manage your administrator | To | By | You can also | 
| --- | --- | --- | --- | 
| In IAM Identity Center \(Recommended\) | Use short\-term credentials to access AWS\.This aligns with the security best practices\. For information about best practices, see [Security best practices in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-users-federation-idp) in the *IAM User Guide*\. | Following the instructions in [Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) in the AWS IAM Identity Center \(successor to AWS Single Sign\-On\) User Guide\. | Configure programmatic access by [Configuring the AWS CLI to use AWS IAM Identity Center \(successor to AWS Single Sign\-On\)](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html) in the AWS Command Line Interface User Guide\. | 
| In IAM \(Not recommended\) | Use long\-term credentials to access AWS\. | Following the instructions in [Creating your first IAM admin user and user group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the IAM User Guide\. | Configure programmatic access by [Managing access keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) in the IAM User Guide\. | 

## Step 3: Create an access key ID and secret access key<a name="prerequisites-create-keys"></a>

For CLI access, you need an access key ID and a secret access key\. Use temporary credentials instead of long\-term access keys when possible\. Temporary credentials include an access key ID, a secret access key, and a security token that indicates when the credentials expire\. For more information, see [Best practices for managing AWS access keys](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html) in the *AWS General Reference*\.

Users need programmatic access if they want to interact with AWS outside of the AWS Management Console\. The way to grant programmatic access depends on the type of user that's accessing AWS:
+ If you manage identities in IAM Identity Center, the AWS APIs require a profile, and the AWS Command Line Interface requires a profile or an environment variable\.
+ If you have IAM users, the AWS APIs and the AWS Command Line Interface require access keys\. Whenever possible, create temporary credentials that consist of an access key ID, a secret access key, and a security token that indicates when the credentials expire\.

To grant users programmatic access, choose one of the following options\.


****  

| Which user needs programmatic access? | To | By | 
| --- | --- | --- | 
|  Workforce identity \(Users managed in IAM Identity Center\)  | Use short\-term credentials to sign programmatic requests to the AWS CLI or AWS APIs \(directly or by using the AWS SDKs\)\. |  Following the instructions for the interface that you want to use: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/prerequisites.html)  | 
| IAM | Use short\-term credentials to sign programmatic requests to the AWS CLI or AWS APIs \(directly or by using the AWS SDKs\)\. | Following the instructions in [Using temporary credentials with AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_use-resources.html) in the IAM User Guide\. | 
| IAM | Use long\-term credentials to sign programmatic requests to the AWS CLI or AWS APIs \(directly or by using the AWS SDKs\)\.\(Not recommended\) | Following the instructions in [Managing access keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) in the IAM User Guide\. | 

## Step 4: Install the AWS CLI<a name="prerequisites-install-cli"></a>

The AWS CLI is an open source tool that enables you to interact with AWS services using commands in your command\-line shell\. The AWS SAM CLI requires the AWS CLI for activities such as configuring credentials\. To learn more about the AWS CLI, see [What is the AWS Command Line Interface?](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html) in the *AWS Command Line Interface User Guide*\.

To install the AWS CLI, see [ Installing or updating the latest version of the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) in the *AWS Command Line Interface User Guide*\.

## Step 5: Use the AWS CLI to configure AWS credentials<a name="prerequisites-configure-credentials"></a>

**To configure credentials with the AWS CLI**

1. Run the `aws configure` command from the command line\.

1. Configure the following\. Select each link to learn more:

   1. [ Access key ID](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-creds)

   1. [ Secret access key](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-creds)

   1. [AWS Region](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-region)

   1. [ Output format](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-format)

   The following example shows sample values\.

   ```
   $ aws configure
   AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
   AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
   Default region name [None]: us-west-2
   Default output format [None]: json
   ```

The AWS CLI stores this information in a *profile* \(a collection of settings\) named `default` in the `credentials` file\. By default, the information in this profile is used when you run an AWS CLI command that doesn't explicitly specify a profile to use\. For more information on the `credentials` file, see [ Configuration and credential file settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html) in the *AWS Command Line Interface User Guide*\.

For more information on configuring credentials, such as using an existing configuration and credentials file, see [Quick setup](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html) in the *AWS Command Line Interface User Guide*\.

## Next steps<a name="prerequisites-next-steps"></a>

You are now ready to install the AWS SAM CLI and start using AWS SAM\. To install the AWS SAM CLI, see [Installing the AWS SAM CLI](install-sam-cli.md)\.