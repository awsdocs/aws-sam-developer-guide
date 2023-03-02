# Building Rust Lambda functions with Cargo Lambda<a name="building-rust"></a>


|  | 
| --- |
| This feature is in preview release for AWS SAM and is subject to change\. | 

Use the AWS SAM command line interface \(AWS SAM CLI\) with your Rust AWS Lambda functions\.

**Topics**
+ [Prerequisites](#building-rust-prerequisites)
+ [Configuring AWS SAM to use with Rust Lambda functions](#building-rust-configure)
+ [Examples](#building-rust-examples)

## Prerequisites<a name="building-rust-prerequisites"></a>

### Cargo Lambda subcommand<a name="building-rust-prerequisites-cargo"></a>

The AWS SAM CLI requires installation of Cargo Lambda, a subcommand for Cargo\.
+ To learn more about Cargo Lambda, see [What is Cargo Lambda?](https://www.cargo-lambda.info/guide/what-is-cargo-lambda.html) 
+ For Cargo Lambda installation instructions, see [Installation](https://www.cargo-lambda.info/guide/installation.html) in the *Cargo Lambda documentation*\.

### Opt in to AWS SAM CLI beta features<a name="building-rust-prerequisites-cli"></a>

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

1. Choose option `y` when the AWS SAM CLI prompts you to opt in\.

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

Use any AWS SAM CLI command with your AWS SAM template\. For more information about AWS SAM CLI commands, see [AWS SAM CLI command reference](serverless-sam-cli-command-reference.md)\.

## Examples<a name="building-rust-examples"></a>

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