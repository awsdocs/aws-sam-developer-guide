# Process DynamoDB events<a name="serverless-example-ddb"></a>

With this example application, you build on what you learned in the overview and the Quick Start guide, and install another example application\. This application consists of a Lambda function that's invoked by a DynamoDB table event source\. The Lambda function is very simple—it logs data that was passed in through the event source message\.

This exercise shows you how to mimic event source messages that are passed to Lambda functions when they're invoked\.

## Before you begin<a name="gs-ex2-prereq"></a>

Make sure that you've completed the required setup in the [Installing the AWS SAM CLI](serverless-sam-cli-install.md)\.

## Step 1: Initialize the application<a name="gs-ex2-setup-local-app"></a>

In this section, you download the application package, which consists of an AWS SAM template and application code\.

**To initialize the application**

1. Run the following command at an AWS SAM CLI command prompt\.

   ```
   sam init \
   --location gh:aws-samples/cookiecutter-aws-sam-dynamodb-python \
   --no-input
   ```

1. Review the contents of the directory that the command created \(`dynamodb_event_reader/`\): 
   + `template.yaml` – Defines two AWS resources that the Read DynamoDB application needs: a Lambda function and a DynamoDB table\. The template also defines mapping between the two resources\.
   + `read_dynamodb_event/` directory – Contains the DynamoDB application code\.

## Step 2: Test the application locally<a name="gs-ex2-test-locally"></a>

For local testing, use the AWS SAM CLI to generate a sample DynamoDB event and invoke the Lambda function:

```
sam local generate-event dynamodb update | sam local invoke --event - ReadDynamoDBEvent
```

The `generate-event` command creates a test event source message like the messages that are created when all components are deployed to the AWS Cloud\. This event source message is piped to the Lambda function ReadDynamoDBEvent\.

Verify that the expected messages are printed to the console, based on the source code in `app.py`\.

## Step 3: Package the application<a name="gs-ex2-setup-pacakge-app"></a>

After testing your application locally, you use the AWS SAM CLI to create a deployment package, which you use to deploy the application to the AWS Cloud\.

**To create a Lambda deployment package**

1. Create an S3 bucket in the location where you want to save the packaged code\. If you want to use an existing S3 bucket, skip this step\.

   ```
   aws s3 mb s3://bucketname
   ```

1. Create the deployment package by running the following `package` CLI command at the command prompt\. 

   ```
   sam package \
       --template-file template.yaml \
       --output-template-file packaged.yaml \
       --s3-bucket bucketname
   ```

   You specify the new template file, `packaged.yaml`, when you deploy the application in the next step\.

## Step 4: Deploy the application<a name="gs-ex2-setup-deploy-app"></a>

Now that you've created the deployment package, you use it to deploy the application to the AWS Cloud\. You then test the application\.

**To deploy the serverless application to the AWS Cloud**
+ In the AWS SAM CLI, use the `deploy` CLI command to deploy all of the resources that you defined in the template\. 

  ```
  sam deploy \
      --template-file packaged.yaml \
      --stack-name sam-app \
      --capabilities CAPABILITY_IAM \
      --region us-east-1
  ```

  In the command, the `--capabilities` parameter allows AWS CloudFormation to create an IAM role\. 

  AWS CloudFormation creates the AWS resources that are defined in the template\. You can access the names of these resources in the AWS CloudFormation console\.

**To test the serverless application in the AWS Cloud**

1. Open the DynamoDB console\.

1. Insert a record into the table that you just created\.

1. Go to the **Metrics** tab of the table, and choose **View all CloudWatch metrics**\. In the CloudWatch console, choose **Logs** to be able to view the log output\.

## Next steps<a name="gs-ex2-setup-deploy-app-next-steps"></a>

The AWS SAM GitHub repository contains additional example applications for you to download and experiement with\. To access this repository, see [AWS SAM example applications](https://github.com/aws-samples/serverless-app-examples)\.