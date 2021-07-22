# Locally testing AWS CDK applications<a name="serverless-cdk-testing"></a>


****  

|  | 
| --- |
| CDK integration with the AWS SAM CLI is currently in public preview\. During public preview, CDK integration with the AWS SAM CLI may be subject to backwards incompatible changes\. | 

You can use the AWS SAM CLI to locally test your AWS CDK applications by running the following commands from the project root directory of your AWS CDK application:
+ [sam local invoke](sam-cli-command-reference-sam-local-invoke.md)
+ [sam local start\-api](sam-cli-command-reference-sam-local-start-api.md)
+ [sam local start\-lambda](sam-cli-command-reference-sam-local-start-lambda.md)

**Note**  
The AWS SAM CLI only supports Lambda functions created with the standard Lambda construct\. For information about the standard Lambda construct, see [@aws\-cdk/aws\-lambda module](https://docs.aws.amazon.com/cdk/api/latest/docs/aws-lambda-readme.html)\.

When you run any of the sam local commands with a AWS CDK application, the AWS SAM CLI runs cdk synth on your behalf if the [cloud assembly](https://docs.aws.amazon.com/cdk/latest/guide/apps.html#apps_cloud_assembly) doesn't already exist\. The default location of the cloud assembly relative to the project root directory is `./aws-sam/build`\.

When running sam local invoke you need the function identifier that you want to invoke, and the stack name where the function is defined\.

**Usage:**

```
# Invoke the function FUNCTION_IDENTIFIER declared in the stack STACK_NAME
sam-beta-cdk local invoke [OPTIONS] [STACK_NAME/FUNCTION_IDENTIFIER]

# Start all APIs declared in the AWS CDK application
sam-beta-cdk local start-api [OPTIONS]

# Start a local endpoint that emulates AWS Lambda
sam-beta-cdk local start-lambda [OPTIONS]
```

**Options:**

For the public preview version of the AWS SAM CLI, the following options are available in addition to the options available in the production version of the `sam local` functions described in this topic\.


****  

| Option | Description | 
| --- | --- | 
| \-\-project\-type \[CFN \| CDK\] | Specifies whether this is an AWS SAM or AWS CDK application\. If this option is not specified, the AWS SAM CLI will attempt to determine which type of project it is based on the existance of template\.yaml \(AWS SAM\) or cdk\.json \(AWS CDK\) in the project root directory\. | 
| \-\-cdk\-app TEXT | Command\-line for executing your app, or a cloud assembly directory\. This option is passed directly to the \-\-app option of the cdk synth command\. For more information, see [Toolkit reference](https://docs.aws.amazon.com/cdk/latest/guide/cli.html#cli-ref) in the AWS Cloud Development Kit \(CDK\) Developer Guide\. | 
| \-\-cdk\-context | Runtime context in key\-value pairs for your AWS CDK application\. This option is passed directly to the \-\-context option of the cdk synth command\. For more information, see [Toolkit reference](https://docs.aws.amazon.com/cdk/latest/guide/cli.html#cli-ref) in the AWS Cloud Development Kit \(CDK\) Developer Guide\. | 

## Example<a name="testing-cdk-applications-examples"></a>

Consider a stack and a function that are declared with the following sample:

```
app = new HelloCdkStack(app, "HelloCdkStack",
   ...
)
class HelloCdkStack extends cdk.Stack {
  constructor(scope: cdk.Construct, id: string, props?: cdk.StackProps) {
    ...
    const fn = new lambda.Function(this, 'MyFunction', {
  		...
	});
}
```

In this example the stack name is *HelloCdkStack* and the function identifier is *MyFunction*\. The following command locally invokes the Lambda function defined in example presented above:

```
sam-beta-cdk local invoke HelloCdkStack/MyFunction
```