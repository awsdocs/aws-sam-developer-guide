# Installing the AWS SAM CLI<a name="serverless-sam-cli-install"></a>

## Prerequisites<a name="serverless-sam-cli-install-prerequisites"></a>
+ Docker
+ Python 2\.7 or Python 3\.6
+ The [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/setup-awscli.html)

You need to have Docker installed and running to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\.
+ macOS: [Docker for Mac](https://store.docker.com/editions/community/docker-ce-desktop-mac)\.
+ Windows: [Docker For Windows \(create an account and follow through to download from the Docker Store\)](https://www.docker.com/docker-windows)\.
+ Linux: Check your distro's package manager \(for example, `yum install docker`\)\.

  For Centos 7\.5 the requirements are:

  ```
  yum install gcc zip py-pip py-setuptools ca-certificates groff  python-dev g++ make docker epel-release python-pip python-devel\
              python-tools
   # run post install of above
   pip install --upgrade pip
   pip install --upgrade setuptools
   pip install --upgrade aws-sam-cli
  ```

  If you want to use the lambda\-local option \(without running it as root\) you will need to add your user to the docker group

  ```
  usermod -a -G Docker yourUserName
  ```

Verify that Docker is working, and that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You do not need to install/fetch/pull any containers, because the AWS SAM CLI will do it automatically as required\.

**Note**  
For macOS and Windows users: The AWS SAM CLI requires that the project directory \(or any parent directory\) is listed in [Docker file sharing options](https://docs.docker.com/docker-for-mac/osxfs/)\.

## Installing<a name="serverless-sam-cli-install-using-pip"></a>

Install the AWS SAM CLI using PIP by following these steps:

1. Verify that the Python version is 2\.7 or 3\.6\.

   ```
   $ python --version
   ```

   If it isn't installed, [download and install Python](https://www.python.org/downloads/)\.

1. Verify that PIP is installed\.

   ```
   $ pip --version
   ```

   If it isn't installed, [download and install PIP](https://pip.pypa.io/en/stable/installing/)\.

1. Install `aws-sam-cli`\.

   ```
   pip install --user aws-sam-cli
   ```

1. Adjust your `PATH` to include the Python scripts that are installed under the user's home directory\.

   **macOS and Linux:**

   On Unix/Mac systems, the command `python -m site --user-base` typically prints `~/.local` path, so you need to add `/bin` to obtain the script path\.
**Note**  
As explained in the [Python Developer's Guide](https://www.python.org/dev/peps/pep-0370/#specification), the user's home directory \(where the scripts are installed\) is `~/.local/bin` for Unix/Mac\.

   ```
   # Find your Python User Base path (where Python --user will install packages/scripts)
   $ USER_BASE_PATH=$(python -m site --user-base)
   
   # Update your preferred shell configuration
   -- Standard bash --> ~/.bash_profile
   -- ZSH           --> ~/.zshrc
   $ export PATH=$PATH:$USER_BASE_PATH/bin
   ```

   Restart or open a new terminal, and verify that the installation worked:

   ```
   # Restart current shell
   $ exec "$SHELL"
   $ sam --version
   ```

   **Windows:**

   On Windows systems, the command `py -m site --user-site` typically prints `%APPDATA%\Roaming\Python<VERSION>\site-packages`, so you need to remove the last `\site-packages` folder, and replace it with the `\Scripts` folder\.

   ```
   $ python -m site --user-base
   ```

   Using File Explorer, go to the folder that's indicated in the output, and look for the `Scripts` folder\. Visually confirm that the `sam` application is inside this folder\.

   Copy the file path\.
**Note**  
As explained in the [ Python Developer's Guide](https://www.python.org/dev/peps/pep-0370/#specification), the user's home directory \(where the scripts are installed\) is `%APPDATA%\Python\Scripts` for Windows\.

   Search Windows for `Edit the system environment variables`\.

   Choose **Environment Variables**\.

   Under **System Variables**, choose **Path**\.

   Choose **New**, and enter the file path to the Python Scripts folder\.

1. Verify that `sam` is installed\.

   Restart or open a new terminal, and verify that the installation worked\.

   ```
   # Restart current shell
   $ sam --version
   ```

## Upgrading<a name="serverless-sam-cli-install-upgrading"></a>

You can upgrade `sam` by using PIP:

```
$ pip install --user --upgrade aws-sam-cli
```

You must first uninstall previous versions of the AWS SAM CLI \(0\.2\.11 or earlier\)\. Then follow the earlier installation steps\. To uninstall, use this command:

```
$ npm uninstall -g aws-sam-local
```

## Advanced Installations<a name="serverless-sam-cli-install-advanced"></a>

### Build from Source<a name="serverless-sam-cli-install-advanced-from-source"></a>

First, install Python \(2\.7 or 3\.6\) on your machine, and then run the following:

```
# Clone the repository
$ git clone git@github.com:awslabs/aws-sam-cli.git

# cd into the git
$ cd aws-sam-cli

# pip install the repository
$ pip install --user -e .
```

### Install with PyEnv<a name="serverless-sam-cli-install-advanced-pyenv"></a>

```
# Install PyEnv (https://github.com/pyenv/pyenv#installation)
$ brew update
$ brew install pyenv

# Initialize pyenv using bash_profile
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi\nexport PATH="~/.pyenv/bin:$PATH"' >> ~/.bash_profile
# or using zshrc
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi\nexport PATH="~/.pyenv/bin:$PATH"' >> ~/.zshrc

# restart the shell
$ exec "$SHELL"

# Install Python 2.7
$ pyenv install 2.7.14
$ pyenv local 2.7.14

# Install the CLI
$ pip install --user aws-sam-cli

# Verify your installation worked
$ sam –-version
```

### Updating AWS SAM on AWS Cloud9<a name="serverless-sam-cli-install-advanced-cloud9"></a>

If your AWS Cloud9 environment has an AWS SAM CLI version earlier than 0\.3\.0 installed, there are a few extra steps that you must do to upgrade to newer versions:

```
# Uninstall the older version of SAM Local
$ npm uninstall -g aws-sam-local

# Remove the symlink
$ rm -rf $(which sam)

# Install the CLI
$ pip install --user aws-sam-cli

# Create new symlink
$ ln -sf $(which sam) ~/.c9/bin/sam

# Reset the bash cache
$ hash -r

# Verify your installation worked
$ sam –-version
```

## Troubleshooting<a name="serverless-sam-cli-install-troubleshooting"></a>

### Mac Issues<a name="serverless-sam-cli-install-troubleshooting-mac"></a>

**TLSV1\_ALERT\_PROTOCOL\_VERSION**

If you get an error similar to the following, then you're probably using the default version of Python that came with your Mac\. This is outdated\. 

```
Could not fetch URL https://pypi.python.org/simple/click/: There was a problem confirming the ssl certificate: [SSL: TLSV1_ALERT_PROTOCOL_VERSION] tlsv1 alert protocol version (_ssl.c:590) - skipping
```

Make sure that you install Python again using Homebrew and try again:

```
$ brew install python
```

After it's installed, then repeat the installation process\.