# Using sam build<a name="using-sam-cli-build"></a>

Use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam build` command to prepare your serverless application for subsequent steps in your development workflow, such as local testing or deploying to the AWS Cloud\. This command creates a `.aws-sam` directory that structures your application in a format and location that `sam local` and `sam deploy` require\.
+ For an introduction to the AWS SAM CLI, see [What is the AWS SAM CLI?](what-is-sam.md#what-is-sam-cli)\.
+ For a list of `sam build` command options, see [sam build](sam-cli-command-reference-sam-build.md)\.
+ For an example of using `sam build` during a typical development workflow, see [Step 2: Build your application](serverless-getting-started-hello-world.md#serverless-getting-started-hello-world-build)\.

**Note**  
Using `sam build` requires that you start with the basic components of a serverless application on your development machine\. This includes an AWS SAM template, AWS Lambda function code, and any language\-specific files and dependencies\. To learn more, see [Using sam init](using-sam-cli-init.md)\.

**Topics**
+ [Building applications with sam build](#using-sam-cli-build-apps)
+ [Local testing and deployment](#using-sam-cli-build-test-deploy)
+ [Best practices](#using-sam-cli-build-best)
+ [Options for sam build](#using-sam-cli-build-options)
+ [Examples](#using-sam-cli-build-examples)
+ [Learn more](#using-sam-cli-build-learn)

## Building applications with sam build<a name="using-sam-cli-build-apps"></a>

Before using `sam build`, consider and configure the following:

1. **Lambda functions and layers** – The `sam build` command can build Lambda functions and layers\. To learn more about Lambda layers, see [Building layers](building-layers.md)\.

1. **Lambda runtime** – The *runtime* provides a language\-specific environment that runs your function in an execution environment when invoked\. You can configure native and custom runtimes\.

   1. **Native runtime** – Author your Lambda functions in a supported Lambda runtime and build you functions to use a native Lambda runtime in the AWS Cloud\.

   1. **Custom runtime** – Author your Lambda functions using any programming language and build your runtime using a custom process defined in a makefile or third\-party builder such as esbuild\. To learn more, see [Building custom runtimes](building-custom-runtimes.md)\.

1. **Lambda package type** – Lambda functions can be packaged in the following Lambda deployment package types:

   1. **\.zip file archive** – Contains your application code and its dependencies\.

   1. **Container image** – Contains the base operating system, the runtime, Lambda extensions, your application code and its dependencies\.

These application settings can be configured when initializing an application using `sam init`\.
+ To learn more about using `sam init`, see [Using sam init](using-sam-cli-init.md)\.
+ To learn more about configuring these settings in your application, see [Building applications](serverless-sam-cli-using-build.md)\.

**To build an application**

1. `cd` to the root of your project\. This is the same location as your AWS SAM template\.

   ```
   $ cd sam-app
   ```

1. Run the following:

   ```
   sam-app $ sam build <arguments> <options>
   ```
**Note**  
A commonly used option is `--use-container`\. To learn more, see [Building a Lambda function inside of a provided container](#using-sam-cli-build-options-container)\.

   The following is an example of the AWS SAM CLI output:

   ```
   sam-app $ sam build
   Starting Build use cache
   Manifest file is changed (new hash: 3298f1304...d4d421) or dependency folder (.aws-sam/deps/4d3dfad6-a267-47a6-a6cd-e07d6fae318c) is missing for (HelloWorldFunction), downloading dependencies and copying/building source
   Building codeuri: /Users/.../sam-app/hello_world runtime: python3.9 metadata: {} architecture: x86_64 functions: HelloWorldFunction
   Running PythonPipBuilder:CleanUp
   Running PythonPipBuilder:ResolveDependencies
   Running PythonPipBuilder:CopySource
   Running PythonPipBuilder:CopySource
   
   Build Succeeded
   
   Built Artifacts  : .aws-sam/build
   Built Template   : .aws-sam/build/template.yaml
   
   Commands you can use next
   =========================
   [*] Validate SAM template: sam validate
   [*] Invoke Function: sam local invoke
   [*] Test Function in the Cloud: sam sync --stack-name {{stack-name}} --watch
   [*] Deploy: sam deploy --guided
   ```

1. The AWS SAM CLI creates a `.aws-sam` build directory\. The following is an example:

   ```
   .aws-sam
   ├── build
   │   ├── HelloWorldFunction
   │   │   ├── __init__.py
   │   │   ├── app.py
   │   │   └── requirements.txt
   │   └── template.yaml
   └── build.toml
   ```

Depending on how your application is configured, the AWS SAM CLI does the following:

1. Downloads, installs, and organizes dependencies in the `.aws-sam/build` directory\.

1. Prepares your Lambda code\. This can include compiling your code, creating executable binaries, and building container images\.

1. Copies build artifacts to the `.aws-sam` directory\. The format will vary based on your application package type\.

   1. For \.zip package types, the artifacts are not zipped yet so that they can be used for local testing\. The AWS SAM CLI zips your application when using `sam deploy`\.

   1. For container image package types, a container image is created locally and referenced in the `.aws-sam/build.toml` file\.

1. Copies the AWS SAM template over to the `.aws-sam` directory and modifies it with new file paths when necessary\.

The following are the major components that make up your build artifacts in the `.aws-sam` directory:
+ **The build directory** – Contains your Lambda functions and layers structured independently of each other\. This results in a unique structure for each function or layer in the `.aws-sam/build` directory\.
+ **The AWS SAM template** – Modified with updated values based on changes during the build process\.
+ **The build\.toml file** – A configuration file that contains build settings used by the AWS SAM CLI\.

## Local testing and deployment<a name="using-sam-cli-build-test-deploy"></a>

When performing local testing with `sam local` or deployment with `sam deploy`, the AWS SAM CLI does the following:

1. It first checks to see if an `.aws-sam` directory exists and if an AWS SAM template is located within that directory\. If these conditions are met, the AWS SAM CLI considers this as the root directory of your application\.

1. If these conditions are not met, the AWS SAM CLI considers the original location of your AWS SAM template as the root directory of your application\.

When developing, if changes are made to your original application files, run `sam build` to update the `.aws-sam` directory before testing locally\.

## Best practices<a name="using-sam-cli-build-best"></a>
+ Don’t edit any code under the `.aws-sam/build` directory\. Instead, update your original source code in your project folder and run `sam build` to update the `.aws-sam/build` directory\.
+ When you modify your original files, run `sam build` to update the `.aws-sam/build` directory\.
+ You may want the AWS SAM CLI to reference your project’s original root directory instead of the `.aws-sam` directory, such as when developing and testing with `sam local`\. Delete the `.aws-sam` directory or the AWS SAM template in the `.aws-sam` directory to have the AWS SAM CLI recognize your original project directory as the root project directory\. When ready, run `sam build` again to create the `.aws-sam` directory\.
+ When you run `sam build`, the `.aws-sam/build` directory gets overwritten each time\. The `.aws-sam` directory does not\. If you want to store files, such as logs, store them in `.aws-sam` to prevent them from being overwritten\.

## Options for sam build<a name="using-sam-cli-build-options"></a>

### Building a single resource<a name="using-sam-cli-build-options-resource"></a>

Provide the resource’s logical ID to build only that resource\. The following is an example:

```
$ sam build HelloWorldFunction
```

To build a resource of a nested application or stack, provide the application or stack logical ID along with the resource logical ID using the format `<stack-logical-id>/<resource-logical-id>` :

```
$ sam build MyNestedStack/MyFunction
```

### Building a Lambda function inside of a provided container<a name="using-sam-cli-build-options-container"></a>

The `--use-container` option downloads a container image and uses it to build your Lambda functions\. The local container is then referenced in your `.aws-sam/build.toml` file\.

This option requires Docker to be installed\. For instructions, see [Installing Docker](install-docker.md)\.

The following is an example of this command:

```
$ sam build --use-container
```

You can specify the container image to use with the `--build-image` option\. The following is an example:

```
$ sam build --use-container --build-image amazon/aws-sam-cli-build-image-nodejs12.x
```

To specify the container image to use for a single function, provide the function logical ID\. The following is an example:

```
$ sam build --use-container --build-image Function1=amazon/aws-sam-cli-build-image-python3.8
```

### Pass environment variables to the build container<a name="using-sam-cli-build-options-env"></a>

Use the `--container-env-var` to pass environment variables to the build container\. The following is an example:

```
$ sam build --use-container --container-env-var Function1.GITHUB_TOKEN=<token1> --container-env-var GLOBAL_ENV_VAR=<global-token>
```

To pass environment variables from a file, use the `--container-env-var-file` option\. The following is an example:

```
$ sam build --use-container --container-env-var-file <env.json>
```

Example of the `env.json` file:

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

### Speed up the building of applications that contain multiple functions<a name="using-sam-cli-build-options-speed"></a>

When you run `sam build` on an application with multiple functions, the AWS SAM CLI builds each function one at a time\. To speed up the build process, use the `--parallel` option\. This builds all of your functions and layers at the same time\.

The following is an example of this command:

```
$ sam build —-parallel
```

## Examples<a name="using-sam-cli-build-examples"></a>

### Building an application that uses a native runtime and \.zip package type<a name="using-sam-cli-build-examples-tutorial1"></a>

For this example, see [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md)\.

### Building an application that uses a native runtime and image package type<a name="using-sam-cli-build-examples-image"></a>

First, we run `sam init` to initialize a new application\. During the interactive flow, we select the `Image` package type\. The following is an example:

```
$ sam init
...
Which template source would you like to use?
        1 - AWS Quick Start Templates
        2 - Custom Template Location
