# Building applications<a name="serverless-sam-cli-using-build"></a>

To build your serverless application, use the `sam build` command\. This command also gathers the build artifacts of your application's dependencies and places them in the proper format and location for next steps, such as locally testing, packaging, and deploying\.

You specify your application's dependencies in a manifest file, such as `requirements.txt` \(Python\) or `package.json` \(Node\.js\), or by using the `Layers` property of a function resource\. The `Layers` property contains a list of [AWS Lambda layer](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html) resources that the Lambda function depends on\.

The format of your application's build artifacts depends on each function's `PackageType` property\. The options for this property are:
+ **`Zip`** – A \.zip file archive, which contains your application code and its dependencies\. If you package your code as a \.zip file archive, you must specify a Lambda runtime for your function\.
+ **`Image`** – A container image, which includes the base operating system, runtime, and extensions, in addition to your application code and its dependencies\.

For more information about Lambda package types, see [Lambda deployment packages](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-package.html) in the *AWS Lambda Developer Guide*\.

## Building a \.zip file archive<a name="build-zip-archive"></a>

To build your serverless application as a \.zip file archive, declare `PackageType: Zip` for your serverless function\.

If your Lambda function depends on packages that have natively compiled programs, use the `--use-container` flag\. This flag locally compiles your functions in a Docker container that behaves like a Lambda environment, so they're in the right format when you deploy them to the AWS Cloud\.

When you use the `--use-container` option, by default AWS SAM pulls the container image from [Amazon ECR Public](https://docs.aws.amazon.com/AmazonECR/latest/public/what-is-ecr.html)\. If you would like to pull a container image from another repository, for example DockerHub, you can use the `--build-image` option and provide the URI of an alternate container image\. Following are two example commands for building applications using container images from the DockerHub repository:

```
# Build a Node.js 12 application using a container image pulled from DockerHub
sam build --use-container --build-image amazon/aws-sam-cli-build-image-nodejs12.x

# Build a function resource using using the Python 3.8 container image pulled from DockerHub
sam build --use-container --build-image Function1=amazon/aws-sam-cli-build-image-python3.8
```

For a list of URIs you can use with `--build-image`, see [Image repositories](serverless-image-repositories.md) which contains DockerHub URIs for a number of supported runtimes\.

For additional examples of building a \.zip file archive application, see the Examples section later in this topic\.

## Building a container image<a name="build-container-image"></a>

To build your serverless application as a container image, declare `PackageType: Image` for your serverless function\. You must also declare the `Metadata` resource attribute with the following entries:

`Dockerfile`  
The name of the Dockerfile associated with the Lambda function\.

`DockerContext`  
The location of the Dockerfile\.

`DockerTag`  
\(Optional\) A tag to apply to the built image\.

`DockerBuildArgs`  
Build arguments for the build\.

The following is an example `Metadata` resource attribute section:

```
    Metadata:
      Dockerfile: Dockerfile
      DockerContext: ./hello_world
      DockerTag: v1
```

To download a sample application that's configured with the `Image` package type, see [Step 1: Download a sample AWS SAM application](serverless-getting-started-hello-world.md#serverless-getting-started-hello-world-initialize) in **Tutorial: Deploying a Hello World application**\. At the prompt asking which package type you want to install, choose `Image`\.

## Container environment variable file<a name="serverless-sam-cli-using-container-environment-file"></a>

To provide a JSON file that contains environment variables for the build container, use the `--container-env-var-file` argument with the `sam build` command\. You can provide a single environment variable that applies to all serverless resources, or different environment variables for each resource\.

### Format<a name="serverless-sam-cli-using-container-environment-file-format"></a>

The format for passing environment variables to a build container depends on how many environment variables you provide for your resources\.

To provide a single environment variable for all resources, specify a `Parameters` object like the following:

```
{
  "Parameters": {
    "GITHUB_TOKEN": "TOKEN_GLOBAL"
  }
}
```

To provide different environment variables for each resource, specify objects for each resource like the following:

```
{
  "MyFunction1": {
    "GITHUB_TOKEN": "TOKEN1"
  },
  "MyFunction2": {
    "GITHUB_TOKEN": "TOKEN2"
  }
}
```

Save your environment variables as a file, for example, named `env.json`\. The following command uses this file to pass your environment variables to the build container:

```
sam build --use-container --container-env-var-file env.json
```

### Precedence<a name="serverless-sam-cli-using-container-environment-file-precedence"></a>
+ The environment variables that you provide for specific resources take precedence over the single environment variable for all resources\.
+ Environment variables that you provide on the command line take precedence over environment variables in a file\.

## Examples<a name="building-applications-examples"></a>

### Example 1: \.zip file archive<a name="examples-zip-archives"></a>

The following `sam build` commands build a \.zip file archive:

```
# Build all functions and layers, and their dependencies
sam build

# Run the build process inside a Docker container that functions like a Lambda environment
sam build --use-container

# Build a Node.js 12 application using a container image pulled from DockerHub
sam build --use-container --build-image amazon/aws-sam-cli-build-image-nodejs12.x

# Build a function resource using using the Python 3.8 container image pulled from DockerHub
sam build --use-container --build-image Function1=amazon/aws-sam-cli-build-image-python3.8 

# Build and run your functions locally
sam build && sam local invoke

# For more options
sam build --help
```

### Example 2: Container image<a name="examples-container-image-1"></a>

The following AWS SAM template builds as a container image:

```
Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function
    Properties:
      PackageType: Image
      ImageConfig:
        Command: ["app.lambda_handler"]
    Metadata:
      Dockerfile: Dockerfile
      DockerContext: ./hello_world
      DockerTag: v1
```

The following is an example Dockerfile:

```
FROM public.ecr.aws/lambda/python:3.8

COPY app.py requirements.txt ./

RUN python3.8 -m pip install -r requirements.txt

# Overwrite the command by providing a different command directly in the template.
CMD ["app.lambda_handler"]
```