# Building serverless applications<a name="serverless-building"></a>

Building your serverless application involves taking your AWS SAM template file, application code, and any applicable language\-specific files and dependencies, and placing all build artifacts in the proper format and location for subsquent steps in your workflow\.

For example, you might want to locally test your application, or you might want to deploy your application using the AWS SAM CLI\. Both of these activities use the build artifacts of your application as inputs\.

This section shows you how to use the `` command to build serverless applications using AWS SAM\. You have the option to build all functions and layers of your application, or individual components of your application, like a specific function or layer\.

**Topics**
+ [Building applications](serverless-sam-cli-using-build.md)
+ [Building layers](building-layers.md)
+ [Building custom runtimes](building-custom-runtimes.md)