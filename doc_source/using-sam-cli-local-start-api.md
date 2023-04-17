# Using sam local start\-api<a name="using-sam-cli-local-start-api"></a>

Use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam local start-api` subcommand to run your AWS Lambda functions locally and test through a local HTTP server host\. This type of test is helpful for Lambda functions that are invoked by an Amazon API Gateway endpoint\.
+ For an introduction to the AWS SAM CLI, see [What is the AWS SAM CLI?](what-is-sam.md#what-is-sam-cli)\.
+ For a list of `sam local start-api` command options, see [sam local start\-api](sam-cli-command-reference-sam-local-start-api.md)\.
+ For an example of using `sam local start-api` during a typical development workflow, see [Step 6: \(Optional\) Test your application locally](serverless-getting-started-hello-world.md#serverless-getting-started-hello-world-test)\.

## Prerequisites<a name="using-sam-cli-local-start-api-prerequisites"></a>

To use `sam local start-api`, install the AWS SAM CLI by completing the following:
+ [AWS SAM prerequisites](prerequisites.md)\.
+ [Installing the AWS SAM CLI](install-sam-cli.md)\.

Before using `sam local start-api`, we recommend a basic understanding of the following:
+ [Configuring the AWS SAM CLI](using-sam-cli-configure.md)\.
+ [Using sam init](using-sam-cli-init.md)\.
+ [Using sam build](using-sam-cli-build.md)\.
+ [Using sam deploy](using-sam-cli-deploy.md)\.

## Using sam local start\-api<a name="using-sam-cli-local-start-api-use"></a>

When you run `sam local start-api`, the AWS SAM CLI assumes that your current working directory is your project’s root directory\. The AWS SAM CLI will first look for a `template.[yaml|yml]` file within a `.aws-sam` subfolder\. If not found, the AWS SAM CLI will look for a `template.[yaml|yml]` file within your current working directory\.

**To start a local HTTP server**

1. From the root directory of your project, run the following:

   ```
   $ sam local start-api <options>
   ```

1. The AWS SAM CLI builds your Lambda functions in a local Docker container\. It then outputs the local address of your HTTP server endpoint\. The following is an example:

   ```
   $ sam local start-api
   
   Initializing the lambda functions containers.
   Local image is up-to-date
   Using local image: public.ecr.aws/lambda/python:3.9-rapid-x86_64.
   
   Mounting /Users/.../sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated, inside runtime container
   Containers Initialization is done.
   Mounting HelloWorldFunction at http://127.0.0.1:3000/hello [GET]
   You can now browse to the above endpoints to invoke your functions. You do not need to restart/reload SAM CLI while working on your functions, changes will be reflected instantly/automatically. If you used sam build before running local commands, you will need to re-run sam build for the changes to be picked up. You only need to restart SAM CLI if you update your AWS SAM template
   2023-04-12 14:41:05 WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
    * Running on http://127.0.0.1:3000
   ```

1. You can invoke your Lambda function through the browser or command prompt\. The following is an example:

   ```
   sam-app$ curl http://127.0.0.1:3000/hello
   {"message": "Hello world!"}%
   ```

1. When you make changes to your Lambda function code, consider the following to refresh your local HTTP server:
   + If your application doesn’t have a `.aws-sam` directory and your function uses an interpreted language, the AWS SAM CLI will automatically update your function by creating a new container and hosting it\.
   + If your application does have a `.aws-sam` directory, you need to run `sam build` to update your function\. Then run `sam local start-api` again to host the function\.
   + If your function uses a compiled language or if your project requires complex packaging support, run your own build solution to update your function\. Then run `sam local start-api` again to host the function\.

### Lambda functions that use Lambda authorizers<a name="using-sam-cli-local-start-api-authorizers"></a>

**Note**  
This feature is new in AWS SAM CLI version 1\.80\.0\. To upgrade, see [Upgrading the AWS SAM CLI](manage-sam-cli-versions.md#manage-sam-cli-versions-upgrade)\.

For Lambda functions that use Lambda authorizers, the AWS SAM CLI will automatically invoke your Lambda authorizer before invoking your Lambda function endpoint\.

The following is an example of starting a local HTTP server for a function that uses a Lambda authorizer:

```
$ sam local start-api
2023-04-17 15:02:13 Attaching import module proxy for analyzing dynamic imports

AWS SAM CLI does not guarantee 100% fidelity between authorizers locally
and authorizers deployed on AWS. Any application critical behavior should
be validated thoroughly before deploying to production.

Testing application behaviour against authorizers deployed on AWS can be done using the sam sync command.

Mounting HelloWorldFunction at http://127.0.0.1:3000/authorized-request [GET]
You can now browse to the above endpoints to invoke your functions. You do not need to restart/reload SAM CLI while working on your functions, changes will be reflected instantly/automatically. If you used sam build before running local commands, you will need to re-run sam build for the changes to be picked up. You only need to restart SAM CLI if you update your AWS SAM template
2023-04-17 15:02:13 WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on http://127.0.0.1:3000
2023-04-17 15:02:13 Press CTRL+C to quit
```

When you invoke your Lambda function endpoint through the local HTTP server, the AWS SAM CLI first invokes your Lambda authorizer\. If authorization is successful, the AWS SAM CLI will invoke your Lambda function endpoint\. The following is an example:

```
$ curl http://127.0.0.1:3000/authorized-request --header "header:my_token"
{"message": "from authorizer"}%

