# Testing and debugging serverless applications<a name="serverless-test-and-debug"></a>

With the AWS SAM command line interface \(CLI\), you can locally test and "step\-through" debug your serverless applications before uploading your application to the AWS Cloud\. You can verify whether your application is behaving as expected, debug what's wrong, and fix any issues, before going through the steps of packaging and deploying your application\.

When you locally invoke a Lambda function in debug mode within the AWS SAM CLI, you can then attach a debugger to it\. With the debugger, you can step through your code line by line, see the values of various variables, and fix issues the same way you would for any other application\.

**Topics**
+ [Invoking Functions Locally](serverless-sam-cli-using-invoke.md)
+ [Running API Gateway locally](serverless-sam-cli-using-start-api.md)
+ [Integrating with automated tests](serverless-sam-cli-using-automated-tests.md)
+ [Generating sample event payloads](serverless-sam-cli-using-generate-event.md)
+ [Step\-through debugging Lambda functions locally](serverless-sam-cli-using-debugging.md)
+ [Passing additional runtime debug arguments](serverless-sam-cli-using-debugging-additional-arguments.md)