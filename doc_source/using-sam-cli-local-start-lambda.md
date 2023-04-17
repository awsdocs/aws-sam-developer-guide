# Using sam local start\-lambda<a name="using-sam-cli-local-start-lambda"></a>

Use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam local start-lambda` subcommand to invoke your AWS Lambda function through the AWS Command Line Interface \(AWS CLI\) or SDKs\. This command starts a local endpoint that emulates AWS Lambda\.
+ For an introduction to the AWS SAM CLI, see [What is the AWS SAM CLI?](what-is-sam.md#what-is-sam-cli)\.
+ For a list of `sam local start-lambda` command options, see [sam local start\-lambda](sam-cli-command-reference-sam-local-start-lambda.md)\.

## Prerequisites<a name="using-sam-cli-local-start-api-prerequisites"></a>

To use `sam local start-lambda`, install the AWS SAM CLI by completing the following:
+ [AWS SAM prerequisites](prerequisites.md)\.
+ [Installing the AWS SAM CLI](install-sam-cli.md)\.

Before using `sam local start-lambda`, we recommend a basic understanding of the following:
+ [Configuring the AWS SAM CLI](using-sam-cli-configure.md)\.
+ [Using sam init](using-sam-cli-init.md)\.
+ [Using sam build](using-sam-cli-build.md)\.
+ [Using sam deploy](using-sam-cli-deploy.md)\.

## Using sam local start\-lambda<a name="using-sam-cli-local-start-lambda-use"></a>

When you run `sam local start-lambda`, the AWS SAM CLI assumes that your current working directory is your project’s root directory\. The AWS SAM CLI will first look for a `template.[yaml|yml]` file within a `.aws-sam` subfolder\. If not found, the AWS SAM CLI will look for a `template.[yaml|yml]` file within your current working directory\.

**To use sam local start\-lambda**

1. From the root directory of your project, run the following:

   ```
   $ sam local start-lambda <options>
   ```

1. The AWS SAM CLI builds your Lambda functions in a local Docker container\. It then outputs the local address to your HTTP server endpoint\. The following is an example:

   ```
   $ sam local start-lambda
   Initializing the lambda functions containers.
   Local image is up-to-date
   Using local image: public.ecr.aws/lambda/python:3.9-rapid-x86_64.
   
   Mounting /Users/.../sam-app/hello_world as /var/task:ro,delegated, inside runtime container
   Containers Initialization is done.
   Starting the Local Lambda Service. You can now invoke your Lambda Functions defined in your template through the endpoint.
   2023-04-13 07:25:43 WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
    * Running on http://127.0.0.1:3001
   2023-04-13 07:25:43 Press CTRL+C to quit
   ```

1. Use the AWS CLI or SDKs to invoke your Lambda function locally\.

   The following is an example using the AWS CLI:

   ```
   $ aws lambda invoke --function-name "HelloWorldFunction" --endpoint-url "http://127.0.0.1:3001" --no-verify-ssl out.txt
       
   StatusCode: 200
   (END)
   ```

   The following is an example using the AWS SDK for Python:

   ```
   import boto3
   from botocore.config import Config
   from botocore import UNSIGNED
   
   lambda_client = boto3.client('lambda',
                                endpoint_url="http://127.0.0.1:3001",
                                use_ssl=False,
                                verify=False,
                                config=Config(signature_version=UNSIGNED,
                                              read_timeout=1,
                                              retries={'max_attempts': 0}
                                              )
                               )
   lambda_client.invoke(FunctionName="HelloWorldFunction")
   ```

## Options<a name="using-sam-cli-local-start-lambda-options"></a>

### Specify a template<a name="using-sam-cli-local-start-lambda-options-template"></a>

To specify a template for the AWS SAM CLI to reference, use the `--template` option\. The AWS SAM CLI will load just that AWS SAM template and the resources it points to\. The following is an example:

```
$ sam local start-lambda --template myTemplate.yaml
```

## Best practices<a name="using-sam-cli-local-start-lambda-best"></a>

If your application has a `.aws-sam` directory from running `sam build`, be sure to run `sam build` every time you update your function code\. Then, run `sam local start-lambda` to locally test your updated function code\.

Local testing is a great solution for quick development and testing before deploying to the cloud\. However, local testing doesn’t validate everything, such as permissions between your resources in the cloud\. As much as possible, test your applications in the cloud\. We recommend [using `sam sync`](using-sam-cli-sync.md) to speed up your cloud testing workflows\.

## Learn more<a name="using-sam-cli-local-start-lambda-learn"></a>

For a list of all `sam local start-lambda` options, see [sam local start\-lambda](sam-cli-command-reference-sam-local-start-lambda.md)\.