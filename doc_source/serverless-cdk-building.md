# Building AWS CDK applications<a name="serverless-cdk-building"></a>


****  

|  | 
| --- |
| CDK integration with the AWS SAM CLI is currently in public preview\. During public preview, CDK integration with the AWS SAM CLI may be subject to backwards incompatible changes\. | 

The AWS SAM CLI provides support for building Lambda functions and layers defined in your AWS CDK application by detecting that the following command is run in the AWS CDK application directory:
+ [sam build](sam-cli-command-reference-sam-build.md)

When you run the `sam build` command with a AWS CDK application, AWS SAM runs `cdk synth` on your behalf to produce the [cloud assembly](https://docs.aws.amazon.com/cdk/latest/guide/apps.html#apps_cloud_assembly) that will be needed for subsequent steps in your development workflow\. The default location of the cloud assembly relative to the project root directory is `./aws-sam/build`\.

**Options:**

For the public preview version of the AWS SAM CLI, the following options are available in addition to the options available in the production version of the `sam build` function\.


****  

| Option | Description | 
| --- | --- | 
| \-\-project\-type \[CFN \| CDK\] | Specifies whether this is an AWS SAM or AWS CDK application\. If this option is not specified, the AWS SAM CLI will attempt to determine which type of project it is based on the existance of template\.yaml \(AWS SAM\) or cdk\.json \(AWS CDK\) in the project root directory\. | 
| \-\-cdk\-app | Command\-line for executing your app, or a cloud assembly directory\. This option is passed directly to the \-\-app option of the cdk synth command\. For more information, see [Toolkit reference](https://docs.aws.amazon.com/cdk/latest/guide/cli.html#cli-ref) in the AWS Cloud Development Kit \(AWS CDK\) Developer Guide\. | 
| \-\-cdk\-context | Runtime context in key\-value pairs for your AWS CDK application\. This option is passed directly to the \-\-context option of the cdk synth command\. For more information, see [Toolkit reference](https://docs.aws.amazon.com/cdk/latest/guide/cli.html#cli-ref) in the AWS Cloud Development Kit \(AWS CDK\) Developer Guide\. | 

## Example<a name="building-cdk-applications-examples"></a>

Running the following command from the AWS CDK project root directory will build the application and place the cloud assembly in default location of `./aws-sam/build`\. 

```
sam-beta-cdk build
```