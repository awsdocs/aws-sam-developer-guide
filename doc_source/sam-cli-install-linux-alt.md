# Installing the AWS SAM CLI on Linux using Homebrew<a name="sam-cli-install-linux-alt"></a>

To install the AWS SAM CLI on Linux, you can use the Homebrew package manager\. For more information about Homebrew, see [Homebrew on Linux](https://docs.brew.sh/Homebrew-on-Linux) on the Homebrew Documentation website\.

**Note**  
Installing Homebrew changes your environment's default Python version to the one that Homebrew installs\.

To install Homebrew, you must first install Git\. Git is available on many different operating systems, including most modern Linux distributions\. For instructions about installing Git on your particular operating system, see [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) on the Git website\.

## Install Homebrew<a name="sam-cli-install-linux-alt-homebrew"></a>

After successfully installing Git, to install Homebrew, run the following command:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Next, add Homebrew to your PATH by running the following commands\. These commands work on all major flavors of Linux by adding either `~/.profile` on Debian and Ubuntu, or `~/.bash_profile` on CentOS, Fedora, and Red Hat\.

```
test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile
```

Verify that Homebrew is installed\.

```
brew --version
```

On successful installation of Homebrew, you should see output like the following:

```
 
 Homebrew 2.1.6 
 Homebrew/homebrew-core (git revision ef21; last commit 2019-06-19)
```

## Install the AWS SAM CLI using Homebrew<a name="sam-cli-install-linux-alt-sam-cli"></a>

To install the AWS SAM CLI using Homebrew, run the following commands:

```
brew tap aws/tap
brew install aws-sam-cli
```

Verify the installation\.

```
sam --version
```

On successful installation of the AWS SAM CLI, you should see output like the following:

```
 
 SAM CLI, version 1.15.0
```

## Upgrading the AWS SAM CLI using Homebrew<a name="sam-cli-install-linux-alt-upgrading"></a>

To upgrade the AWS SAM CLI using Homebrew, replace install with upgrade as follows:

```
brew upgrade aws-sam-cli
```

## Troubleshooting<a name="sam-cli-install-linux-alt-troubleshooting"></a>

### Installing Homebrew message: "Enter your password to install to /home/linuxbrew/\.linuxbrew"<a name="serverless-sam-cli-install-linux-troubleshooting-homebrew-enter-password"></a>

During the **Install Homebrew** step, by default you're prompted to provide a password\. However, you might not want to set up a password for the current user, for example, when you're setting up a non\-interactive environment like CI/CD systems\.

If you don't want to set up a password for the current user, you can install Homebrew in non\-interactive mode by setting the environment variable `CI=1`\. For example:

```
CI=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

### Installing AWS SAM CLI error: "The following formulae cannot be installed from bottles and must be built from source\. pkg\-config, gdbm, openssl@1\.1, ncurses, xz and python@3\.8"<a name="serverless-sam-cli-install-linux-troubleshooting-build-from-sourced"></a>

If you see this error while installing the AWS SAM CLI, you don't have the `gcc` module installed\. Install the `gcc` module for your Linux distribution\.

```
# for Amazon Linux, Amazon Linux 2, CentOS and Red Hat:
sudo yum install gcc
# for Debian and Ubuntu:
sudo apt-get update
sudo apt-get install gcc
```

After installing the `gcc` module, run the commands in the **Install the AWS SAM CLI using Homebrew** section again\.

### Shell error: "command not found"<a name="serverless-sam-cli-install-linux-troubleshooting-homebrew-sam-cli-not-found"></a>

If you receive this error, your shell can't locate the AWS SAM CLI executable in the PATH\. Verify the location of the directory where you installed the AWS SAM CLI executable, and then verify that the directory is on your PATH\.

For example, if you used the instructions in this topic to both install Homebrew and use Homebrew to install the AWS SAM CLI, then the AWS SAM CLI executable is installed to the following location:

```
 /home/linuxbrew/.linuxbrew/bin/sam
```