Invoking app.authorizer_handler (python3.8)
Local image is up-to-date
Using local image: public.ecr.aws/lambda/python:3.8-rapid-x86_64.

Mounting /Users/.../sam-app/... as /var/task:ro,delegated, inside runtime container
START RequestId: 38d3b472-a2c8-4ea6-9a77-9b386989bef0 Version: $LATEST
END RequestId: 38d3b472-a2c8-4ea6-9a77-9b386989bef0
REPORT RequestId: 38d3b472-a2c8-4ea6-9a77-9b386989bef0    Init Duration: 1.08 ms    Duration: 628.26 msBilled Duration: 629 ms    Memory Size: 128 MB    Max Memory Used: 128 MB
Invoking app.request_handler (python3.8)
Using local image: public.ecr.aws/lambda/python:3.8-rapid-x86_64.

Mounting /Users/.../sam-app/... as /var/task:ro,delegated, inside runtime container
START RequestId: fdc12255-79a3-4365-97e9-9459d06446ff Version: $LATEST
END RequestId: fdc12255-79a3-4365-97e9-9459d06446ff
REPORT RequestId: fdc12255-79a3-4365-97e9-9459d06446ff    Init Duration: 0.95 ms    Duration: 659.13 msBilled Duration: 660 ms    Memory Size: 128 MB    Max Memory Used: 128 MB
No Content-Type given. Defaulting to 'application/json'.
2023-04-17 15:03:03 127.0.0.1 - - [17/Apr/2023 15:03:03] "GET /authorized-request HTTP/1.1" 200 -
```

## Options<a name="using-sam-cli-local-start-api-options"></a>

### Continuously reuse containers to speed up local function invokes<a name="using-sam-cli-local-start-api-options-warm"></a>

By default, the AWS SAM CLI creates a new container each time your function is invoked through the local HTTP server\. Use the `--warm-containers` option to automatically reuse your container for function invokes\. This speeds up the time it takes for the AWS SAM CLI to prepare your Lambda function for local invocation\. You can customize this option further by providing the `eager` or `lazy` argument\.
+ `eager` – Containers for all functions are loaded at startup and persist between invocations\.
+ `lazy` – Containers are only loaded when each function is first invoked\. They then persist for additional invocations\.

The following is an example:

```
$ sam local start-api --warm-containers eager
```

When using `--warm-containers` and modifying your Lambda function code:
+ If your application has a `.aws-sam` directory, run `sam build` to update your function code in your application’s build artifacts\.
+ When a code change is detected, the AWS SAM CLI automatically shuts down the Lambda function container\.
+ When you invoke the function again, the AWS SAM CLI automatically creates a new container\.

### Specify a container image to use for your Lambda functions<a name="using-sam-cli-local-start-api-options-specify"></a>

By default, the AWS SAM CLI uses Lambda base images from Amazon Elastic Container Registry \(Amazon ECR\) to invoke your functions locally\. Use the `--invoke-image` option to reference a custom container image\. The following is an example:

```
$ sam local start-api --invoke-image public.ecr.aws/sam/emu-python3.8
```

You can specify the function to use with the custom container image\. The following is an example:

```
$ sam local start-api --invoke-image Function1=amazon/aws/sam-cli-emulation-image-python3.8
```

### Specify a template to locally test<a name="using-sam-cli-local-start-api-options-template"></a>

To specify a template for the AWS SAM CLI to reference, use the `--template` option\. The AWS SAM CLI will load just that AWS SAM template and the resources it points to\. The following is an example:

```
$ sam local start-api --template myTemplate.yaml
```

### Specify the host development environment of your Lambda function<a name="using-sam-cli-local-start-api-options-dev"></a>

By default, the `sam local start-api` subcommand creates an HTTP server using `localhost` with IP address `127.0.0.1`\. You can customize these values if your local development environment is isolated from your local machine\.

Use the `--container-host` option to specify a host\. The following is an example:

```
$ sam local start-api --container-host host.docker.internal
```

Use the `--container-host-interface` option to specify the IP address of the host network that container ports should bind to\. The following is an example:

```
$ sam local start-api --container-host-interface 0.0.0.0
```

## Best practices<a name="using-sam-cli-local-start-api-best"></a>

If your application has a `.aws-sam` directory from running `sam build`, be sure to run `sam build` every time you update your function code\. Then, run `sam local start-api` to locally test your updated function code\.

Local testing is a great solution for quick development and testing before deploying to the cloud\. However, local testing doesn’t validate everything, such as permissions between your resources in the cloud\. As much as possible, test your applications in the cloud\. We recommend [using `sam sync`](using-sam-cli-sync.md) to speed up your cloud testing workflows\.

## Learn more<a name="using-sam-cli-local-start-api-learn"></a>

For a list of all `sam local start-api` options, see [sam local start\-api](sam-cli-command-reference-sam-local-start-api.md)\.