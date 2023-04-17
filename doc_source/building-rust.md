# Building Rust Lambda functions with Cargo Lambda<a name="building-rust"></a>


|  | 
| --- |
| This feature is in preview release for AWS SAM and is subject to change\. | 

Use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) with your Rust AWS Lambda functions\.

**Topics**
+ [Prerequisites](#building-rust-prerequisites)
+ [Configuring AWS SAM to use with Rust Lambda functions](#building-rust-configure)
+ [Examples](#building-rust-examples)

## Prerequisites<a name="building-rust-prerequisites"></a>

**Rust language**  
To install Rust, see [Install Rust](https://www.rust-lang.org/tools/install) in the *Rust language website*\.

**Cargo Lambda**  
The AWS SAM CLI requires installation of [https://www.cargo-lambda.info/guide/what-is-cargo-lambda.html](https://www.cargo-lambda.info/guide/what-is-cargo-lambda.html), a subcommand for Cargo\. For installation instructions, see [Installation](https://www.cargo-lambda.info/guide/installation.html) in the *Cargo Lambda documentation*\.

**Docker**  
Building and testing Rust Lambda functions requires Docker\. For installation instructions, see [Installing Docker](install-docker.md)\.

**Opt in to AWS SAM CLI beta feature**  
Since this feature is in preview, you must opt in using one of the following methods:  

1. Use the environment variable: `SAM_CLI_BETA_RUST_CARGO_LAMBDA=1`\.

1. Add the following to your `samconfig.toml` file:

   ```
   [default.build.parameters]
   beta_features = true
   [default.sync.parameters]
   beta_features = true
   ```

1. Use the `--beta-features` option when using a supported AWS SAM CLI command\. For example:

   ```
   $ sam build --beta-features
   ```

1. Choose option `y` when the AWS SAM CLI prompts you to opt in\. The following is an example:

   ```
   $ sam build
   Starting Build use cache
   Build method "rust-cargolambda" is a beta feature.
   Please confirm if you would like to proceed
   You can also enable this beta feature with "sam build --beta-features". [y/N]: y
   ```

## Configuring AWS SAM to use with Rust Lambda functions<a name="building-rust-configure"></a>

### Step 1: Configure your AWS SAM template<a name="building-rust-configure-template"></a>

Configure your AWS SAM template with the following:
+ **Binary** – Optional\. Specify when your template contains multiple Rust Lambda functions\.
+ **BuildMethod** – `rust-cargolambda`\.
+ **CodeUri** – path to your `Cargo.toml` file\.
+ **Handler** – `bootstrap`\.
+ **Runtime** – `provided.al2`\.

To learn more about custom runtimes, see [Custom AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-custom.html) in the *AWS Lambda Developer Guide*\.

Here is an example of a configured AWS SAM template:

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Metadata:
      BuildMethod: rust-cargolambda
      BuildProperties: function_a
    Properties:
      CodeUri: ./rust_app
      Handler: bootstrap
      Runtime: provided.al2
...
```

### Step 2: Use the AWS SAM CLI with your Rust Lambda function<a name="building-rust-configure-cli"></a>

Use any AWS SAM CLI command with your AWS SAM template\. For more information, see [Using the AWS SAM CLI](using-sam-cli.md)\.

## Examples<a name="building-rust-examples"></a>

### Hello World example<a name="building-rust-examples-hello"></a>

**In this example, we build the sample Hello World application using Rust as our runtime\.**

First, we initialize a new serverless application using `sam init`\. During the interactive flow, we select the **Hello World application** and choose the **Rust** runtime\.

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
        1 - aot.dotnet7 (provided.al2)
        2 - dotnet6
        3 - dotnet5.0
        ...
        18 - python3.7
        19 - python3.10
        20 - ruby2.7
        21 - rust (provided.al2)
Runtime: 21

Based on your selections, the only Package type available is Zip.
We will proceed to selecting the Package type as Zip.

Based on your selections, the only dependency manager available is cargo.
We will proceed copying the template using cargo.

Would you like to enable X-Ray tracing on the function(s) in your application?  [y/N]: ENTER

Would you like to enable monitoring using CloudWatch Application Insights?
For more info, please view https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-application-insights.html [y/N]: ENTER

Project name [sam-app]: hello-rust

    -----------------------
    Generating application:
    -----------------------
    Name: hello-rust
    Runtime: rust (provided.al2)
    Architectures: x86_64
    Dependency Manager: cargo
    Application Template: hello-world
    Output Directory: .
    Configuration file: hello-rust/samconfig.toml
    
    Next steps can be found in the README file at hello-rust/README.md
        

Commands you can use next
=========================
[*] Create pipeline: cd hello-rust && sam pipeline init --bootstrap
[*] Validate SAM template: cd hello-rust && sam validate
[*] Test Function in the Cloud: cd hello-rust && sam sync --stack-name {stack-name} --watch
```

The following is the structure of our Hello World application:

```
hello-rust
├── README.md
├── events
│   └── event.json
├── rust_app
│   ├── Cargo.toml
│   └── src
│       └── main.rs
├── samconfig.toml
└── template.yaml
```

In our AWS SAM template, our Rust function is defined as the following:

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function 
    Metadata:
      BuildMethod: rust-cargolambda 
    Properties:
      CodeUri: ./rust_app 
      Handler: bootstrap   
      Runtime: provided.al2
      Architectures:
        - x86_64
      Events:
        HelloWorld:
          Type: Api
            Path: /hello
            Method: get
```

Next, we run `sam build` to build our application and prepare for deployment\. The AWS SAM CLI creates a `.aws-sam` directory and organizes our build artifacts there\. Our function is built using Cargo Lambda and stored as an executable binary at `.aws-sam/build/HelloWorldFunction/bootstrap`\.

```
hello-rust$ sam build
Starting Build use cache
Build method "rust-cargolambda" is a beta feature.
Please confirm if you would like to proceed
You can also enable this beta feature with "sam build --beta-features". [y/N]: y

Experimental features are enabled for this session.
Visit the docs page to learn more about the AWS Beta terms https://aws.amazon.com/service-terms/.

Cache is invalid, running build and copying resources for following functions (HelloWorldFunction)
Building codeuri: /Users/.../hello-rust/rust_app runtime: provided.al2 metadata: {'BuildMethod': 'rust-cargolambda'} architecture: x86_64 functions: HelloWorldFunction
Running RustCargoLambdaBuilder:CargoLambdaBuild
Running RustCargoLambdaBuilder:RustCopyAndRename

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

Next, we deploy our application using `sam deploy --guided`\.

```
hello-rust$ sam deploy --guided

Configuring SAM deploy
======================

        Looking for config file [samconfig.toml] :  Found
        Reading default arguments  :  Success

        Setting default arguments for 'sam deploy'
        =========================================
        Stack Name [hello-rust]: ENTER
        AWS Region [us-west-2]: ENTER
        #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
        Confirm changes before deploy [Y/n]: ENTER
        #SAM needs permission to be able to create roles to connect to the resources in your template
        Allow SAM CLI IAM role creation [Y/n]: ENTER
        #Preserves the state of previously provisioned resources when an operation fails
        Disable rollback [y/N]: ENTER
        HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
        Save arguments to configuration file [Y/n]: ENTER
        SAM configuration file [samconfig.toml]: ENTER
        SAM configuration environment [default]: ENTER

        Looking for resources needed for deployment:

        ...

        Uploading to hello-rust/56ba6585d80577dd82a7eaaee5945c0b  817973 / 817973  (100.00%)

        Deploying with following values
        ===============================
        Stack name                   : hello-rust
        Region                       : us-west-2
        Confirm changeset            : True
        Disable rollback             : False
        Deployment s3 bucket         : aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr
        Capabilities                 : ["CAPABILITY_IAM"]
        Parameter overrides          : {}
        Signing Profiles             : {}

Initiating deployment
=====================

        Uploading to hello-rust/a4fc54cb6ab75dd0129e4cdb564b5e89.template  1239 / 1239  (100.00%)


Waiting for changeset to be created..

CloudFormation stack changeset
---------------------------------------------------------------------------------------------------------
Operation                  LogicalResourceId          ResourceType               Replacement              
---------------------------------------------------------------------------------------------------------
+ Add                      HelloWorldFunctionHelloW   AWS::Lambda::Permission    N/A                      
                           orldPermissionProd                                                             
...                    
---------------------------------------------------------------------------------------------------------

Changeset created successfully. arn:aws:cloudformation:us-west-2:513423067560:changeSet/samcli-deploy1681427201/f0ef1563-5ab6-4b07-9361-864ca3de6ad6


Previewing CloudFormation changeset before deployment
======================================================
Deploy this changeset? [y/N]: y

2023-04-13 13:07:17 - Waiting for stack create/update to complete

CloudFormation events from stack operations (refresh every 5.0 seconds)
---------------------------------------------------------------------------------------------------------
ResourceStatus             ResourceType               LogicalResourceId          ResourceStatusReason     
---------------------------------------------------------------------------------------------------------
CREATE_IN_PROGRESS         AWS::IAM::Role             HelloWorldFunctionRole     -                        
CREATE_IN_PROGRESS         AWS::IAM::Role             HelloWorldFunctionRole     Resource creation        
...
---------------------------------------------------------------------------------------------------------

CloudFormation outputs from deployed stack
---------------------------------------------------------------------------------------------------------
Outputs                                                                                                 
---------------------------------------------------------------------------------------------------------
Key                 HelloWorldFunctionIamRole                                                           
Description         Implicit IAM Role created for Hello World function                                  
Value               arn:aws:iam::513423067560:role/hello-rust-HelloWorldFunctionRole-10II2P13AUDUY      

Key                 HelloWorldApi                                                                       
Description         API Gateway endpoint URL for Prod stage for Hello World function                    
Value               https://ggdxec9le9.execute-api.us-west-2.amazonaws.com/Prod/hello/                  

Key                 HelloWorldFunction                                                                  
Description         Hello World Lambda Function ARN                                                     
Value               arn:aws:lambda:us-west-2:513423067560:function:hello-rust-HelloWorldFunction-       
yk4HzGzYeZBj                                                                                            
---------------------------------------------------------------------------------------------------------


Successfully created/updated stack - hello-rust in us-west-2
```

To test, we can invoke our Lambda function using the API endpoint\.

```
$ curl https://ggdxec9le9.execute-api.us-west-2.amazonaws.com/Prod/hello/
Hello World!%
```

To test our function locally, first we ensure our function’s `Architectures` property matches our local machine\.

```
...
Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function # More info about Function Resource: https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessfunction
    Metadata:
      BuildMethod: rust-cargolambda # More info about Cargo Lambda: https://github.com/cargo-lambda/cargo-lambda
    Properties:
      CodeUri: ./rust_app   # Points to dir of Cargo.toml
      Handler: bootstrap    # Do not change, as this is the default executable name produced by Cargo Lambda
      Runtime: provided.al2
      Architectures:
        - arm64
...
```

Since we modified our architecture from `x86_64` to `arm64` in this example, we run `sam build` to update our build artifacts\. We then run `sam local invoke` to locally invoke our function\.

```
hello-rust$ sam local invoke
Invoking bootstrap (provided.al2)
Local image was not found.
Removing rapid images for repo public.ecr.aws/sam/emulation-provided.al2
Building image.....................................................................................................................................
Using local image: public.ecr.aws/lambda/provided:al2-rapid-arm64.

Mounting /Users/.../hello-rust/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated, inside runtime container
START RequestId: fbc55e6e-0068-45f9-9f01-8e2276597fc6 Version: $LATEST
{"statusCode":200,"body":"Hello World!"}END RequestId: fbc55e6e-0068-45f9-9f01-8e2276597fc6
REPORT RequestId: fbc55e6e-0068-45f9-9f01-8e2276597fc6  Init Duration: 0.68 ms  Duration: 130.63 ms     Billed Duration: 131 ms     Memory Size: 128 MB     Max Memory Used: 128 MB
```

### Single Lambda function project<a name="building-rust-examples-single"></a>

**Here is an example of a serverless application containing one Rust Lambda function\. **

Project directory structure:

```
.
├── Cargo.lock
├── Cargo.toml
├── src
│   └── main.rs
└── template.yaml
```

AWS SAM template:

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Metadata:
      BuildMethod: rust-cargolambda
    Properties:
      CodeUri: ./             
      Handler: bootstrap
      Runtime: provided.al2
...
```

### Multiple Lambda function project<a name="building-rust-examples-multiple"></a>

**Here is an example of a serverless application containing multiple Rust Lambda functions\.**

Project directory structure:

```
.
├── Cargo.lock
├── Cargo.toml
├── src
│   ├── function_a.rs
│   └── function_b.rs
└── template.yaml
```

AWS SAM template:

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  FunctionA:
    Type: AWS::Serverless::Function
    Metadata:
      BuildMethod: rust-cargolambda
      BuildProperties:
        Binary: function_a 
    Properties:
      CodeUri: ./           
      Handler: bootstrap     
      Runtime: provided.al2
  FunctionB:
    Type: AWS::Serverless::Function
    Metadata:
      BuildMethod: rust-cargolambda
      BuildProperties:
        Binary: function_b
    Properties:
      CodeUri: ./
      Handler: bootstrap
      Runtime: provided.al2
```

`Cargo.toml` file:

```
[package]
name = "test-handler"
version = "0.1.0"
edition = "2021"

[dependencies]
lambda_runtime = "0.6.0"
serde = "1.0.136"
tokio = { version = "1", features = ["macros"] }
tracing = { version = "0.1", features = ["log"] }
tracing-subscriber = { version = "0.3", default-features = false, features = ["fmt"] }

[[bin]]
name = "function_a"
path = "src/function_a.rs"

[[bin]]
name = "function_b"
path = "src/function_b.rs"
```