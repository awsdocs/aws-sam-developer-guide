# Deploying serverless applications<a name="serverless-deploying"></a>

AWS SAM uses AWS CloudFormation as the underlying deployment mechanism\. For more information, see [What is AWS CloudFormation?](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/) in the *AWS CloudFormation User Guide*\. The standard inputs to deploying serverless applications are the build artifacts created using the [sam build](sam-cli-command-reference-sam-build.md) command\. For more information about sam build, see [Building serverless applications](serverless-building.md)\.

You can deploy your application manually using AWS SAM command line interface \(CLI\) commands\. You can also automate the deployments of your application using a continuous integration and continuous deployment \(CI/CD\) system\. You can use many common CI/CD systems for deploying AWS SAM applications, including [AWS CodePipeline](http://aws.amazon.com/codepipeline), [Jenkins](https://www.jenkins.io/), [GitLab CI/CD](https://docs.gitlab.com/ee/ci/), and [GitHub Actions](https://github.com/features/actions)\.

## Deploying using CI/CD systems<a name="serverless-deploying-ci-cd"></a>

AWS SAM helps organizations create pipelines for their preferred CI/CD systems, so that they can realize the benefits of CI/CD with minimal effort, such as accelerating deployment frequency, shortening lead time for changes, and reducing deployment errors\.

AWS SAM simplifies CI/CD tasks for serverless applications with the help of build container images\. The images that AWS SAM provides include the AWS SAM CLI and build tools for a number of supported AWS Lambda runtimes\. This makes it easier to build and package serverless applications using the AWS SAM CLI\. These images also alleviate the need for teams to create and manage their own images for CI/CD systems\. For more information about AWS SAM build container images, see [Image repositories](serverless-image-repositories.md)\.

Multiple CI/CD systems support AWS SAM build container images\. Which CI/CD system you should use depends on several factors\. These include whether your application uses a single runtime or multiple runtimes, or whether you want to build your application within a container image or directly on a host machine, either a virtual machine \(VM\) or bare metal host\.

AWS SAM also provides a set of default pipeline templates for multiple CI/CD systems that encapsulate AWS's deployment best practices\. These default pipeline templates use standard JSON/YAML pipeline configuration formats, and the built\-in best practices help perform multi\-account and multi\-region deployments, and verify that pipelines cannot make unintended changes to infrastructure\.

You have two main options for using AWS SAM to deploy your serverless applications: 1\) Modify your existing pipeline configuration to use AWS SAM CLI commands, or 2\) Generate an example CI/CD pipeline configuration that you can use as a starting point for your own application\.

For more information about these options, see the following topics:
+ [Modifying your existing CI/CD pipelines](serverless-deploying-modify-pipeline.md)
+ [Generating starter CI/CD pipelines](serverless-generating-example-ci-cd.md)

## Deploying using the AWS SAM CLI<a name="serverless-sam-cli-using-package-and-deploy"></a>

After you develop and test your serverless application locally, you can deploy your application using the [sam deploy](sam-cli-command-reference-sam-deploy.md) command\.

To have AWS SAM guide you through the deployment with prompts, specify the \-\-guided flag\. When you specify this flag, the sam deploy command zips your application artifacts, uploads them either to Amazon Simple Storage Service \(Amazon S3\) \(for \.zip file archives\) or to Amazon Elastic Container Registry \(Amazon ECR\) \(for container images\)\. The command then deploys your application to the AWS Cloud\.

**Example:**

```
# Deploy an application using prompts:
sam deploy --guided
```

## Troubleshooting deployments using the AWS SAM CLI<a name="serverless-deploying-troubleshooting"></a>

### AWS SAM CLI error: "Security Constraints Not Satisfied"<a name="troubleshooting-security-constraints"></a>

When running sam deploy \-\-guided, you're prompted with the question `HelloWorldFunction may not have authorization defined, Is this okay? [y/N]`\. If you respond to this prompt with **N** \(the default response\), you see the following error:

```
 
Error: Security Constraints Not Satisfied
```

The prompt is informing you that the application you're about to deploy might have an Amazon API Gateway API configured without authorization\. By responding **N** to this prompt, you're saying that this is not OK\.

To fix this, you have the following options:
+ Configure your application with authorization\. For information about configuring authorization, see [Controlling access to API Gateway APIs](serverless-controlling-access-to-apis.md)\.
+ Respond to this question with **Y** to indicate that you're OK with deploying an application that has an API Gateway API configured without authorization\.

## Gradual deployments<a name="serverless-deploying-gradual"></a>

If you want to deploy your AWS SAM application gradually rather than all at once, you can specify deployment configurations that AWS CodeDeploy provides\. For more information, see [Working with deployment configurations in CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/deployment-configurations.html) in the *AWS CodeDeploy User Guide*\.

For information about configuring your AWS SAM application to deploy gradually, see [Deploying serverless applications gradually](automating-updates-to-serverless-apps.md)\.

## Learn more<a name="serverless-sam-cli-using-invoke-learn"></a>

For hands\-on examples of deploying serverless applications, see the following from *The Complete AWS SAM Workshop*:
+ [Module 3 \- Deploy manually](https://s12d.com/sam-ws-en-manual-deploy) – Learn how to build, package, and deploy a serverless application using the AWS SAM CLI\.
+ [Module 4 \- CI/CD](https://s12d.com/sam-ws-en-cicd-deploy) – Learn how to automate the build, package, and deployment phases by creating a *continuous integration and delivery \(CI/CD\)* pipeline\.