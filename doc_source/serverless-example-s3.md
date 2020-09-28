# Process Amazon S3 events<a name="serverless-example-s3"></a>

With this example application, you build on what you learned in the previous examples, and install a more complex application\. This application consists of a Lambda function that's invoked by an Amazon S3 object upload event source\. This exercise shows you how to access AWS resources and make AWS service calls through a Lambda function\.

This sample serverless application processes object\-creation events in Amazon S3\. For each image that's uploaded to a bucket, Amazon S3 detects the object\-created event and invokes a Lambda function\. The Lambda function invokes Amazon Rekognition to detect text that's in the image\. It then stores the results returned by Amazon Rekognition in a DynamoDB table\.

**Note**  
With this example application, you perform steps in a slightly different order than in previous examples\. The reason for this is that this example requires that AWS resources are created and IAM permissions are configured *before* you can test the Lambda function locally\. We're going to leverage AWS CloudFormation to create the resources and configure the permissions for you\. Otherwise, you would need to do this manually before you can test the Lambda function locally\.  
Because this example is more complicated, be sure that you're familiar with installing the previous example applications before executing this one\.

## Before you begin<a name="serverless-example-s3-prereq"></a>

Make sure that you've completed the required setup in the [Installing the AWS SAM CLI](serverless-sam-cli-install.md)\.

## Step 1: Initialize the application<a name="serverless-example-s3-setup-local-app"></a>

In this section, you download the sample application, which consists of an AWS SAM template and application code\.

**To initialize the application**

1. Run the following command at an AWS SAM CLI command prompt\.

   ```
   sam init \
   --location https://github.com/aws-samples/cookiecutter-aws-sam-s3-rekognition-dynamodb-python \
   --no-input
   ```

1. Review the contents of the directory that the command created \(`aws_sam_ocr/`\): 
   + `template.yaml` – Defines three AWS resources that the Amazon S3 application needs: a Lambda function, an Amazon S3 bucket, and a DynamoDB table\. The template also defines the mappings and permissions between these resources\.
   + `src/` directory – Contains the Amazon S3 application code\.
   + `SampleEvent.json` – The sample event source, which is used for local testing\.

## Step 2: Package the application<a name="serverless-example-s3-package-serverless-app"></a>

Before you can test this application locally, you must use the AWS SAM CLI to create a deployment package, which you use to deploy the application to the AWS Cloud\. This deployment creates the necessary AWS resources and permissions that are required to test the application locally\.

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

## Step 3: Deploy the application<a name="serverless-example-s3-deploy-serverless-app"></a>

Now that you've created the deployment package, you use it to deploy the application to the AWS Cloud\. You then test the application by invoking it in the AWS Cloud\.

**To deploy the serverless application to the AWS Cloud**
+ In the AWS SAM CLI, use the `deploy` command to deploy all of the resources that you defined in the template\. 

  ```
  sam deploy \
      --template-file packaged.yaml \
      --stack-name aws-sam-ocr \
      --capabilities CAPABILITY_IAM \
      --region us-east-1
  ```

  In the command, the `--capabilities` parameter allows AWS CloudFormation to create an IAM role\. 

  AWS CloudFormation creates the AWS resources that are defined in the template\. You can access the names of these resources in the AWS CloudFormation console\.

**To test the serverless application in the AWS Cloud**

1. Upload an image to the Amazon S3 bucket that you created for this sample application\.

1. Open the DynamoDB console and find the table that was created\. See the table for results returned by Amazon Rekognition\.

1. Verify that the DynamoDB table contains new records that contain text that Amazon Rekognition found in the uploaded image\.

## Step 4: Test the application locally<a name="serverless-example-s3-test-locally"></a>

Before you can test the application locally, you must first retrieve the names of the AWS resources that were created by AWS CloudFormation\.
+ Retrieve the Amazon S3 key name and bucket name from AWS CloudFormation\. Modify the `SampleEvent.json` file by replacing the values for the object key, bucket name, and bucket ARN\.
+ Retrieve the DynamoDB table name\. This name is used for the following `sam local invoke` command\.

Use the AWS SAM CLI to generate a sample Amazon S3 event and invoke the Lambda function:

```
TABLE_NAME=Table name obtained from AWS CloudFormation console sam local invoke --event SampleEvent.json
```

The `TABLE_NAME=` portion sets the DynamoDB table name\. The `--event` parameter specifies the file that contains the test event message to pass to the Lambda function\.

You can now verify that the expected DynamoDB records were created, based on the results returned by Amazon Rekognition\.

## Next steps<a name="serverless-example-s3-next-steps"></a>

The AWS SAM GitHub repository contains additional example applications for you to download and experiement with\. To access this repository, see [AWS SAM example applications](https://github.com/aws-samples/serverless-app-examples)\.