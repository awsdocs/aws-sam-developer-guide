# Building \.NET 7 Lambda functions with Native AOT compilation<a name="build-dotnet7"></a>

Build and package your \.NET 7 AWS Lambda functions with the AWS Serverless Application Model \(AWS SAM\), utilizing Native Ahead\-of\-Time \(AOT\) compilation to improve AWS Lambda cold\-start times\.

**Topics**
+ [\.NET 7 Native AOT overview](#build-dotnet7-overview)
+ [Using AWS SAM with your \.NET 7 Lambda functions](#build-dotnet7-sam)
+ [Install prerequisites](#build-dotnet7-prerequisites)
+ [Define \.NET 7 Lambda functions in your AWS SAM template](#build-dotnet7-sam-define)
+ [Build your application with the AWS SAM CLI](#build-dotnet7-sam-build)
+ [Learn more](#build-dotnet7-learn-more)

## \.NET 7 Native AOT overview<a name="build-dotnet7-overview"></a>

Historically, \.NET Lambda functions have cold\-start times which impact user experience, system latency, and usage costs of your serverless applications\. With \.NET 7, Microsoft adds support for Native AOT compilation, which speeds up performance by compiling \.NET code directly to machine and operating system native code, eliminating Just\-in\-Time \(JIT\) compiling at runtime\. With \.NET 7 Native AOT compilation, you can improve cold\-start times of your Lambda functions\. To learn more about Native AOT for \.NET 7, see [Using Native AOT](https://github.com/dotnet/runtime/tree/main/src/coreclr/nativeaot#readme) in the *Dotnet GitHub repository*\.

## Using AWS SAM with your \.NET 7 Lambda functions<a name="build-dotnet7-sam"></a>

Do the following to configure your \.NET 7 Lambda functions with the AWS Serverless Application Model \(AWS SAM\):
+ Install prerequisites on your development machine\.
+ Define \.NET 7 Lambda functions in your AWS SAM template\.
+ Build your application with the AWS SAM CLI\.

## Install prerequisites<a name="build-dotnet7-prerequisites"></a>

The following are required prerequisites:
+ The AWS SAM CLI
+ The \.NET Core CLI
+ The Amazon\.Lambda\.Tools \.NET Core Global Tool
+ Docker

**Install the AWS SAM CLI**

1. To check if you already have the AWS SAM CLI installed, run the following:

   ```
   sam --version
   ```

1. To install the AWS SAM CLI, see [Installing the AWS SAM CLI](install-sam-cli.md)\.

1. To upgrade an installed version of the AWS SAM CLI, see [Upgrading the AWS SAM CLI](manage-sam-cli-versions.md#manage-sam-cli-versions-upgrade)\.

**Install the \.NET Core CLI**

1. To download and install the \.NET Core CLI, see [Download \.NET](https://dotnet.microsoft.com/download) from Microsoft's website\.

1. For more information on the \.NET Core CLI, see [\.NET Core CLI](https://docs.aws.amazon.com/lambda/latest/dg/csharp-package-cli.html) in the *AWS Lambda Developer Guide*\.

**Install the Amazon\.Lambda\.Tools \.NET Core Global Tool**

1. Run the following command:

   ```
   dotnet tool install -g Amazon.Lambda.Tools
   ```

1. If you already have the tool installed, you can make sure that it is the latest version using the following command:

   ```
   dotnet tool update -g Amazon.Lambda.Tools
   ```

1. For more information about the Amazon\.Lambda\.Tools \.NET Core Global Tool, see the [AWS Extensions for \.NET CLI](https://github.com/aws/aws-extensions-for-dotnet-cli) repository on GitHub\.

**Install Docker**
+ Building with Native AOT, requires Docker to be installed\. For installation instructions, see [Installing Docker to use with the AWS SAM CLI](install-docker.md)\.

## Define \.NET 7 Lambda functions in your AWS SAM template<a name="build-dotnet7-sam-define"></a>

To define a \.NET7 Lambda function in your AWS SAM template, do the following:
+ Define a custom runtime by setting `Runtime` to `provided.al2`\. We define a custom runtime because a \.NET 7 runtime option is not available\.
+ Add a `Metadata` object to your `AWS::Serverless::Function` resource and specify `dotnet7` for the `BuildMethod`\.

```
Resources:
HelloWorldFunction:
  Type: AWS::Serverless::Function
  Properties:
    CodeUri: function-source-folder
    Handler: app.handler
    Runtime: provided.al2
    Architectures:
      - x86_64
    Events:
      HelloWorld:
        Type: Api 
        Properties:
          Path: /hello
          Method: get
  Metadata:
    BuildMethod: dotnet7
```

**Note**  
For the `Architectures` property, `x86_64` is the only supported option because \.NET 7 cannot run on `arm64`\. For more information, see the [Reconsider \.NET 7 build environment GitHub issue](https://github.com/dotnet/runtime/issues/76195)\.

## Build your application with the AWS SAM CLI<a name="build-dotnet7-sam-build"></a>

 From your project's root directory, run `sam build` to begin building your application\. If the `PublishAot` property has been defined in your \.NET 7 project file, the AWS SAM CLI will build with Native AOT compilation\. To learn more about the `PublishAot` property, see [Native AOT Deployment](https://learn.microsoft.com/en-us/dotnet/core/deploying/native-aot/) in Microsoft's *\.NET documentation*\.

To build your function, the AWS SAM CLI invokes the \.NET Core CLI which uses the Amazon\.Lambda\.Tools \.NET Core Global Tool\.

**Note**  
When building, if a `.sln` file exists in the same or parent directory of your project, the directory containing the `.sln` file will be mounted to the container\. If a `.sln` file is not found, only the project folder is mounted\. Therefore, if you are building a multi\-project application, ensure the `.sln` file is property located\.

## Learn more<a name="build-dotnet7-learn-more"></a>

For more information on building \.NET 7 Lambda functions, see [Building serverless applications on Lambda using \.NET 7](http://aws.amazon.com/blogs/compute/building-serverless-net-applications-on-aws-lambda-using-net-7/)\.

For a reference of the sam build command, see [sam build](sam-cli-command-reference-sam-build.md)\.