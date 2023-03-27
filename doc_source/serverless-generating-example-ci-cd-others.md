# Generating starter pipelines for Jenkins, GitLab CI/CD, GitHub Actions, or Bitbucket Pipelines<a name="serverless-generating-example-ci-cd-others"></a>

To generate a starter pipeline configuration for Jenkins, GitLab CI/CD, GitHub Actions, or Bitbucket Pipelines perform the following tasks in this order:

1. Create infrastructure resources

1. Connect your Git repository with your CI/CD system

1. Create credential objects

1. Generate the pipeline configuration

1. Commit your pipeline configuration to Git repository

**Note**  
The following procedure utilizes two AWS SAM CLI commands, `sam pipeline bootstrap` and `sam pipeline init`\. The reason there are two commands is to handle the use case where administrators \(that is, users who need permission to set up infrastructure AWS resource like IAM users and roles\) have more permission that developers \(that is, users who just need permission to set up individual pipelines, but not the required infrastructure AWS resources\)\.

## Step 1: Create infrastructure resources<a name="generating-example-step-1"></a>

Pipelines that use AWS SAM require certain AWS resources, like an IAM user and roles with necessary permissions, an Amazon S3 bucket, and optionally an Amazon ECR repository\. You must have a set of infrastructure resources for each deployment stage of the pipeline\.

You can run the following command to help with this setup:

```
sam pipeline bootstrap
```

**Note**  
Run the previous command for each deployment stage of your pipeline\.

You must capture the AWS credentials \(key id and secret key\) for the pipeline users for each deployment stage of your pipeline, because they are needed for subsequent steps\.

## Step 2: Connect your Git repository with your CI/CD system<a name="generating-example-step-2"></a>

Connecting your Git repository to your CI/CD system is necessary so that the CI/CD system is able to access your application source code for builds and deployments\.

**Note**  
You can skip this step if you are using one of the following combinations, because the connection is done for you automatically:  
GitHub Actions with GitHub repository
GitLab CI/CD with GitLab repository
Bitbucket Pipelines with a Bitbucket repository

To connect your Git repository with your CI/CD system, do one of the following:
+ If you're using Jenkins, see the [Jenkins documentation](https://www.jenkins.io/doc/book/pipeline/multibranch/) for "Adding a branch source\."
+ If you're using GitLab CI/CD and a Git repository other than GitLab, see the [GitLab documentation](https://docs.gitlab.com/ee/ci/ci_cd_for_external_repos/) for "connecting an external repository\."

## Step 3: Create credential objects<a name="generating-example-step-3"></a>

Each CI/CD system has its own way of managing credentials needed for the CI/CD system to access your Git repository\.

To create the necessary credential objects, do one of the following:
+ If you're using Jenkins, create a single "credential" that stores both the key id and secret key\. Follow the instructions in the [Building a Jenkins Pipeline with AWS SAM](https://aws.amazon.com/blogs/compute/building-a-jenkins-pipeline-with-aws-sam/) blog, in the **Configure Jenkins** section\. You will need the "Credential id" for the next step\.
+ If you're using GitLab CI/CD, create two "protected variables", one for each of key id and secret key\. Follow the instructions in the [GitLab documentation](https://docs.gitlab.com/ee/ci/variables/) – you will need two "variable keys" for the next step\.
+ If you're using GitHub Actions, create two "encrypted secrets", one for each of key and secret key\. Follow the instructions in the [GitHub documentation](https://docs.github.com/en/actions/reference/encrypted-secrets) \- you will need two "secret names" for the next step\.
+ If you're using Bitbucket Pipelines, create two "secure variables", one for each of key id and secret key\. Follow the instructions in the [Variables and secrets ](https://support.atlassian.com/bitbucket-cloud/docs/variables-and-secrets) \- you will need two "secret names" for the next step\.

## Step 4: Generate the pipeline configuration<a name="generating-example-step-4"></a>

To generate the pipeline configuration, run the following command\. You will need to input the credential object that you created in the previous step:

```
sam pipeline init
```

## Step 5: Commit your pipeline configuration to Git repository<a name="generating-example-step-5"></a>

This step is necessary to ensure your CI/CD system is aware of your pipeline configuration, and will run when changes are committed\.

## Learn more<a name="serverless-generating-other-cicd-learn"></a>

For a hands\-on example of setting up a CI/CD pipeline using GitHub Actions, see [CI/CD with GitHub](https://s12d.com/sam-ws-en-gh) in *The Complete AWS SAM Workshop*\.