Choice: 1

Choose an AWS Quick Start application template
        1 - Hello World Example
        2 - Multi-step workflow
        3 - Serverless API
        4 - Scheduled task
        5 - Standalone function
        6 - Data processing
        7 - Hello World Example With Powertools
        8 - Infrastructure event management
        9 - Serverless Connector Hello World Example
        10 - Multi-step workflow with Connectors
        11 - Lambda EFS example
        12 - DynamoDB Example
        13 - Machine Learning
Template: 1

Use the most popular runtime and package type? (Python and zip) [y/N]: ENTER

Which runtime would you like to use?
        ...
        11 - java8
        12 - nodejs18.x
        13 - nodejs16.x
        14 - nodejs14.x
        ...
Runtime: 12

What package type would you like to use?
        1 - Zip
        2 - Image
Package type: 2

Based on your selections, the only dependency manager available is npm.
We will proceed copying the template using npm.

Would you like to enable X-Ray tracing on the function(s) in your application?  [y/N]: ENTER

Would you like to enable monitoring using CloudWatch Application Insights?
For more info, please view https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-application-insights.html [y/N]: ENTER

Project name [sam-app]: ENTER

Cloning from https://github.com/aws/aws-sam-cli-app-templates (process may take a moment)

    -----------------------
    Generating application:
    -----------------------
    Name: sam-app
    Base Image: amazon/nodejs18.x-base
    Architectures: x86_64
    Dependency Manager: npm
    Output Directory: .
    Configuration file: sam-app/samconfig.toml

    Next steps can be found in the README file at sam-app/README.md
    
