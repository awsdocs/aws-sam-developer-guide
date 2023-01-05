# sam metadata resource<a name="terraform-sam-metadata"></a>


|  | 
| --- |
|  Terraform support is in preview release for the AWS SAM CLI and is subject to change\. To provide feedback and submit feature requests, create a [GitHub Issue](https://github.com/aws/aws-sam-cli/issues/new?labels=area%2Fterraform)\.  | 

This page contains reference information for the sam metadata resource resource type used with Terraform projects\.
+ For an introduction to using the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) with Terraform, see [What is AWS SAM CLI support for Terraform?](what-is-terraform-support.md)\.
+ To use the AWS SAM CLI with Terraform, see [Using the AWS SAM CLI with Terraform for local debugging and testing](using-samcli-terraform.md)\.

**Topics**
+ [Arguments](#terraform-sam-metadata-arguments)
+ [Examples](#terraform-sam-metadata-examples)

## Arguments<a name="terraform-sam-metadata-arguments"></a>


****  

| Argument | Description | 
| --- | --- | 
| built\_output\_path | The path to your AWS Lambda function's built artifacts\. | 
| docker\_build\_args | Decoded string of the Docker build arguments JSON object\. This argument is optional\. | 
| docker\_context | The path to the directory containing the Docker image build context\. | 
| docker\_file |  The path to the Docker file\. This path is relative to the `docker_context` path\. This argument is optional\. Default value is `Dockerfile`\.  | 
| docker\_tag | The value of the created Docker image tag\. This value is optional\. | 
| depends\_on | The path to the building resource for your Lambda function or layer\. To learn more, see [The depends\_on argument](https://developer.hashicorp.com/terraform/language/meta-arguments/depends_on) in Terraform's documentation\. | 
| original\_source\_code |  The path to where your Lambda function is defined\. This value can be a string, array of strings, or a decoded JSON object as a string\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/terraform-sam-metadata.html)  | 
| resource\_name | The Lambda function name\. | 
| resource\_type |  The format of your Lambda function package type\. Accepted values are: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/terraform-sam-metadata.html)  | 
| source\_code\_property | The path to the Lambda resource code in the JSON object\. Define this property when original\_source\_code is a JSON object\. | 

## Examples<a name="terraform-sam-metadata-examples"></a>

### sam metadata resource referencing a Lambda function using the ZIP package type<a name="terraform-sam-metadata-examples-example1"></a>

```
# Lambda function resource
resource "aws_lambda_function" "tf_lambda_func" {
  filename = "${path.module}/python/hello-world.zip"
  handler = "index.lambda_handler"
    runtime = "python3.8"
    function_name = "function_example"
    role = aws_iam_role.iam_for_lambda.arn
    depends_on = [
      null_resource.build_lambda_function # function build logic
    ]
}

# sam metadata resource
resource "null_resource" "sam_metadata_function_example" {
  triggers = {
    resource_name = "aws_lambda_function.function_example"
    resource_type = "ZIP_LAMBDA_FUNCTION"
    original_source_code = "${path.module}/python"
    built_output_path = "${path.module}/building/function_example"
  }
  depends_on = [
    null_resource.build_lambda_function # function build logic
  ]
}
```

### sam metadata resource referencing a Lambda function using the image package type<a name="terraform-sam-metadata-examples-example2"></a>

```
resource "null_resource" "sam_metadata_function {
  triggers = {
    resource_name = "aws_lambda_function.image_function"
    resource_type = "IMAGE_LAMBDA_FUNCTION"
    docker_context = local.lambda_src_path
    docker_file = "Dockerfile"
    docker_build_args = jsonencode(var.build_args)
    docker_tag = "latest"
  }
}
```

### sam metadata resource referencing a Lambda layer<a name="terraform-sam-metadata-examples-example3"></a>

```
resource "null_resource" "sam_metadata_layer1" {
  triggers = {
    resource_name = "aws_lambda_layer_version.layer"
    resource_type = "LAMBDA_LAYER"
    original_source_code = local.layer_src
    built_output_path = "${path.module}/${layer_build_path}"
  }
  depends_on = [null_resource.layer_build]
}
```