# Nested Applications<a name="serverless-sam-template-nested-applications"></a>

A serverless application can include one or more **nested applications**\. A nested application can be deployed as a stand\-alone artifact or as a component of a larger application\. As serverless architectures grow, common patterns emerge in which the same components are defined in multiple application templates\. You can now separate out common patterns as dedicated applications, and then nest them as part of new or existing application templates\. With nested applications, you can remain even more focused on just the business logic of your application\.

To include a nested application in your serverless application, use the [AWS::Serverless::Application](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-template.html#serverless-sam-template-application) resource type\. The maximum number of applications that can be nested is 200\.

## Nested applications in the AWS Serverless Application Repository<a name="serverless-sam-template-nested-applications-in-serverlessrepo"></a>

The AWS Serverless Application Repository supports applications that contain nested applications\. You can review the details of nested applications in the AWS Serverless Application Repository using the AWS SDK, the AWS API, and the Lambda console\.

 When users deploy your application containing nested applications, they must acknowledge they understand that nested applications are included\. For more information about acknowleding nested applications, see [Acknowledging IAM Roles, Resource Policies, and Nested Applications when Deploying Applications](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/acknowledging-application-capabilities.html) in the *AWS Serverless Application Repository Developer Guide*\.

## Creating a Nested Application Section for a AWS SAM Template<a name="serverless-sam-template-nested-applications-how-to"></a>

To nest an application into your serverless application's AWS SAM template, you need to obtain the following elements of the nested application:
+ ARN
+ Semantic Version
+ Parameters

To obtain these elements, follow these steps:

1. Make sure you logged in to the AWS Management Console\.

1. Find the application you want to nest in the AWS Serverless Application Repository by using the steps found in the [Browsing, Searching, and Deploying Applications](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/serverless-app-consuming-applications.html#browse-and-search-applications                             ) section of the *AWS Serverless Application Repository Developer Guide*\.

1. When viewing the application's Detail Page in the AWS Serverless Application Repository the ARN is in the browser's URL after `applicationId=` \(starting with `arn:`\)

1. Use the AWS Serverless Application Repository [GetApplication](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/applications-applicationid.html) API or [ `aws serverlessrepo get-application`](https://docs.aws.amazon.com/cli/latest/reference/serverlessrepo/get-application.html) AWS CLI command to get the application’s parameters, and the semantic version you want to use\. Using this information, construct the AWS SAM template section as follows to nest the application:

   ```
   application-alias-name:
     Type: AWS::Serverless::Application
     Properties:
       Location:
         ApplicationId: ARN
         SemanticVersion: semantic-version
       Parameters:
         parameter-name-1: value
         parameter-name-2: value
   ```

   If there are no settings, you can omit the `Parameters:` section altogether\.

   The maximum number of parameters a nested application can have is 60\.