...
```

The AWS SAM CLI initializes an application and creates the following project directory:

```
sam-app
├── README.md
├── events
│   └── event.json
├── hello-world
│   ├── Dockerfile
│   ├── app.mjs
│   ├── package.json
│   └── tests
│       └── unit
│           └── test-handler.mjs
├── samconfig.toml
└── template.yaml
```

Next, we run `sam build` to build our application:

```
sam-app $ sam build
Building codeuri: /Users/.../build-demo/sam-app runtime: None metadata: {'DockerTag': 'nodejs18.x-v1', 'DockerContext': '/Users/.../build-demo/sam-app/hello-world', 'Dockerfile': 'Dockerfile'} architecture: arm64 functions: HelloWorldFunction
Building image for HelloWorldFunction function
Setting DockerBuildArgs: {} for HelloWorldFunction function
Step 1/4 : FROM public.ecr.aws/lambda/nodejs:18
 ---> f5b68038c080
Step 2/4 : COPY app.mjs package*.json ./
 ---> Using cache
 ---> 834e565aae80
Step 3/4 : RUN npm install
 ---> Using cache
 ---> 31c2209dd7b5
Step 4/4 : CMD ["app.lambdaHandler"]
 ---> Using cache
 ---> 2ce2a438e89d
Successfully built 2ce2a438e89d
Successfully tagged helloworldfunction:nodejs18.x-v1

