# Using sam local invoke<a name="using-sam-cli-local-invoke"></a>

Use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam local invoke` subcommand to initiate a one\-time invocation of an AWS Lambda function locally\.
+ For an introduction to the AWS SAM CLI, see [What is the AWS SAM CLI?](what-is-sam.md#what-is-sam-cli)\.
+ For a list of `sam local invoke` command options, see [sam local invoke](sam-cli-command-reference-sam-local-invoke.md)\.
+ For an example of using `sam local invoke` during a typical development workflow, see [Step 6: \(Optional\) Test your application locally](serverless-getting-started-hello-world.md#serverless-getting-started-hello-world-test)\.

## Prerequisites<a name="using-sam-cli-local-invoke-prerequisites"></a>

To use `sam local invoke`, install the AWS SAM CLI by completing the following:
+ [AWS SAM prerequisites](prerequisites.md)\.
+ [Installing the AWS SAM CLI](install-sam-cli.md)\.

Before using `sam local invoke`, we recommend a basic understanding of the following:
+ [Configuring the AWS SAM CLI](using-sam-cli-configure.md)\.
+ [Using sam init](using-sam-cli-init.md)\.
+ [Using sam build](using-sam-cli-build.md)\.
+ [Using sam deploy](using-sam-cli-deploy.md)\.

## Invoke a Lambda function locally<a name="using-sam-cli-local-invoke-use"></a>

When you run `sam local invoke`, the AWS SAM CLI assumes that your current working directory is your project’s root directory\. The AWS SAM CLI will first look for a `template.[yaml|yml]` file within a `.aws-sam` subfolder\. If not found, the AWS SAM CLI will look for a `template.[yaml|yml]` file within your current working directory\.

**To invoke a Lambda function locally**

1. From the root directory of your project, run the following:

   ```
   $ sam local invoke <options>
   ```

1. If your application contains more than one function, provide the function’s logical ID\. The following is an example:

   ```
   $ sam local invoke HelloWorldFunction
   ```

1. The AWS SAM CLI builds your function in a local container using Docker\. It then invokes your function and outputs your function’s response\.

   The following is an example:

   ```
   $ sam local invoke
   Invoking app.lambda_handler (python3.9)
   Local image is out of date and will be updated to the latest runtime. To skip this, pass in the parameter --skip-pull-image
   Building image....................................................................................................................
   Using local image: public.ecr.aws/lambda/python:3.9-rapid-x86_64.
   
   Mounting /Users/.../sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated, inside runtime container
   START RequestId: 64bf7e54-5509-4762-a97c-3d740498d3df Version: $LATEST
   END RequestId: 64bf7e54-5509-4762-a97c-3d740498d3df
   REPORT RequestId: 64bf7e54-5509-4762-a97c-3d740498d3df  Init Duration: 1.09 ms  Duration: 608.42 ms       Billed Duration: 609 ms Memory Size: 128 MB     Max Memory Used: 128 MB
   {"statusCode": 200, "body": "{\"message\": \"hello world\"}"}%
   ```

### Managing logs<a name="using-sam-cli-local-invoke-logs"></a>

When using `sam local invoke`, the Lambda function runtime output \(for example, logs\) is output to `stderr`, and the Lambda function result is output to `stdout`\.

The following is an example of a basic Lambda function:

```
def handler(event, context):
    print("some log") # this goes to stderr
    return "hello world" # this goes to stdout
```

You can save these standard outputs\. The following is an example:

```
$ sam local invoke 1> stdout.log
...

$ cat stdout.log
"hello world"

$ sam local invoke 2> stderr.log
...

