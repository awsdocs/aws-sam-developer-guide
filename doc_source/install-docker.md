# Installing Docker to use with the AWS SAM CLI<a name="install-docker"></a>

Docker is an application that runs containers on your machine\. With Docker, AWS SAM can provide a local environment similar to AWS Lambda as a container to build, test, and debug your serverless applications\.

**Note**  
Docker is required only for testing your applications locally and for building deployment packages using the `--use-container` option\.

**Topics**
+ [Installing Docker](#install-docker-instructions)
+ [Next steps](#install-docker-next-steps)

## Installing Docker<a name="install-docker-instructions"></a>

Follow these instructions to install Docker on your operating system\.

### Linux<a name="install-docker-instructions-linux"></a>

Docker is available on many different operating systems, including most modern Linux distributions, for example, CentOS, Debian, and Ubuntu\. For information about installing Docker on your particular operating system, see [Get Docker](https://docs.docker.com/get-docker/) on the Docker Docs website\.

If you're using Amazon Linux 2, follow these steps to install Docker:

1. Update the installed packages and package cache on your instance\.

   ```
   sudo yum update -y
   ```

1. Install the most recent Docker Community Edition package\.

   ```
   sudo amazon-linux-extras install docker
   ```

1. Start the Docker service\.

   ```
   sudo service docker start
   ```

1. Add the `ec2-user` to the `docker` group so that you can run Docker commands without using sudo\.

   ```
   sudo usermod -a -G docker ec2-user
   ```

1. Pick up the new `docker` group permissions by logging out and logging back in again\. To do this, close your current SSH terminal window and reconnect to your instance in a new one\. Your new SSH session should have the appropriate `docker` group permissions\.

1. Verify that the `ec2-user` can run Docker commands without using sudo\.

   ```
   docker ps
   ```

   You should see the following output, confirming that Docker is installed and running:

   ```
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
   ```

**Note**  
On Linux, to build and run Lambda functions with a different instruction set architecture than your host machine, there are additional steps to configure Docker\. For example, to run `arm64` functions on an `x86_64` machine, you can run the following command to configure the Docker daemon: `docker run --rm --privileged multiarch/qemu-user-static --reset -p yes`\.

If you run into issues installing Docker, see [Installation errors](sam-cli-troubleshooting.md#sam-cli-troubleshoot-install)\. Or, see the [Troubleshooting](https://docs.docker.com/engine/install/linux-postinstall/#troubleshooting) section of **Post\-installation steps for Linux** on the Docker Docs website\.

### macOS<a name="install-docker-instructions-macos"></a>

**Note**  
Docker Desktop is officially supported, but starting with AWS SAM CLI version 1\.47\.0, you can use alternatives as long as they use the Docker runtime\.

1. Install Docker

   The AWS SAM CLI supports Docker running on macOS Sierra 10\.12 or later\. For how to install Docker, see [Install Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/) on the Docker Docs website\.

1. Configure your shared drives

   The AWS SAM CLI requires that the project directory, or any parent directory, is listed in a shared drive\. This may require file sharing\. For more information, see the [ Volume mounting requires file sharing](https://docs.docker.com/desktop/troubleshoot/topics/#volume-mounting-requires-file-sharing-for-any-project-directories-outside-of-home) troubleshooting topic at *Docker docs*\.

1. Verify the installation

   After Docker is installed, verify that it's working\. Also confirm that you can run Docker commands from the command line \(for example, `docker ps`\)\. You don't need to install, fetch, or pull any containers—the AWS SAM CLI does this automatically as required\.

If you run into issues installing Docker, for more troubleshooting tips, see the [Troubleshoot and diagnose](https://docs.docker.com/docker-for-mac/troubleshoot/) section of the Docker Docs website\.

### Windows<a name="install-docker-instructions-windows"></a>

**Note**  
AWS SAM officially supports Docker Desktop\. However, starting with AWS SAM CLI version 1\.47\.0, you can use alternatives as long as they use the Docker runtime\.

1. Install Docker\.

   Docker Desktop supports the most recent Windows operating system\. For legacy versions of Windows, the Docker Toolbox is available\. Choose your version of Windows for the correct Docker installation steps:
   + To install Docker for Windows 10, see [Install Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/) on the Docker Docs website\.
   + To install Docker for earlier versions of Windows, see [The Docker Toolbox](https://github.com/docker-archive/toolbox) on the Docker Toolbox GitHub repository\.

1. Configure your shared drives\.

   The AWS SAM CLI requires that the project directory, or any parent directory, is listed in a shared drive\. In some cases, you must share your drive for Docker to function properly\.

1. Verify the installation\.

   After Docker is installed, verify that it's working\. Also confirm that you can run Docker commands from the command line \(for example, docker ps\)\. You don't need to install, fetch, or pull any containers—the AWS SAM CLI does this automatically as required\.

If you run into issues installing Docker, for more troubleshooting tips, see the [Troubleshoot and diagnose](https://docs.docker.com/docker-for-mac/troubleshoot/) section of the Docker Docs website\.

## Next steps<a name="install-docker-next-steps"></a>

For how to install the AWS SAM CLI, see [Installing the AWS SAM CLI](install-sam-cli.md)\.