Build Succeeded

Built Artifacts  : .aws-sam/build
Built Template   : .aws-sam/build/template.yaml

Commands you can use next
=========================
[*] Validate SAM template: sam validate
[*] Invoke Function: sam local invoke
[*] Test Function in the Cloud: sam sync --stack-name {{stack-name}} --watch
[*] Deploy: sam deploy --guided
```

### Building an application that includes a compiled programming language<a name="using-sam-cli-build-examples-compiled"></a>

In this example, we build an application that contains a Lambda function using the Go runtime\.

First, we initialize a new application using `sam init` and configure our application to use Go:

```
$ sam init

...

Which template source would you like to use?
        1 - AWS Quick Start Templates
        2 - Custom Template Location
Choice: 1

Choose an AWS Quick Start application template
        1 - Hello World Example
        2 - Multi-step workflow
        3 - Serverless API
        ...
Template: 1

Use the most popular runtime and package type? (Python and zip) [y/N]: ENTER

Which runtime would you like to use?
        ...
        4 - dotnetcore3.1
        5 - go1.x
        6 - go (provided.al2)
        ...
Runtime: 5

What package type would you like to use?
        1 - Zip
        2 - Image
Package type: 1

Based on your selections, the only dependency manager available is mod.
We will proceed copying the template using mod.

Would you like to enable X-Ray tracing on the function(s) in your application?  [y/N]: ENTER

Would you like to enable monitoring using CloudWatch Application Insights?
For more info, please view https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-application-insights.html [y/N]: ENTER

Project name [sam-app]: ENTER

Cloning from https://github.com/aws/aws-sam-cli-app-templates (process may take a moment)

    -----------------------
    Generating application:
    -----------------------
    Name: sam-app
    Runtime: go1.x
    Architectures: x86_64
    Dependency Manager: mod
    Application Template: hello-world
    Output Directory: .
    Configuration file: sam-app/samconfig.toml
    
    Next steps can be found in the README file at sam-app-go/README.md
        
