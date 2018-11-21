# Advanced Installations<a name="serverless-sam-cli-install-advanced"></a>

## Build from Source<a name="serverless-sam-cli-install-advanced-from-source"></a>

First, install Python \(2\.7 or 3\.6\) on your machine, and then run the following:

```
# Clone the repository
$ git clone git@github.com:awslabs/aws-sam-cli.git

# cd into the git
$ cd aws-sam-cli

# pip install the repository
$ pip install --user -e .
```

## Install with PyEnv<a name="serverless-sam-cli-install-advanced-pyenv"></a>

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

## Updating AWS SAM on AWS Cloud9<a name="serverless-sam-cli-install-advanced-cloud9"></a>

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