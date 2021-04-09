# Image repositories<a name="serverless-image-repositories"></a>

The following table lists the URIs of container images that you can use to build serverless applications with AWS SAM\.

Prior to version 1\.22\.0 of the AWS SAM CLI, DockerHub was the default repository that the AWS SAM CLI pulled the container image from\. Starting with version 1\.22\.0, the default repository changed to [Amazon ECR Public](https://docs.aws.amazon.com/AmazonECR/latest/public/what-is-ecr.html)\. To pull a container image from a repository other than the current default, you can use the [sam build](sam-cli-command-reference-sam-build.md) command with the `--build-image` option\.

Following are two example commands for building applications using container images from the DockerHub repository:

```
# Build a Node.js 12 application using a container image pulled from DockerHub
sam build --use-container --build-image amazon/aws-sam-cli-build-image-nodejs12.x

# Build a function resource using using the Python 3.8 container image pulled from DockerHub
sam build --use-container --build-image Function1=amazon/aws-sam-cli-build-image-python3.8
```

## Image repository URIs<a name="serverless-image-repository-uris"></a>


| Runtime | Amazon ECR Public\(default starting with version 1\.22\.0\)  | DockerHub \(default prior to version 1\.22\.0\)  | 
| --- | --- | --- | 
| Node\.js 14 | [public\.ecr\.aws/sam/build\-nodejs14\.x](https://gallery.ecr.aws/sam/build-nodejs14.x) | [amazon/aws\-sam\-cli\-build\-image\-nodejs14\.x](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-nodejs14.x) | 
| Node\.js 12 | [public\.ecr\.aws/sam/build\-nodejs12\.x](https://gallery.ecr.aws/sam/build-nodejs12.x) | [amazon/aws\-sam\-cli\-build\-image\-nodejs12\.x](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-nodejs12.x) | 
| Node\.js 10 | [public\.ecr\.aws/sam/build\-nodejs10\.x](https://gallery.ecr.aws/sam/build-nodejs10.x) | [amazon/aws\-sam\-cli\-build\-image\-nodejs10\.x](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-nodejs10.x) | 
| Python 3\.8 | [public\.ecr\.aws/sam/build\-python3\.8](https://gallery.ecr.aws/sam/build-python3.8) | [amazon/aws\-sam\-cli\-build\-image\-python3\.8](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-python3.8) | 
| Python 3\.7 | [public\.ecr\.aws/sam/build\-python3\.7](https://gallery.ecr.aws/sam/build-python3.7) | [amazon/aws\-sam\-cli\-build\-image\-python3\.7](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-python3.7) | 
| Python 3\.6 | [public\.ecr\.aws/sam/build\-python3\.6](https://gallery.ecr.aws/sam/build-python3.6) | [amazon/aws\-sam\-cli\-build\-image\-python3\.6](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-python3.7) | 
| Python 2\.7 | [public\.ecr\.aws/sam/build\-python2\.7](https://gallery.ecr.aws/sam/build-python2.7) | [amazon/aws\-sam\-cli\-build\-image\-python2\.7](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-python2.7) | 
| Ruby 2\.7 | [public\.ecr\.aws/sam/build\-ruby2\.7](https://gallery.ecr.aws/sam/build-ruby2.7) | [amazon/aws\-sam\-cli\-build\-image\-ruby2\.7](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-rub2.7) | 
| Ruby 2\.5 | [public\.ecr\.aws/sam/build\-ruby2\.5](https://gallery.ecr.aws/sam/build-ruby2.5) | [amazon/aws\-sam\-cli\-build\-image\-ruby2\.5](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-rub2.5) | 
| Java 11 | [public\.ecr\.aws/sam/build\-java11](https://gallery.ecr.aws/sam/build-java11) | [amazon/aws\-sam\-cli\-build\-image\-java11](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-java11) | 
| Java 8 \(AL2\) | [public\.ecr\.aws/sam/build\-java8\.al2](https://gallery.ecr.aws/sam/build-java8.al2) | [amazon/aws\-sam\-cli\-build\-image\-java8\.al2](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-java8.al2) | 
| Java 8 | [public\.ecr\.aws/sam/build\-java8](https://gallery.ecr.aws/sam/build-java8) | [amazon/aws\-sam\-cli\-build\-image\-java8](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-java8) | 
| Custom runtime \(AL2\) | [public\.ecr\.aws/sam/build\-provided\.al2](https://gallery.ecr.aws/sam/build-provided.al2) | [amazon/aws\-sam\-cli\-build\-image\-provided\.al2](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-provided.al2) | 
| Custom runtime | [public\.ecr\.aws/sam/build\-provided](https://gallery.ecr.aws/sam/build-provided) | [amazon/aws\-sam\-cli\-build\-image\-provided](https://hub.docker.com/r/amazon/aws-sam-cli-build-image-provided) | 