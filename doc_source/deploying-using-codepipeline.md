# Deploying using AWS CodePipeline<a name="deploying-using-codepipeline"></a>

To configure your [AWS CodePipeline](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html) pipeline to automate the build and deployment of your AWS SAM application, your AWS CloudFormation template and `buildspec.yml` file must contain lines that do the following:

1. Reference a build container image with the necessary runtime from the available images\. The following example uses the `public.ecr.aws/sam/build-nodejs14.x` build container image\.

1. Configure the pipeline stages to run the necessary AWS SAM command line interface \(CLI\) commands\. The following example runs two AWS SAM CLI commands: sam build and sam deploy \(with necessary options\)\.

This example assumes that you have declared all functions and layers in your AWS SAM template file with `runtime: nodejs14.x`\.

**AWS CloudFormation template snippet:**

```
  CodeBuildProject:
    Type: AWS::CodeBuild::Project
    Properties:
      Environment:
        ComputeType: BUILD_GENERAL1_SMALL
        Image: public.ecr.aws/sam/build-nodejs14.x
        Type: LINUX_CONTAINER
      ...
```

**`buildspec.yml` snippet:**

```
version: 0.2
phases:
  build:
    commands:
      - sam build
      - sam deploy --no-confirm-changeset --no-fail-on-empty-changeset
```

For a list of available Amazon Elastic Container Registry \(Amazon ECR\) build container images for different runtimes, see [Image repositories](serverless-image-repositories.md)\.