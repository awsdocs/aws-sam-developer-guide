# Testing and Debugging Serverless Applications<a name="serverless-test-and-debug"></a>

With the AWS SAM command line interface \(CLI\), you can locally test and "step\-through" debug your serverless applications before uploading your application to the AWS Cloud\. You can verify whether your application is behaving as expected, debug what's wrong, and fix any issues, before going through the steps of packaging and deploying your application\.

When you locally invoke a Lambda function in debug mode within the AWS SAM CLI, you can then attach a debugger to it\. With the debugger, you can step through your code line by line, see the values of various variables, and fix issues the same way you would for any other application\.

**Topics**
+ [Invoking Functions Locally](serverless-sam-cli-using-invoke.md)
+ [Running API Gateway Locally](serverless-sam-cli-using-start-api.md)
+ [Integrating with Automated Tests](serverless-sam-cli-using-automated-tests.md)
+ [Generating Sample Event Payloads](serverless-sam-cli-using-generate-event.md)
+ [Step\-Through Debugging Lambda Functions Locally](serverless-sam-cli-using-debugging.md)
+ [Passing Additional Runtime Debug Arguments](serverless-sam-cli-using-debugging-additional-arguments.md)