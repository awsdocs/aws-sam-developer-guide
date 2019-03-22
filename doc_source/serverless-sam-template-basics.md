# AWS SAM Template Concepts<a name="serverless-sam-template-basics"></a>

When you create a serverless application by using AWS SAM, your main objective is to construct an AWS SAM template file that represents the architecture of your serverless application\.

The AWS SAM template file is a YAML or JSON configuration file that adheres to the open source [AWS Serverless Application Model specification](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md)\. You use the template to declare all of the AWS resources that comprise your serverless application\.

AWS SAM templates are an extension of AWS CloudFormation templates\. That is, any resource that you can declare in an AWS CloudFormation template you can also declare in an AWS SAM template\. In addition, you can use the additional resource types provided by AWS SAM—for instance, the resources described in [Declaring Serverless Resources](serverless-sam-template.md)—as shortcuts for some components of your serverless application\.

For an introduction to AWS CloudFormation templates, see [Learn Template Basics](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/gettingstarted.templatebasics.html)\.

For information about the AWS SAM template specification, see [AWS Serverless Application Model Specification](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md)\.

The following sections describe the types of AWS resources that can be declared in AWS SAM template files\.

**Topics**
+ [Declaring Serverless Resources](serverless-sam-template.md)
+ [Declaring AWS CloudFormation Resources](appendix-appendix-sam-templates-and-cf-templates.md)
+ [Nested Applications](serverless-sam-template-nested-applications.md)
+ [Controlling Access to API Gateway APIs](serverless-controlling-access-to-apis.md)

**Example**

The following example AWS SAM template describes the configuration of a Lambda function and an API Gateway endpoint\.

```
Transform: 'AWS::Serverless-2016-10-31'
Resources:

  ThumbnailFunction:
    # This resource creates a Lambda function.
    Type: 'AWS::Serverless::Function'
    
    Properties:
      
      # This function uses the Nodejs v6.10 runtime.
      Runtime: nodejs6.10
        
      # This is the Lambda function's handler.
      Handler: index.handler
      
      # The location of the Lambda function code.
      CodeUri: ./src
      
      # Event sources to attach to this function. In this case, we are attaching
      # one API Gateway endpoint to the Lambda function. The function is
      # called when a HTTP request is made to the API Gateway endpoint.
      Events:

        ThumbnailApi:
            # Define an API Gateway endpoint that responds to HTTP GET at /thumbnail
            Type: Api
            Properties:
                Path: /thumbnail
                Method: GET
```