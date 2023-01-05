# Using OIDC User Accounts with AWS SAM pipeline<a name="deploying-with-oidc"></a>

AWS Serverless Application Model \(AWS SAM\) supports OpenID Connect \(OIDC\) user authentication for Bitbucket, GitHub Actions, and GitLab continuous integration and continuous delivery \(CI/CD\) platforms\. With this support, you can use authorized CI/CD user accounts from any of these platforms to manage your serverless application pipelines\. Otherwise, you would need to create and manage multiple AWS Identity and Access Management \(IAM\) users to control access to AWS SAM pipelines\.

## Set up OIDC with AWS SAM pipeline<a name="deploying-with-oidc-setup"></a>

During the `sam pipeline bootstrap` configuration process, do the following to set up OIDC with your AWS SAM pipeline\.

1. When prompted to choose an identity provider, select **OIDC**\.

1. Next, select a supported OIDC provider\.

1. Enter the OIDC provider URL, beginning with **https://**\.
**Note**  
AWS SAM references this URL when it generates the `AWS::IAM::OIDCProvider` resource type\.

1. Next, follow the prompts and enter the CI/CD platform information needed to access the selected platform\. These details vary by platform and can include:
   + OIDC client ID\.
   + Code repository name or universally unique identifier \(UUID\)\.
   + Group or Organization name associated with the repository\.
   + GitHub organization that the code repository belongs to\.
   + GitHub repository name\.
   + Branch that deployments will occur from\.

1. AWS SAM displays a summary of the entered OIDC configuration\. Enter the number for a setting to edit it, or press Enter to continue\.

1. When prompted to confirm the creation of resources needed to support the entered OIDC connection, press Y to continue\.

AWS SAM generates an `AWS::IAM::OIDCProvider` AWS CloudFormation resource with the provided configuration that assumes the pipeline execution role\. To learn more about this AWS CloudFormation resource type, see [AWS::IAM::OIDCProvider](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-oidcprovider.html) in the *AWS CloudFormation User Guide*\.

**Note**  
If the identity provider \(IdP\) resource already exists in your AWS account, AWS SAM references it instead of creating a new resource\.

## Example<a name="deploying-with-oidc-setup-example"></a>

The following is an example of setting up OIDC with AWS SAM pipeline\.

```
Select a permissions provider:
    1 - IAM (default)
    2 - OpenID Connect (OIDC)
Choice (1, 2): 2
Select an OIDC provider:
    1 - GitHub Actions
    2 - GitLab
    3 - Bitbucket
Choice (1, 2, 3): 1
Enter the URL of the OIDC provider [https://token.actions.githubusercontent.com]:
Enter the OIDC client ID (sometimes called audience) [sts.amazonaws.com]:
Enter the GitHub organization that the code repository belongs to. If there is no organization enter your username instead: my-org
Enter GitHub repository name: testing
Enter the name of the branch that deployments will occur from [main]:

[3] Reference application build resources
Enter the pipeline execution role ARN if you have previously created one, or we will create one for you []:
Enter the CloudFormation execution role ARN if you have previously created one, or we will create one for you []:
Please enter the artifact bucket ARN for your Lambda function. If you do not have a bucket, we will create one for you []:
Does your application contain any IMAGE type Lambda functions? [y/N]:

[4] Summary
Below is the summary of the answers:
    1 - Account: 123456
    2 - Stage configuration name: dev
    3 - Region: us-east-1
    4 - OIDC identity provider URL: https://token.actions.githubusercontent.com
    5 - OIDC client ID: sts.amazonaws.com
    6 - GitHub organization: my-org
    7 - GitHub repository: testing
    8 - Deployment branch: main
    9 - Pipeline execution role: [to be created]
    10 - CloudFormation execution role: [to be created]
    11 - Artifacts bucket: [to be created]
    12 - ECR image repository: [skipped]
Press enter to confirm the values above, or select an item to edit the value:

This will create the following required resources for the 'dev' configuration:
    - IAM OIDC Identity Provider
    - Pipeline execution role
    - CloudFormation execution role
    - Artifact bucket
Should we proceed with the creation? [y/N]:
```

## Learn more<a name="deploying-with-oidc-setup-learn-more"></a>

For more information on using OIDC with AWS SAM pipeline, see [sam pipeline bootstrap](sam-cli-command-reference-sam-pipeline-bootstrap.md)\.