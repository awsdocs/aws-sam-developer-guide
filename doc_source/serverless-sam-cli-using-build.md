# Building Applications with Dependencies<a name="serverless-sam-cli-using-build"></a>

You can use the `[sam build](sam-cli-command-reference-sam-build.md)` command to compile dependencies for Lambda functions written in Python\. For example, if you write code that uses Python packages, such as a graphics library for image processing, you need to create a deployment package that works on the Amazon Linux AMI\. The `sam build` command allows you to easily create deployment artifacts that target Lambda's execution environment, so that the functions you build locally run in a similar environment in the AWS Cloud\.

The `sam build` command iterates through the functions in your application, looks for a manifest file \(such as `requirements.txt`\) that contain the dependencies, and automatically creates deployment artifacts that you can deploy to Lambda using the `sam package` and `sam deploy` commands\.

If your Lambda function depends on packages that have natively compiled programs, you can use the `--use-container` flag\. The `--use-container` flag compiles your functions in a Lambda\-like environment locally, so they are in the right format when you deploy them to the AWS Cloud\.

Examples:

```
# Build a deployment package
sam build

# Run the build process inside an AWS Lambda-like Docker container
sam build --use-container

# Build and run your functions locally
sam build && sam local invoke
  
# Build and package for deployment
sam build && sam package --s3-bucket <bucketname>

# For more options
sam build --help
```