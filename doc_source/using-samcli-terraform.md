# Using the AWS SAM CLI with Terraform for local debugging and testing<a name="using-samcli-terraform"></a>


|  | 
| --- |
|  Terraform support is in preview release for the AWS SAM CLI and is subject to change\. To provide feedback and submit feature requests, create a [GitHub Issue](https://github.com/aws/aws-sam-cli/issues/new?labels=area%2Fterraform)\.  | 

The AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) supports local debugging and testing of your AWS Lambda functions and layers\. For an introduction to this feature, see [What is AWS SAM CLI support for Terraform?](what-is-terraform-support.md)

**Topics**
+ [Local debugging and testing overview](#using-samcli-terraform-overview)
+ [sam metadata resource](#using-samcli-terraform-metadata)
+ [Defining the sam metadata resource](#using-samcli-terraform-metadata-define)
+ [Using the AWS SAM CLI with Terraform](#using-samcli-terraform-instructions)
+ [Building your Terraform project with sam build](#using-samcli-terraform-build)
+ [Local testing with sam local invoke](#using-samcli-terraform-local-invoke)
+ [Local testing with sam local start\-lambda](#using-samcli-terraform-local-start-lambda)
+ [Unsupported Terraform features](#using-samcli-terraform-unsupported)

## Local debugging and testing overview<a name="using-samcli-terraform-overview"></a>

The general process to prepare your Terraform project for local debugging and testing consists of:

1. Determine if you need to define a sam metadata resource, depending on your Terraform project structure\.

1. Determine if you need to run sam build, depending on your Terraform project structure\.

1. Use supported AWS SAM CLI commands to locally debug and test your Lambda functions\.

As you locally debug and test, use terraform plan and terraform apply to prepare and deploy your changes\.

## sam metadata resource<a name="using-samcli-terraform-metadata"></a>

The sam metadata resource is a `null_resource` Terraform resource type that is optional based on your Terraform project structure\. To learn more about this resource type, see [null\_resource](https://registry.terraform.io/providers/hashicorp/null/latest/docs/resources/resource) in Terraform's documentation\.

The sam metadata resource provides the AWS SAM CLI with the information it needs to locate Lambda functions and layers, along with their source code, build dependencies, and build logic from within your Terraform project\. If you build your Lambda resource artifacts outside of your Terraform project and pass these artifact paths into your Terraform project, the sam metadata resource is not required\.

Alternatively, if you use Terraform variables to define your Lambda artifacts, you don't need to define a sam metadata resource\. The AWS SAM CLI will utilize those Terraform variables\. For more information on Terraform variables, see [https://developer.hashicorp.com/terraform/cli/config/environment-variables#tf_var_name](https://developer.hashicorp.com/terraform/cli/config/environment-variables#tf_var_name) in Terraform's *Developer Documentation*

Otherwise, if you build your Lambda functions and layers from within your Terraform project, the sam metadata resource is required for each function and layer\.

## Defining the sam metadata resource<a name="using-samcli-terraform-metadata-define"></a>

Use the following guidelines when defining your sam metadata resource:
+ Name your sam metadata resource starting with `sam_metadata_` for the AWS SAM CLI to identify it as a sam metadata resource\.
+ Define your properties within the `triggers` block\.
+ Define your Lambda function or layer build logic with the `depends_on` argument\.

Here is a basic sam metadata resource template structure:

```
resource "null_resource" "sam_metadata_..." {
  triggers = {
    resource_name = resource_name
    resource_type = resource_type
    original_source_code = original_source_code
    built_output_path = built_output_path
  }
  depends_on = [
    null_resource.build_lambda_function # ref to your build logic
  ]
}
```

The details of your sam metadata resource will vary based on the Lambda resource type \(function or layer\), and the packaging type \(ZIP or image\)\. For more information on defining this resource, along with examples, see [sam metadata resource](terraform-sam-metadata.md)\.

## Using the AWS SAM CLI with Terraform<a name="using-samcli-terraform-instructions"></a>

The main properties you need to define when using supported AWS SAM CLI commands are:
+ `--hook-name`
+ `--beta-features`

These properties can be defined from the command line when running AWS SAM CLI commands, or in your `samconfig.toml` file\. Add the following to define these properties in your `samconfig.toml` file:

```
version = 0.1
[default]
[default.build.parameters]
hook_name = "terraform"
beta_features = true
```

Optionally, configure these properties when using the AWS SAM CLI with supported commands\. See the following examples for defining these properties from your command line:

```
# Using sam build with Terraform
sam build --hook-name terraform --beta-features

# Using sam local invoke with Terraform
sam local invoke --hook-name terraform --beta-features

# Using sam local start-lambda with Terraform
sam local start-lambda --hook-name terraform --beta-features
```

If you do not allow beta features, the AWS SAM CLI will prompt you to opt in when you define the `--hook-name` option:

```
Supporting Terraform applications is a beta feature.
Please confirm if you would like to proceed using AWS SAM CLI with terraform application.
You can also enable this beta feature with 'sam local invoke --beta-features'. [y/N]: y

Experimental features are enabled for this session.
Visit the docs page to learn more about the AWS Beta terms https://aws.amazon.com/service-terms/.
```

## Building your Terraform project with sam build<a name="using-samcli-terraform-build"></a>

Running sam build to initialize your Terraform project for local debugging and testing is only required if you define a sam metadata resource\. Otherwise, running sam build is not required\.

To build wth sam build, run the following from your Terraform project root directory:

```
sam build --hook-name terraform --beta-features lambda-resource-id
```

Optionally, you can provide the `id` of the Lambda function or layer to be built\. Accepted ids are the Lambda function name or the full Terraform resource address, such as `aws_lambda_function.list_books` or `module.list_book_function.aws_lambda_function.this[0]`\.

**Note**  
When running sam build, your sam metadata resource `depends_on` argument must refer to your Lambda resource build logic\.

For more information on sam build, see [sam build](sam-cli-command-reference-sam-build.md)\.

## Local testing with sam local invoke<a name="using-samcli-terraform-local-invoke"></a>

**Note**  
To use the AWS SAM CLI to test locally, you must have Docker intalled and configured\. For instructions, see [Installing Docker to use with the AWS SAM CLI](install-docker.md)\.

The following is an example of testing your Lambda function locally by passing in an event:

```
sam local invoke --hook-name terraform --beta-features hello_world_function -e events/event.json -
```

For more information on sam local invoke, see [sam local invoke](sam-cli-command-reference-sam-local-invoke.md)\.

## Local testing with sam local start\-lambda<a name="using-samcli-terraform-local-start-lambda"></a>

The following is an example of testing your Lambda function locally with the AWS CLI:

```
# Start Lambda
sam local start-lambda --hook-name terraform --beta-features hello_world_function 

# Test locally
aws lambda invoke --function-name hello_world_function --endpoint-url http://127.0.0.1:3001/ response.json --cli-binary-format raw-in-base64-out --payload file://events/event.json
```

For more information on sam local start\-lambda, see [sam local start\-lambda](sam-cli-command-reference-sam-local-start-lambda.md)\.

## Unsupported Terraform features<a name="using-samcli-terraform-unsupported"></a>

The following Terraform features are not supported at this time:
+ Lambda functions linked to multiple layers\.
+ Terraform local values\.