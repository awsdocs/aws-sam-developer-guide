# Managing permissions with AWS CloudFormation mechanisms<a name="sam-permissions-cloudformation"></a>

To control access to AWS resources, the AWS Serverless Application Model \(AWS SAM\) can use the same mechanisms as AWS CloudFormation\. For more information, see [Controlling access with AWS Identity and Access Management](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-iam-template.html) in the *AWS CloudFormation User Guide*\.

There are three main options for granting a user permission to manage serverless applications\. Each option provides users with different levels of access control\.
+ Grant administrator permissions\.
+ Attach necessary AWS managed policies\.
+ Grant specific AWS Identity and Access Management \(IAM\) permissions\.

Depending on which option you choose, users can manage only serverless applications containing AWS resources that they have permission to access\.

The following sections describe each option in more detail\.

## Grant administrator permissions<a name="sam-permissions-cloudformation-admin"></a>

If you grant administrator permissions to a user, they can manage serverless applications that contain any combination of AWS resources\. This is the simplest option, but it also grants users the broadest set of permissions, which therefore enables them to perform actions with the highest impact\.

For more information about granting administrator permissions to a user, see [Creating your first IAM admin user and group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

## Attach necessary AWS managed policies<a name="sam-permissions-cloudformation-managed-policies"></a>

You can grant users a subset of permissions using [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies), rather than granting full administrator permissions\. If you use this option, make sure that the set of AWS managed policies covers all of the actions and resources required for the serverless applications that the users manage\.

For example, the following AWS managed policies are sufficient to [deploy the sample Hello World application](serverless-getting-started-hello-world.md):
+ AWSCloudFormationFullAccess
+ IAMFullAccess
+ AWSLambda\_FullAccess
+ AmazonAPIGatewayAdministrator
+ AmazonS3FullAccess
+ AmazonEC2ContainerRegistryFullAccess

 For information about attaching policies to an IAM user, see [Changing permissions for an IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_change-permissions.html) in the *IAM User Guide*\.

## Grant specific IAM permissions<a name="sam-permissions-cloudformation-policy-statement"></a>

For the most granular level of access control, you can grant specific IAM permissions to users using [policy statements](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_statement.html)\. If you use this option, make sure that the policy statement includes all of the actions and resources required for the serverless applications that the users manage\.

The best practice with this option is to deny users the permission to create roles, including Lambda execution roles, so they can't grant themselves escalated permissions\. So, you as the administrator must first create a [Lambda execution role](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html) that will be specified in the serverless applications that users will manage\. For information about creating Lambda execution roles, see [Creating an execution role in the IAM console](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html#permissions-executionrole-console)\.

For the [sample Hello World application](serverless-getting-started-hello-world.md) the **AWSLambdaBasicExecutionRole** is sufficient to run the application\. After you've created a Lambda execution role, modify the AWS SAM template file of the sample Hello World application to add the following property to the `AWS::Serverless::Function` resource:

```
  Role: lambda-execution-role-arn
```

With the modified Hello World application in place, the following policy statement grants sufficient permissions for users to deploy, update, and delete the application:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "CloudFormationTemplate",
            "Effect": "Allow",
            "Action": [
                "cloudformation:CreateChangeSet"
            ],
            "Resource": [
                "arn:aws:cloudformation:*:aws:transform/Serverless-2016-10-31"
            ]
        },
        {
            "Sid": "CloudFormationStack",
            "Effect": "Allow",
            "Action": [
                "cloudformation:CreateChangeSet",
                "cloudformation:CreateStack",
                "cloudformation:DeleteStack",
                "cloudformation:DescribeChangeSet",
                "cloudformation:DescribeStackEvents",
                "cloudformation:DescribeStacks",
                "cloudformation:ExecuteChangeSet",
                "cloudformation:GetTemplateSummary",
                "cloudformation:ListStackResources",
                "cloudformation:UpdateStack"
            ],
            "Resource": [
                "arn:aws:cloudformation:*:111122223333:stack/*"
            ]
        },
        {
            "Sid": "S3",
            "Effect": "Allow",
            "Action": [
                "s3:CreateBucket",
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource": [
                "arn:aws:s3:::*/*"
            ]
        },
        {
            "Sid": "ECRRepository",
            "Effect": "Allow",
            "Action": [
                "ecr:BatchCheckLayerAvailability",
                "ecr:BatchGetImage",
                "ecr:CompleteLayerUpload",
                "ecr:CreateRepository",
                "ecr:DeleteRepository",
                "ecr:DescribeImages",
                "ecr:DescribeRepositories",
                "ecr:GetDownloadUrlForLayer",
                "ecr:GetRepositoryPolicy",
                "ecr:InitiateLayerUpload",
                "ecr:ListImages",
                "ecr:PutImage",
                "ecr:SetRepositoryPolicy",
                "ecr:UploadLayerPart"
            ],
            "Resource": [
                "arn:aws:ecr:*:111122223333:repository/*"
            ]
        },
        {
            "Sid": "ECRAuthToken",
            "Effect": "Allow",
            "Action": [
                "ecr:GetAuthorizationToken"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Sid": "Lambda",
            "Effect": "Allow",
            "Action": [
                "lambda:AddPermission",
                "lambda:CreateFunction",
                "lambda:DeleteFunction",
                "lambda:GetFunction",
                "lambda:GetFunctionConfiguration",
                "lambda:ListTags",
                "lambda:RemovePermission",
                "lambda:TagResource",
                "lambda:UntagResource",
                "lambda:UpdateFunctionCode",
                "lambda:UpdateFunctionConfiguration"
            ],
            "Resource": [
                "arn:aws:lambda:*:111122223333:function:*"
            ]
        },
        {
            "Sid": "IAM",
            "Effect": "Allow",
            "Action": [
                "iam:CreateRole",
                "iam:AttachRolePolicy",
                "iam:DeleteRole",
                "iam:DetachRolePolicy",
                "iam:GetRole",
                "iam:TagRole"
            ],
            "Resource": [
                "arn:aws:iam::111122223333:role/*"
            ]
        },
        {
            "Sid": "IAMPassRole",
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "iam:PassedToService": "lambda.amazonaws.com"
                }
            }
        },
        {
            "Sid": "APIGateway",
            "Effect": "Allow",
            "Action": [
                "apigateway:DELETE",
                "apigateway:GET",
                "apigateway:PATCH",
                "apigateway:POST",
                "apigateway:PUT"
            ],
            "Resource": [
                "arn:aws:apigateway:*::*"
            ]
        }
    ]
}
```

**Note**  
The example policy statement in this section grants sufficient permission for you to deploy, update, and delete the the [sample Hello World application](serverless-getting-started-hello-world.md)\. If you add additional resource types to your application, you need to update the policy statement to include the following:  
Permission for your application to call the service's actions\.
The service principal, if needed for the service's actions\.
For example, if you add a Step Functions workflow, you may need to add permissions for actions listed [here](https://docs.aws.amazon.com/service-authorization/latest/reference/list_awsstepfunctions.html#awsstepfunctions-actions-as-permissions), and the `states.amazonaws.com` service principal\.

For more information about IAM policies, see [Managing IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage.html) in the *IAM User Guide*\.