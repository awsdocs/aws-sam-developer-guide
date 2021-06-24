# Step\-through debugging Lambda functions locally<a name="serverless-sam-cli-using-debugging"></a>

You can use AWS SAM with a variety of AWS toolkits and debuggers to test and debug your serverless applications locally\.

For example, you can perform local step\-through debugging of your Lambda functions by setting breakpoints, inspecting variables, and executing function code one line at a time\. Local step\-through debugging tightens the feedback loop by making it possible for you to find and troubleshoot issues that you might run into in the cloud\.

## Using AWS Toolkits<a name="serverless-sam-cli-using-aws-toolkits"></a>

AWS Toolkits are integrated development environment \(IDE\) plugins that provide you with the ability to perform many common debugging tasks, like setting breakpoints, inspecting variables, and executing function code one line at a time\. AWS Toolkits make it easier for you to develop, debug, and deploy serverless applications that are built using AWS SAM\. They provide an experience for building, testing, debugging, deploying, and invoking Lambda functions that's integrated into your IDE\.

For more information about AWS Toolkits that you can use with AWS SAM, see the following:
+ [AWS Toolkit for Visual Studio Code](https://docs.aws.amazon.com/toolkit-for-vscode/latest/userguide/)
+ [AWS Cloud9](https://docs.aws.amazon.com/cloud9/latest/user-guide/)
+ [AWS Toolkit for JetBrains](https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/)

There are a variety AWS Toolkits that work with different combinations of IDEs and runtimes\. The following table lists common IDE/runtime combinations that support step\-through debugging of AWS SAM applications:


| IDE | Runtime | AWS Toolkit | Instructions for step\-through debugging | 
| --- | --- | --- | --- | 
| Visual Studio Code |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-using-debugging.html)  | AWS Toolkit for Visual Studio Code | [Working with AWS Serverless Application](https://docs.aws.amazon.com/toolkit-for-vscode/latest/userguide/serverless-apps.html) in the AWS Toolkit for Visual Studio Code User Guide  | 
| AWS Cloud9 |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-using-debugging.html)  | AWS Cloud9, with AWS Toolkit enabled1 |  [Working with AWS serverless applications using the AWS Toolkit](https://docs.aws.amazon.com/cloud9/latest/user-guide/serverless-apps-toolkit.html) in the *AWS Cloud9 User Guide*\.  | 
| WebStorm | Node\.js | AWS Toolkit for JetBrains2 |  [Running \(invoking\) or debugging a local function](https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/invoke-lambda.html) in the *AWS Toolkit for JetBrains*  | 
| PyCharm | Python | AWS Toolkit for JetBrains2 |  [Running \(invoking\) or debugging a local function](https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/invoke-lambda.html) in the *AWS Toolkit for JetBrains*  | 
| Rider | \.NET | AWS Toolkit for JetBrains2 |  [Running \(invoking\) or debugging a local function](https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/invoke-lambda.html) in the *AWS Toolkit for JetBrains*  | 
| IntelliJ | Java | AWS Toolkit for JetBrains2 |  [Running \(invoking\) or debugging a local function](https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/invoke-lambda.html) in the *AWS Toolkit for JetBrains*  | 
| GoLand | Go | AWS Toolkit for JetBrains2 |  [Running \(invoking\) or debugging a local function](https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/invoke-lambda.html) in the *AWS Toolkit for JetBrains*  | 

**Notes:**

1. To use AWS Cloud9 to step\-through debug AWS SAM applications, the AWS Toolkit must be enabled\. For more information, see [Enabling the AWS Toolkit](https://docs.aws.amazon.com/cloud9/latest/user-guide/toolkit-welcome.html#access-toolkit) in the *AWS Cloud9 User Guide*\.

1. To use the AWS Toolkit for JetBrains to step\-through debug AWS SAM applications, you must first install and configure it by following the instructions found in [Installing the AWS Toolkit for JetBrains](https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/setup-toolkit.html) in the *AWS Toolkit for JetBrains*\.

## Running AWS SAM locally in debug mode<a name="serverless-sam-cli-running-locally"></a>

In addition to integrating with AWS Toolkits, you can also run AWS SAM in "debug mode" to attach to third\-party debuggers like [ptvsd](https://pypi.org/project/ptvsd/) or [delve](https://github.com/go-delve/delve)\.

To run AWS SAM in debug mode, use commands [sam local invoke](sam-cli-command-reference-sam-local-invoke.md) or [sam local start\-api](sam-cli-command-reference-sam-local-start-api.md) with the `--debug-port` or `-d` option\.

For example:

```
# Invoke a function locally in debug mode on port 5858
sam local invoke -d 5858 <function logical id>

# Start local API Gateway in debug mode on port 5858
sam local start-api -d 5858
```

**Note**  
If you're using `sam local start-api`, the local API Gateway instance exposes all of your Lambda functions\. However, because you can specify a single debug port, you can only debug one function at a time\. You need to call your API before the AWS SAM CLI binds to the port, which allows the debugger to connect\.