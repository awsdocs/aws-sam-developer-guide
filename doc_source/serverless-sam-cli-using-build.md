# Building applications<a name="serverless-sam-cli-using-build"></a>

To build your serverless application, use the `` command\.

`sam build` also gathers the build artifacts of your application's dependencies, and places them in the proper format and location for subsequent steps in your workflow\. You specify dependencies in a manifest file that you include in your application \(such as `requirements.txt` for Python functions, or `package.json` for Nodejs functions\), or by using the `Layers` property of a function resource\. The `Layers` property contains a list of Lambda layer resources that the function depends on\.

If your AWS Lambda function depends on packages that have natively compiled programs, use the `--use-container` flag\. The `--use-container` flag locally compiles your functions in a Docker container that functions like a Lambda environment, so they are in the right format when you deploy them to the AWS Cloud\.

## Examples<a name="building-applications-examples"></a>

The following `sam build` commands build applications\.

```
# Build all functions and layers, and their dependencies
sam build

# Run the build process inside a Docker container that functions like a Lambda environment
sam build --use-container

# Build and run your functions locally
sam build && sam local invoke

# For more options
sam build --help
```