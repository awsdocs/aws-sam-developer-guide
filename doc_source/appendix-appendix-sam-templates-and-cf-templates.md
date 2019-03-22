# Declaring AWS CloudFormation Resources<a name="appendix-appendix-sam-templates-and-cf-templates"></a>

AWS SAM is a higher\-level abstraction of AWS CloudFormation that simplifies serverless application development\. AWS SAM template files are AWS CloudFormation template files with a few additional resource types defined that are specific to serverless applications—such as API Gateway endpoints and Lambda functions\. This means that AWS SAM supports the full suite of resources, intrinsic functions, and other template features that are available in AWS CloudFormation\.

For example, the following AWS SAM template creates a Lambda function by using AWS SAM resource syntax\. It also creates an Amazon S3 bucket by using AWS CloudFormation resource syntax:

```
Transform: 'AWS::Serverless-2016-10-31'
Resources:

  MyFunction:
    # SAM resource to create a Lambda function
    Type: 'AWS::Serverless::Function'
    
    Properties:
      Runtime: nodejs6.10
      .... 
    
  MyBucket:
    # AWS CloudFormation resource to create an S3 bucket
    Type: 'AWS::S3::Bucket'
```

For an introduction to AWS CloudFormation templates, see [Learn Template Basics](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/gettingstarted.templatebasics.html)\.

For more information about working with AWS CloudFormation templates, see [Working with AWS CloudFormation Templates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-guide.html)\. 

For the full reference for AWS CloudFormation templates, see the [AWS CloudFormation Template Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html)\.