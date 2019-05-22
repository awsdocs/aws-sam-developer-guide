# Additional Installation Topics<a name="serverless-sam-cli-install-additional"></a>

The topics listed below contain additional information about installing the AWS SAM CLI\.

## Installing Using Pip<a name="serverless-sam-cli-install-using-pip"></a>

To install the AWS SAM CLI using pip, first make sure that you've installed the [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) and Docker for the platform you're using:
+ [Docker for Linux](serverless-sam-cli-install-linux.md#serverless-sam-cli-install-linux-docker)
+ [Install Docker for Windows](serverless-sam-cli-install-windows.md#serverless-sam-cli-install-windows-docker)
+ [Docker for macOS](serverless-sam-cli-install-mac.md#serverless-sam-cli-install-mac-docker)

## <a name="w4aac26b7c17b9"></a>

Follow these steps to install the AWS SAM CLI by using pip:

1. Verify that the Python version is 2\.7 or 3\.6\.

   ```
   $ python --version
   ```

   If it isn't installed, [download and install Python](https://www.python.org/downloads/)\.

1. Verify that pip is installed\.

   ```
   $ pip --version
   ```

   If it isn't installed, [download and install pip](https://pip.pypa.io/en/stable/installing/)\.

1. Install `aws-sam-cli`\.

   ```
   pip install --user aws-sam-cli
   ```

1. Adjust your `PATH` to include the Python scripts that are installed under the user's home directory\.
   + **Linux:** [Adjusting Your Path on Linux](serverless-sam-cli-install-linux-path.md)
   + **Windows:** [Adjusting Your Path on Windows](serverless-sam-cli-install-windows-path.md)
   + **macOS:** [Adjusting Your Path on macOS](serverless-sam-cli-install-mac-path.md)

1. Verify that `sam` is installed\.

   Restart or open a new terminal, and verify that the installation worked\.

   ```
   # Restart current shell
   $ sam --version
   ```

## Upgrading<a name="serverless-sam-cli-install-upgrading"></a>

You can upgrade `sam` by using pip:

```
$ pip install --user --upgrade aws-sam-cli
```

First uninstall previous versions of the AWS SAM CLI \(0\.2\.11 or earlier\)\. Then follow the earlier installation steps\. To uninstall, use this command:

```
$ npm uninstall -g aws-sam-local
```

## Building from Source<a name="serverless-sam-cli-install-additional-from-source"></a>

To build from source, first install Python \(2\.7 or 3\.6\) on your machine, and then run the following:

```
# Clone the repository
$ git clone git@github.com:awslabs/aws-sam-cli.git

# cd into the git
$ cd aws-sam-cli

# pip install the repository
$ pip install --user -e .
```

## Installing with PyEnv<a name="serverless-sam-cli-install-additional-pyenv"></a>

To install with PyEnv, run the following commands:

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
$ sam --version
```

## Updating on AWS Cloud9<a name="serverless-sam-cli-install-additional-cloud9"></a>

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
$ sam --version
```