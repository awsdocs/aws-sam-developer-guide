# Installing Homebrew to use with the AWS SAM CLI<a name="install-homebrew"></a>

You can optionally use Homebrew to install and manage versions of the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) on macOS and Linux machines\. To use Homebrew, follow the installation instructions here\.

**Topics**
+ [Installing Git](#install-homebrew-git)
+ [Installing Homebrew](#install-homebrew-instructions)
+ [Next steps](#install-homebrew-next-steps)

## Installing Git<a name="install-homebrew-git"></a>

To install Homebrew, you must first install Git\. Git is available on many different operating systems, including most modern Linux distributions and macOS\. For instructions about installing Git on your particular operating system, see [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) on the Git website\.

## Installing Homebrew<a name="install-homebrew-instructions"></a>

### Linux<a name="instal-homebrew-instructions-linux"></a>

**Note**  
Installing Homebrew changes your environment's default Python version to the one that Homebrew installs\.

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

### macOS<a name="install-homebrew-instructions-macos"></a>

After you have successfully installed Git, run the following to install Homebrew, making sure to follow the prompts:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Verify that Homebrew is installed:

```
brew --version
```

On successful installation of Homebrew, you should see output like the following:

```
Homebrew 2.5.7
Homebrew/homebrew-core (git revision 1be3ad; last commit 2020-10-29)
Homebrew/homebrew-cask (git revision a0cf3; last commit 2020-10-29)
```

## Next steps<a name="install-homebrew-next-steps"></a>

To install the AWS SAM CLI, see [Installing the AWS SAM CLI](install-sam-cli.md)\.