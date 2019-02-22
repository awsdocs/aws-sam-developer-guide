# Quick Start<a name="serverless-quick-start"></a>

This guide walks you through the steps to build an example serverless application using the AWS Serverless Application Model \(AWS SAM\)\. You can use this example application as a starting point for developing your own serverless application\. 

## Steps for Using AWS SAM<a name="how-it-works-using-aws-sam"></a>

The following steps outline how to build a serverless application using AWS SAM:

1. **Initialize**\. Download a sample application from template using `sam init`\.

1. **Test Locally**\. Test the application locally using `sam local invoke` and/or `sam local start-api`\. Note that with these commands, even though your Lambda function is invoked locally, it reads from and writes to AWS resources in the AWS Cloud\.

1. **Package**\. When you're satisfied with your Lambda function, bundle the Lambda function, AWS SAM template, and any dependencies into an AWS CloudFormation deployment package using `sam package`\.

1. **Deploy**\. Deploy the application to the AWS Cloud using `sam deploy`\. At this point, you're able to test your application in the AWS Cloud by invoking it using standard Lambda methods\.

The example [Hello World Application](#gs-ex1) in the next section walks you through these steps in building your first serverless application using AWS SAM\.

## Hello World Application<a name="gs-ex1"></a>

In this exercise, you download and test a sample Hello World serverless application\. The application represents a simple API backend\. It has an Amazon API Gateway endpoint that supports a GET operation and a Lambda function\. When a GET request is sent to the endpoint, API Gateway invokes the Lambda function\. Then, AWS Lambda executes the function\. The function returns a string that includes a `hello world` message, and the IP address that's returned by a call to the `http://checkip.amazonaws.com/` website\.

The application has the following components:
+ An AWS SAM template that defines two AWS resources for the Hello Word application: an API Gateway service with a GET operation, and a Lambda function\. The template also defines the mapping between the API Gateway GET operation and the Lambda function\. 
+ Application code that's written in Python\.

In addition, there's a `requirements.txt` file that's needed to install dependencies for this sample application\. This file is used when you're initializing the application\.

### Before You Begin<a name="gs-ex1-prereq"></a>

Make sure that you have the required setup for this exercise:
+ You must have an AWS account with an IAM user that has administrator permissions\. See [Set Up an AWS Account](https://docs.aws.amazon.com/lambda/latest/dg/setup.html)\.
+ You must have the AWS SAM CLI \(command line interface\) installed\. See [Installing the AWS SAM CLI](serverless-sam-cli-install.md)\.

### Initialize the Application<a name="gs-ex1-setup-local-app"></a>

In this section, you download the sample application, which consists of an AWS SAM template and application code\. You also download the dependencies that are required to execute the application code, and copy everything that's needed to test and package the application into the required directory structure\.

**To initialize the application**

1. Run the following command at an AWS SAM CLI command prompt\.

   ```
   sam init --runtime python3.6 
   ```

1. Review the contents of the directory that the command created \(`sam-app/`\): 
   + `template.yaml` – Defines two AWS resources that the Hello World application needs: a Lambda function and an API Gateway endpoint that supports a GET operation\. The template also defines mapping between the two resources\.
   + Content related to the Hello World application code:
     + `hello_world/` directory – Contains the application code, which returns `hello world` when you run it\.
**Note**  
For this exercise, the application code is written in Python, and you specify the runtime in the `init` command\. AWS Lambda supports additional languages for creating application code\. If you specify another supported runtime, the `init` command provides the Hello World code in the specified language\. If you choose a different runtime, you need to use different instructions in the next step to set up a directory and download dependencies\. The `init` command downloads a `ReadMe` file that provides this information\. For information about supported runtimes, see [Lambda Execution Environment and Available Libraries](https://docs.aws.amazon.com/lambda/latest/dg/current-supported-versions.html)\.

1. Follow the steps below to create a subdirectory that contains the application code and dependencies\.

   1. Switch to the directory that the `init` command created in the preceding step\.

      ```
      cd sam-app
      ```

   1. Install the dependencies by running the following `sam` command\. The dependencies for the Hello World application code are described in the `hello_world/requirements.txt` file\. 

      ```
      sam build --use-container
      ```

      Verify that the command created the `.aws-sam/build/HelloWorld/` directory and copied the dependencies to it\. 

   The `.aws-sam/build/HelloWorld/` directory now has the application code and dependencies that are needed to execute the Lambda function\.

### Test the Application Locally<a name="gs-ex1-test-locally"></a>

Now that you have the AWS SAM application on your local machine, follow the steps below to test it locally\.

**To test the application locally**

1. Start the API Gateway endpoint locally\. You must run the following command from the directory that contains the `template.yaml` file\.

   ```
   sam local start-api
   ```

   The command returns an API Gateway endpoint, which you can send requests to for local testing\.

1. Test the application\. Copy the API Gateway endpoint URL, paste it in the browser, and choose **Enter**\. An example API Gateway endpoint URL is `http://127.0.0.1:3000/hello`\.

   API Gateway locally invokes the Lambda function that the endpoint is mapped to\. The Lambda function executes in the local Docker container and returns `hello world`\. API Gateway returns a response to the browser that contains the text\. 

**Exercise: Change the message string**

After successfully testing the sample application, you can experiment with making a simple modification: change the message string that's returned\. Note that the copy of the application code being executed is in the `.aws-sam/build/HelloWorld/` directory \(not the `hello_world/` directory\)\.

1. Kill the process running `sam local start-api`\.

1. Edit the `hello_world/app.py` file to change the message string from `'hello world'` to `'Hello World!'`\.

1. Rebuild your function by running `sam build --use-container`\.

1. Restart the API Gateway endpoint locally by running `sam local start-api`\.

1. Reload the test URL in your browser and observe the new string\.

### Package the Application<a name="gs-ex1-setup-pacakge-app"></a>

After testing your application locally, you use the AWS SAM CLI to create a deployment package\. You use this package to deploy the application to the AWS Cloud\. 

**Note**  
In the following steps, you create a \.zip file for the contents of the `/build` directory\. This directory contains the application code and dependencies\. This \.zip file is the **deployment package** for your serverless application\. For more information, see [Creating a Deployment Package \(Python\)]( https://docs.aws.amazon.com/lambda/latest/dg/lambda-python-how-to-create-deployment-package.html) in the *AWS Lambda Developer Guide*\.

**To create a Lambda deployment package**

1. Create an S3 bucket in the location where you want to save the packaged code\. If you want to use an existing S3 bucket, skip this step\.

   ```
   aws s3 mb s3://bucketname
   ```

1. Create the Lambda function deployment package by running the following `package` AWS SAM CLI command at the command prompt\. 

   ```
   sam package \
       --output-template-file packaged.yaml \
       --s3-bucket bucketname
   ```

   The command does the following:
   + Zips the contents of the `.aws-sam/build/HelloWorld/` directory\. This directory was created by `sam build` and where your dependencies were installed\.
   + Outputs a new template file, called `packaged.yaml`, which you use in the next step to deploy the application to the AWS Cloud\. The `packaged.yaml` template file is similar to the original template file \(`template.yaml`\), but has one key difference—the `CodeUri` property points to the Amazon S3 bucket and object that contains the Lambda function code and dependencies\. The following snippet from an example `packaged.yaml` template file shows this property: 

     ```
     HelloWorldFunction:
         Type: AWS::Serverless::Function # For more information about function resources, see https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessfunction
         Properties:
           CodeUri: s3://bucketname/fbd77a3647a4f47a352fcObjectGUID
     
     ...
     ```

### Deploy the Application<a name="gs-ex1-setup-deploy-app"></a>

Now that you've created the deployment package, you use it to deploy the application to the AWS Cloud\. You then test the application there\.

**To deploy the serverless application to the AWS Cloud**
+ In the AWS SAM CLI, use the `deploy` command to deploy all of the resources that you defined in the template\. 

  ```
  sam deploy \
      --template-file packaged.yaml \
      --stack-name sam-app \
      --capabilities CAPABILITY_IAM \
      --region us-east-1
  ```

  In the command, the `--capabilities` parameter enables AWS CloudFormation to create an IAM role\. 

   The example uses the us\-east\-1 AWS Region to create all resources\. You can choose to specify any other Region\.

  AWS CloudFormation creates the AWS resources as defined in the template, and groups them in an entity called a *stack* in AWS CloudFormation\. You can access this stack in the console\.

**To test the serverless application in the AWS Cloud**

1. Open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/)\.

1. Choose the AWS CloudFormation stack that you created in the preceding step from the list shown\.

1. Under **Outputs**, copy the URL of the API Gateway endpoint URL\.

1. Open a browser, paste the endpoint URL, and choose **Enter**\.

   This sends a GET request to the endpoint\. API Gateway invokes the Lambda function that the endpoint is mapped to\. AWS Lambda executes the Lambda function and returns `hello world`\. API Gateway returns a response with the text to the browser\.

## Additional Example Applications<a name="getstarted-nextstep"></a>

There are two ways you can explore additional serverless applications that are built using AWS SAM:
+ Download applications from templates using the AWS SAM CLI command `sam init`\. See [Example Serverless Applications](serverless-example-applications.md) for instructions about these examples\.
+ Explore additional [AWS SAM example applications](https://github.com/awslabs/serverless-application-model/tree/master/examples/apps) in the AWS SAM GitHub repository\.