# Packaging AWS CDK applications<a name="serverless-cdk-packaging"></a>


****  

|  | 
| --- |
| CDK integration with the AWS SAM CLI is currently in public preview\. During public preview, CDK integration with the AWS SAM CLI may be subject to backwards incompatible changes\. | 

The AWS SAM CLI provides support for packaging AWS CDK applications by detecting that the following command is run from the project root directory of your AWS CDK application:
+ [sam package](sam-cli-command-reference-sam-package.md)

When you run the sam package command with a AWS CDK application, AWS SAM runs cdk synth on your behalf if the [cloud assembly](https://docs.aws.amazon.com/cdk/latest/guide/apps.html#apps_cloud_assembly) doesn't already exist\. The default location of the cloud assembly relative to the project root directory is `./aws-sam/build`\.

The following options are available with this command for packaging AWS CDK applications:

**Options:**

For the public preview version of the AWS SAM CLI, the following options are available in addition to the options available in the production version of the sam package command\.


****  

| Option | Description | 
| --- | --- | 
| \-\-project\-type \[CFN \| CDK\] | Specifies whether this is an AWS SAM or AWS CDK application\. If this option is not specified, the AWS SAM CLI will attempt to determine which type of project it is based on the existance of template\.yaml \(AWS SAM\) or cdk\.json \(AWS CDK\) in the project root directory\. | 
| \-\-cdk\-app TEXT | Command\-line for executing your app, or a cloud assembly directory\. This option is passed directly to the \-\-app option of the cdk synth command\. For more information, see [Toolkit reference](https://docs.aws.amazon.com/cdk/latest/guide/cli.html#cli-ref) in the AWS Cloud Development Kit \(CDK\) Developer Guide\. | 
| \-\-cdk\-context | Runtime context in key\-value pairs for your AWS CDK application\. This option is passed directly to the \-\-context option of the cdk synth command\. For more information, see [Toolkit reference](https://docs.aws.amazon.com/cdk/latest/guide/cli.html#cli-ref) in the AWS Cloud Development Kit \(CDK\) Developer Guide\. | 

## Examples<a name="deploying-cdk-applications-examples"></a>

Running the following command from the AWS CDK project root directory will package the application\.

```
sam-beta-cdk package
```