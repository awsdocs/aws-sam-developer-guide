# Step\-through debugging Lambda functions locally<a name="serverless-sam-cli-using-debugging"></a>

You can use AWS SAM with a number of AWS toolkits to test and debug your serverless applications locally\.

For example, you can perform step\-through debugging of your Lambda functions\. Step\-through debugging makes it easier to understand what the code is doing\. It tightens the feedback loop by making it possible for you to find and troubleshoot issues that you might run into in the cloud\.

## Using AWS Toolkits<a name="serverless-sam-cli-using-aws-toolkits"></a>

AWS toolkits are plugins that provide you with the ability to perform many common debugging tasks, like setting breakpoints, executing code line by line, and inspecting the values of variables\. Toolkits make it easier for you to develop, debug, and deploy serverless applications that are built using AWS\. They provide an experience for building, testing, debugging, deploying, and invoking Lambda functions that's integrated into the integrated development environment \(IDE\)\. 

For more information about AWS toolkits that you can use with AWS SAM, see the following:
+ [AWS Toolkit for JetBrains](https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/)
+ [AWS Toolkit for PyCharm](https://aws.amazon.com/pycharm/)
+ [AWS Toolkit for IntelliJ](https://aws.amazon.com/intellij/)
+ [AWS Toolkit for Visual Studio Code](https://aws.amazon.com/visualstudiocode/)

## Running AWS SAM locally<a name="serverless-sam-cli-running-locally"></a>

The commands `sam local invoke` and `sam local start-api` both support local step\-through debugging of your Lambda functions\. To run AWS SAM locally with step\-through debugging support enabled, specify `--debug-port` or `-d` on the command line\. For example:

```
# Invoke a function locally in debug mode on port 5858
sam local invoke -d 5858 <function logical id>

# Start local API Gateway in debug mode on port 5858
sam local start-api -d 5858
```

**Note**  
If you're using `sam local start-api`, the local API Gateway instance exposes all of your Lambda functions\. However, because you can specify a single debug port, you can only debug one function at a time\. You need to call your API before the AWS SAM CLI binds to the port, which allows the debugger to connect\.

**Topics**

The following topics provide examples of how to set up your environment to test and debug your serverless applications locally\.
+ [Step\-through debugging Node\.js functions locally](serverless-sam-cli-using-debugging-nodejs.md)
+ [Step\-through debugging Python functions locally](serverless-sam-cli-using-debugging-python.md)
+ [Step\-through debugging Golang functions locally](serverless-sam-cli-using-debugging-golang.md)