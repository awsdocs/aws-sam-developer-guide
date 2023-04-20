# Image repositories<a name="serverless-image-repositories"></a>

AWS SAM simplifies continuous integration and continuous delivery \(CI/CD\) tasks for serverless applications with the help of build container images\. The images that AWS SAM provides include the AWS SAM command line interface \(CLI\) and build tools for a number of supported AWS Lambda runtimes\. This make it easier to build and package serverless applications using the AWS SAM CLI\. You can use these images with CI/CD systems to automate the building and deployment of AWS SAM applications\. For examples, see [Deploying using CI/CD systems](serverless-deploying.md#serverless-deploying-ci-cd)\.

AWS SAM build container image URIs are tagged with the version of the AWS SAM CLI included in that image\. If you specify the untagged URI, then the latest version is used\. For example, `public.ecr.aws/sam/build-nodejs14.x` uses the latest image\. However, `public.ecr.aws/sam/build-nodejs14.x:1.24.1` uses the the image containing AWS SAM CLI version 1\.24\.1\.

Starting with version 1\.33\.0 of the AWS SAM CLI, both `x86_64` and `arm64` container images are available for supported runtimes\. For more information, see [Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) in the *AWS Lambda Developer Guide*\.

**Note**  
Prior to version 1\.22\.0 of the AWS SAM CLI, DockerHub was the default repository that the AWS SAM CLI pulled the container image from\. Starting with version 1\.22\.0, the default repository changed to Amazon Elastic Container Registry Public \(Amazon ECR Public\)\. To pull a container image from a repository other than the current default, you can use the [sam build](sam-cli-command-reference-sam-build.md) command with the \-\-build\-image option\. The examples at the end of this topic show how to build applications using DockerHub repository images\.

## Image repository URIs<a name="serverless-image-repository-uris"></a>

The following table lists the URIs of [Amazon ECR Public](https://docs.aws.amazon.com/AmazonECR/latest/public/what-is-ecr.html) build container images that you can use to build and package serverless applications with AWS SAM\.

**Note**  
Amazon ECR Public replaced DockerHub starting with the AWS SAM CLI version 1\.22\.0\. If you are using an earlier version of the AWS SAM CLI, we recommend that you upgrade\.


| Runtime |  Amazon ECR Public | 
| --- | --- | 
| \.NET 7 | [public\.ecr\.aws/sam/build\-dotnet7](https://gallery.ecr.aws/sam/build-dotnet7) | 
| \.NET 6 | [public\.ecr\.aws/sam/build\-dotnet6](https://gallery.ecr.aws/sam/build-dotnet6) | 
| \.NET Core 3\.1 | [public\.ecr\.aws/sam/build\-dotnetcore3\.1](https://gallery.ecr.aws/sam/build-dotnetcore3.1) | 
| Node\.js 18 | [public\.ecr\.aws/sam/build\-nodejs18\.x](https://gallery.ecr.aws/sam/build-nodejs18.x) | 
| Node\.js 16 | [public\.ecr\.aws/sam/build\-nodejs16\.x](https://gallery.ecr.aws/sam/build-nodejs16.x) | 
| Node\.js 14 | [public\.ecr\.aws/sam/build\-nodejs14\.x](https://gallery.ecr.aws/sam/build-nodejs14.x) | 
| Node\.js 12 | [public\.ecr\.aws/sam/build\-nodejs12\.x](https://gallery.ecr.aws/sam/build-nodejs12.x) | 
| Python 3\.10 | [public\.ecr\.aws/sam/build\-python3\.10](https://gallery.ecr.aws/sam/build-python3.10) | 
| Python 3\.9 | [public\.ecr\.aws/sam/build\-python3\.9](https://gallery.ecr.aws/sam/build-python3.9) | 
| Python 3\.8 | [public\.ecr\.aws/sam/build\-python3\.8](https://gallery.ecr.aws/sam/build-python3.8) | 
| Python 3\.7 | [public\.ecr\.aws/sam/build\-python3\.7](https://gallery.ecr.aws/sam/build-python3.7) | 
| Ruby 2\.7 | [public\.ecr\.aws/sam/build\-ruby2\.7](https://gallery.ecr.aws/sam/build-ruby2.7) | 
| Java 17 | [public\.ecr\.aws/sam/build\-java17](https://gallery.ecr.aws/sam/build-java17) | 
| Java 11 | [public\.ecr\.aws/sam/build\-java11](https://gallery.ecr.aws/sam/build-java11) | 
| Java 8 \(AL2\) | [public\.ecr\.aws/sam/build\-java8\.al2](https://gallery.ecr.aws/sam/build-java8.al2) | 
| Java 8 | [public\.ecr\.aws/sam/build\-java8](https://gallery.ecr.aws/sam/build-java8) | 
| Go 1\.x | [public\.ecr\.aws/sam/build\-go1\.x](https://gallery.ecr.aws/sam/build-go1.x) | 
| Custom runtime \(AL2\) | [public\.ecr\.aws/sam/build\-provided\.al2](https://gallery.ecr.aws/sam/build-provided.al2) | 
| Custom runtime | [public\.ecr\.aws/sam/build\-provided](https://gallery.ecr.aws/sam/build-provided) | 

## Examples<a name="serverless-image-repository-example-commands"></a>

The following two example commands build applications using container images from the DockerHub repository:

**Build a Node\.js 12 application using a container image pulled from DockerHub**:

```
$ sam build --use-container --build-image amazon/aws-sam-cli-build-image-nodejs12.x
```

**Build a function resource using the Python 3\.8 container image pulled from DockerHub**:

```
$ sam build --use-container --build-image Function1=amazon/aws-sam-cli-build-image-python3.8
```