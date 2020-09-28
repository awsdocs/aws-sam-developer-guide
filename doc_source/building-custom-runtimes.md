# Building custom runtimes<a name="building-custom-runtimes"></a>

You can use the `` command to build custom runtimes required for your Lambda function\. You declare your Lambda function to use a custom runtime by specifying `Runtime: provided` for the function\.

To build a custom runtime, declare the `Metadata` resource attribute with a `BuildMethod: makefile` entry\. You provide a custom makefile, where you declare a build target of the form `build-function-logical-id` that contains the build commands for your runtime\. Your makefile is responsible for compiling the custom runtime if necessary, and copying the build artifacts into the proper location required for subsequent steps in your workflow\.

## Examples<a name="building-custom-runtimes-examples"></a>

### Example 1: Custom runtime for a function written in Rust<a name="building-custom-runtimes-examples-rust"></a>

The following AWS SAM template declares a function that uses a custom runtime for a Lambda function written in Rust, and instructs `sam build` to execute the commands for the `build-HelloRustFunction` build target\.

```
Resources:
  HelloRustFunction:
    Type: AWS::Serverless::Function
    Properties:
      FunctionName: HelloRust
      Handler: bootstrap.is.real.handler
      Runtime: provided
      MemorySize: 512
      CodeUri: .
    Metadata:
      BuildMethod: makefile
```

The following `makefile` contains the build target and commands that will be executed\.

```
build-HelloRustFunction:
  cargo build --release --target x86_64-unknown-linux-musl
  cp ./target/x86_64-unknown-linux-musl/release/bootstrap $(ARTIFACTS_DIR)
```

For more information about setting up your development environment in order to execute the `cargo build` command in the previous `makefile`, see the [Rust Runtime for AWS Lambda](https://aws.amazon.com/blogs/opensource/rust-runtime-for-aws-lambda/) blog post\.

### Example 2: Makefile builder for Python3\.7 \(alternative to using the bundled builder\)<a name="building-custom-runtimes-examples-python"></a>

You might want to use a library or module that is not included in a bundled builder\. This example shows a AWS SAM template for a Python3\.7 runtime with a makefile builder\.

```
Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: hello_world/
      Handler: app.lambda_handler
      Runtime: python3.7
    Metadata:
      BuildMethod: makefile
```

The following `makefile` contains the build target and commands that will be executed\.

```
build-HelloWorldFunction:
    cp *.py $(ARTIFACTS_DIR)
    cp requirements.txt $(ARTIFACTS_DIR)
    python -m pip install -r requirements.txt -t $(ARTIFACTS_DIR)
    rm -rf $(ARTIFACTS_DIR)/bin
```