$ cat stderr.log
Invoking app.lambda_handler (python3.9)
Local image is up-to-date
Using local image: public.ecr.aws/lambda/python:3.9-rapid-x86_64.
Mounting /Users/.../sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated, inside runtime container
START RequestId: 0b46e646-3bdf-4b58-8beb-242d00912c46 Version: $LATEST
some log
END RequestId: 0b46e646-3bdf-4b58-8beb-242d00912c46
REPORT RequestId: 0b46e646-3bdf-4b58-8beb-242d00912c46  Init Duration: 0.91 ms  Duration: 589.19 ms Billed Duration: 590 ms Memory Size: 128 MB Max Memory Used: 128 MB
```

You can use these standard outputs to further automate your local development processes\.

## Options<a name="using-sam-cli-local-invoke-options"></a>

### Pass custom events to invoke the Lambda function<a name="using-sam-cli-local-invoke-options-events"></a>

To pass an event to the Lambda function, use the `--event` option\. The following is an example:

```
$ sam local invoke --event events/s3.json S3JsonLoggerFunction
```

You can create events with the `sam local generate-event` subcommand\. To learn more, see [Using sam local generate\-event](using-sam-cli-local-generate-event.md)\.

### Pass environment variables when invoking your Lambda function<a name="using-sam-cli-local-invoke-options-env"></a>

If your Lambda function uses environment variables, you can pass them during local testing with the `--env-vars` option\. This is a great way to test a Lambda function locally with services in your application that are already deployed the cloud\. The following is an example:

```
$ sam local invoke --env-vars locals.json
```

### Specify a template or function<a name="using-sam-cli-local-invoke-options-specify"></a>

To specify a template for the AWS SAM CLI to reference, use the `--template` option\. The AWS SAM CLI will load just that AWS SAM template and the resources it points to\.

To invoke a function of a nested application or stack, provide the application or stack logical ID along with the function logical ID\. The following is an example:

```
$ sam local invoke StackLogicalId/FunctionLogicalId
```

### Test a Lambda function from your Terraform project<a name="using-sam-cli-local-invoke-options-terraform"></a>

Use the `--hook-name` option to locally test Lambda functions from your Terraform projects\. To learn more, see [Using the AWS SAM CLI with Terraform for local debugging and testing](using-samcli-terraform.md)\.

The following is an example:

```
$ sam local invoke --hook-name terraform --beta-features
```

## Best practices<a name="using-sam-cli-local-invoke-best"></a>

If your application has a `.aws-sam` directory from running `sam build`, be sure to run `sam build` every time you update your function code\. Then, run `sam local invoke` to locally test your updated function code\.

Local testing is a great solution for quick development and testing before deploying to the cloud\. However, local testing doesn’t validate everything, such as permissions between your resources in the cloud\. As much as possible, test your applications in the cloud\. We recommend [using `sam sync`](using-sam-cli-sync.md) to speed up your cloud testing workflows\.

## Examples<a name="using-sam-cli-local-invoke-examples"></a>

### Generate an Amazon API Gateway sample event and use it to invoke a Lambda function locally<a name="using-sam-cli-local-invoke-examples-api"></a>

First, we generate an API Gateway HTTP API event payload and save it to our `events` folder\.

```
$ sam local generate-event apigateway http-api-proxy > events/apigateway_event.json
```

Next, we modify our Lambda function to return a parameter value from the event\.

```
def lambda_handler(event, context):
    print("HelloWorldFunction invoked")
    return {
        "statusCode": 200,
        "body": json.dumps({
            "message": event['queryStringParameters']['parameter2'],
        }),
    }
```

Next, we locally invoke our Lambda function and provide our custom event\.

```
$ sam local invoke --event events/apigateway_event.json

Invoking app.lambda_handler (python3.9)
Local image is up-to-date
Using local image: public.ecr.aws/lambda/python:3.9-rapid-x86_64.

Mounting /Users/...sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated, inside runtime container
START RequestId: 59535d0d-3d9e-493d-8c98-6264e8e961b8 Version: $LATEST
some log
END RequestId: 59535d0d-3d9e-493d-8c98-6264e8e961b8
REPORT RequestId: 59535d0d-3d9e-493d-8c98-6264e8e961b8  Init Duration: 1.63 ms  Duration: 564.07 ms       Billed Duration: 565 ms Memory Size: 128 MB     Max Memory Used: 128 MB
{"statusCode": 200, "body": "{\"message\": \"value\"}"}%
```

### Pass environment variables when invoking a Lambda function locally<a name="using-sam-cli-local-invoke-examples-env"></a>

This application has a Lambda function that uses an environment variable for an Amazon DynamoDB table name\. The following is an example of the function defined in the AWS SAM template:

```
AWSTemplateFormatVersion: 2010-09-09
Transform: AWS::Serverless-2016-10-31
...
Resources:
  getAllItemsFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: src/get-all-items.getAllItemsHandler
      Description: get all items
      Policies:
        - DynamoDBReadPolicy:
            TableName: !Ref SampleTable
      Environment:
        Variables:
          SAMPLE_TABLE: !Ref SampleTable
...
```

We want to locally test our Lambda function while having it interact with our DynamoDB table in the cloud\. To do this, we create our environment variables file and save it in our project's root directory as `locals.json`\. The value provided here for `SAMPLE_TABLE` references our DynamoDB table in the cloud\.

```
{
    "getAllItemsFunction": {
        "SAMPLE_TABLE": "dev-demo-SampleTable-1U991234LD5UM98"
    }
}
```

Next, we run `sam local invoke` and pass in our environment variables with the `--env-vars` option\.

```
$ sam local invoke getAllItemsFunction --env-vars locals.json

Mounting /Users/...sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated, inside runtime container
START RequestId: 59535d0d-3d9e-493d-8c98-6264e8e961b8 Version: $LATEST
some log
END RequestId: 59535d0d-3d9e-493d-8c98-6264e8e961b8
REPORT RequestId: 59535d0d-3d9e-493d-8c98-6264e8e961b8  Init Duration: 1.63 ms  Duration: 564.07 ms       Billed Duration: 565 ms Memory Size: 128 MB     Max Memory Used: 128 MB
{"statusCode":200,"body":"{}"}
```

## Learn more<a name="using-sam-cli-local-invoke-learn"></a>

For a list of all `sam local invoke` options, see [sam local invoke](sam-cli-command-reference-sam-local-invoke.md)\.

For a demo of using `sam local`, see [AWS SAM for local development\. Testing AWS Cloud resources from local development environments](https://www.youtube.com/watch?v=NzPqMrdgD1s&list=PLJo-rJlep0ED198FJnTzhIB5Aut_1vDAd&index=24) in the *Serverless Land Sessions with SAM series on YouTube*\.