...
```

The AWS SAM CLI initializes the application\. The following is an example of the application directory structure:

```
sam-app
├── Makefile
├── README.md
├── events
│   └── event.json
├── hello-world
│   ├── go.mod
│   ├── go.sum
│   ├── main.go
│   └── main_test.go
├── samconfig.toml
└── template.yaml
```

We reference the `README.md` file for this application’s requirements\.

```
...
## Requirements
* AWS CLI already configured with Administrator permission
* [Docker installed](https://www.docker.com/community-edition)
* [Golang](https://golang.org)
* SAM CLI - [Install the SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)
...
```

Next, we run `sam local invoke` to test our function\. This command errors since Go is not installed on our local machine:

```
sam-app $ sam local invoke
Invoking hello-world (go1.x)
Local image was not found.
Removing rapid images for repo public.ecr.aws/sam/emulation-go1.x
Building image.................................................................................................................................................................................................................................................
Using local image: public.ecr.aws/lambda/go:1-rapid-x86_64.

Mounting /Users/.../Playground/build/sam-app/hello-world as /var/task:ro,delegated inside runtime container
START RequestId: c6c5eddf-042b-4e1e-ba66-745f7c86dd31 Version: $LATEST
fork/exec /var/task/hello-world: no such file or directory: PathError
null
END RequestId: c6c5eddf-042b-4e1e-ba66-745f7c86dd31
REPORT RequestId: c6c5eddf-042b-4e1e-ba66-745f7c86dd31  Init Duration: 0.88 ms  Duration: 175.75 ms Billed Duration: 176 ms Memory Size: 128 MB     Max Memory Used: 128 MB
{"errorMessage":"fork/exec /var/task/hello-world: no such file or directory","errorType":"PathError"}%
```

Next, we run `sam build` to build our application\. We encounter an error since Go is not installed on our local machine:

```
sam-app $ sam build
Starting Build use cache
Cache is invalid, running build and copying resources for following functions (HelloWorldFunction)
Building codeuri: /Users/.../Playground/build/sam-app/hello-world runtime: go1.x metadata: {} architecture: x86_64 functions: HelloWorldFunction

Build Failed
Error: GoModulesBuilder:Resolver - Path resolution for runtime: go1.x of binary: go was not successful
```

While we could configure our local machine to properly build our function, we instead use the `--use-container` option with `sam build`\. The AWS SAM CLI downloads a container image, builds our function using the native GoModulesBuilder, and copies the resulting binary to our `.aws-sam/build/HelloWorldFunction` directory\.

```
sam-app $ sam build --use-container
Starting Build use cache
Starting Build inside a container
Cache is invalid, running build and copying resources for following functions (HelloWorldFunction)
Building codeuri: /Users/.../build/sam-app/hello-world runtime: go1.x metadata: {} architecture: x86_64 functions: HelloWorldFunction

Fetching public.ecr.aws/sam/build-go1.x:latest-x86_64 Docker container image.....................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................
Mounting /Users/.../build/sam-app/hello-world as /tmp/samcli/source:ro,delegated inside runtime container
Running GoModulesBuilder:Build

Build Succeeded

Built Artifacts  : .aws-sam/build
Built Template   : .aws-sam/build/template.yaml

Commands you can use next
=========================
[*] Validate SAM template: sam validate
[*] Invoke Function: sam local invoke
[*] Test Function in the Cloud: sam sync --stack-name {{stack-name}} --watch
[*] Deploy: sam deploy --guided
```

The following is an example of the `.aws-sam` directory:

```
.aws-sam
├── build
│   ├── HelloWorldFunction
│   │   └── hello-world
│   └── template.yaml
├── build.toml
├── cache
│   └── c860d011-4147-4010-addb-2eaa289f4d95
│       └── hello-world
└── deps
```

Next, we run `sam local invoke`\. Our function is successfully invoked:

```
sam-app $ sam local invoke
Invoking hello-world (go1.x)
Local image is up-to-date
Using local image: public.ecr.aws/lambda/go:1-rapid-x86_64.

Mounting /Users/.../Playground/build/sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated inside runtime container
START RequestId: cfc8ffa8-29f2-49d4-b461-45e8c7c80479 Version: $LATEST
END RequestId: cfc8ffa8-29f2-49d4-b461-45e8c7c80479
REPORT RequestId: cfc8ffa8-29f2-49d4-b461-45e8c7c80479  Init Duration: 1.20 ms  Duration: 1782.46 ms        Billed Duration: 1783 ms        Memory Size: 128 MB     Max Memory Used: 128 MB
{"statusCode":200,"headers":null,"multiValueHeaders":null,"body":"Hello, 72.21.198.67\n"}%
```

## Learn more<a name="using-sam-cli-build-learn"></a>

To learn more about using the `sam build` command, see the following:
+ **[Learning AWS SAM: sam build](https://www.youtube.com/watch?v=fDhYKp4op_g)** – Serverless Land "Learning AWS SAM" series on YouTube\.
+ **[Learning AWS SAM \| sam build \| E3 ](https://www.youtube.com/watch?v=vsAvRyLnB7Y)** – Serverless Land "Learning AWS SAM" series on YouTube\.
+ **[AWS SAM build: how it provides artifacts for deployment \(Sessions With SAM S2E8\)](https://www.youtube.com/watch?v=bNbBd6XoDHg)** – Sessions with AWS SAM series on YouTube\.
+ **[AWS SAM custom builds: How to use Makefiles to customize builds in SAM \(S2E9\)](https://www.youtube.com/watch?v=wpccutnSbAk)** – Sessions with AWS SAM series on YouTube\.