# Getting started with Terraform support for AWS SAM CLI<a name="gs-terraform-support"></a>


|  | 
| --- |
|  Terraform support is in preview release for the AWS SAM CLI and is subject to change\. To provide feedback and submit feature requests, create a [GitHub Issue](https://github.com/aws/aws-sam-cli/issues/new?labels=area%2Fterraform)\.  | 

The AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) supports local debugging and testing of AWS Lambda functions and layers within your Terraform projects\.

**Topics**
+ [AWS SAM CLI Terraform prerequisites](#gs-terraform-support-prerequisites)

## AWS SAM CLI Terraform prerequisites<a name="gs-terraform-support-prerequisites"></a>

Complete all prerequisites to begin using the AWS SAM CLI with your Terraform projects\.

1. 

**Install Python 3\.6 or newer**

   Python 3\.6 or newer is required for use with the AWS SAM CLI\. For installation instructions, see [Downloading Python](https://wiki.python.org/moin/BeginnersGuide/Download) in Python's *Beginners Guide*\.

   Verify that Python 3\.6 or newer is added to your machine path by running:

   ```
   python --version
   ```

   The output should display a version of Python that is 3\.6 or newer\.

1. 

**Install or upgrade the AWS SAM CLI**

   To check if you have the AWS SAM CLI installed, run the following:

   ```
   sam --version
   ```

   If the AWS SAM CLI is already installed, the output will display a version\. To upgrade to the newest version, see [Upgrading the AWS SAM CLI](manage-sam-cli-versions.md#manage-sam-cli-versions-upgrade)\.

   For instructions on installing the AWS SAM CLI along with all of its prerequisites, see [Installing the AWS SAM CLI](install-sam-cli.md)\.

1. 

**Install Terraform**

   To check if you have Terraform installed, run the following:

   ```
   terraform -version
   ```

   To install Terraform, see [Install Terraform](https://developer.hashicorp.com/terraform/downloads) in Terraform's *Developer Documentation*\.

1. 

**Install Docker for local testing**

   The AWS SAM CLI requires Docker for local testing\. To install Docker, see [Installing Docker to use with the AWS SAM CLI](install-docker.md)\.

1. 

**Install the make tool \(Windows only\)**

   `Make` is a package manager and installer for Windows\. To install using [Chocolatey](https://chocolatey.org/), see [Using Chocolatey](https://www.technewstoday.com/install-and-use-make-in-windows/#using-chocolatey) in *How to Install and Use "Make" in Windows*\.

### Next steps<a name="gs-terraform-support-next"></a>

You're now ready to begin using the AWS SAM CLI with your Terraform projects\. To learn more, see:
+ [Better together: AWS SAM CLI and HashiCorp Terraform](http://aws.amazon.com/blogs/compute/better-together-aws-sam-cli-and-hashicorp-terraform/) – Tutorial on using the AWS SAM CLI with Terraform\.
+ [Using the AWS SAM CLI with Terraform for local debugging and testing](using-samcli-terraform.md) – Documentation on using the AWS SAM CLI with Terraform\.