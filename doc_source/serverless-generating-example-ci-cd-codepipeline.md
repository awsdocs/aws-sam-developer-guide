# Generating starter pipeline for AWS CodePipeline<a name="serverless-generating-example-ci-cd-codepipeline"></a>

To generate a starter pipeline configuration for AWS CodePipeline, perform the following tasks in this order:

1. Create infrastructure resources

1. Generate the pipeline configuration

1. Commit your pipeline configuration to Git

1. Connect your Git repository with your CI/CD system

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

## Step 2: Generate the pipeline configuration<a name="generating-example-step-2"></a>

To generate the pipeline configuration, run the following command:

```
sam pipeline init
```

## Step 3: Commit your pipeline configuration to Git repository<a name="generating-example-step-3"></a>

This step is necessary to ensure your CI/CD system is aware of your pipeline configuration, and will run when changes are committed\.

## Step 4: Connect your Git repository with your CI/CD system<a name="generating-example-step-4"></a>

For AWS CodePipeline you can now create the connection by running the following command:

```
sam deploy -t codepipeline.yaml --stack-name <pipeline-stack-name> --capabilities=CAPABILITY_IAM --region <region-X>
```

If you are using GitHub or Bitbucket, after running the sam deploy command previously, complete the connection by following the steps under **To complete a connection** found on the [Update a pending connection](https://docs.aws.amazon.com/dtconsole/latest/userguide/connections-update.html) topic in the *Developer Tools console user guide*\. In addition, store a copy of the `CodeStarConnectionArn` from the output of the sam deploy command, because you will need it if you want to use AWS CodePipeline with another branch than `main`\.

## Configuring other branches<a name="configuring-other-branches"></a>

By default, AWS CodePipeline uses the `main` branch with AWS SAM\. If you want to use a branch other than `main`, you must run the sam deploy command again\. Note that depending on which Git repository you are using, you may also need to provide the `CodeStarConnectionArn`:

```
# For GitHub and Bitbucket
sam deploy -t codepipeline.yaml --stack-name <feature-pipeline-stack-name> --capabilities=CAPABILITY_IAM --parameter-overrides="FeatureGitBranch=<branch-name> CodeStarConnectionArn=<codestar-connection-arn>"

# For AWS CodeCommit
sam deploy -t codepipeline.yaml --stack-name <feature-pipeline-stack-name> --capabilities=CAPABILITY_IAM --parameter-overrides="FeatureGitBranch=<branch-name>"
```