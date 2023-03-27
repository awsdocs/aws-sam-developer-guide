# Managing AWS SAM CLI versions<a name="manage-sam-cli-versions"></a>

Manage your AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) versions through upgrading, downgrading, and uninstalling\. Optionally, you can download and install the AWS SAM CLI nightly build\.

**Topics**
+ [Upgrading the AWS SAM CLI](#manage-sam-cli-versions-upgrade)
+ [Uninstalling the AWS SAM CLI](#manage-sam-cli-versions-uninstall)
+ [Installing the AWS SAM CLI nightly build](#manage-sam-cli-versions-nightly-build)
+ [Installing the AWS SAM CLI into a virtual environment using pip](#manage-sam-cli-versions-install-virtual)
+ [Troubleshooting](#manage-sam-cli-versions-troubleshoot)

## Upgrading the AWS SAM CLI<a name="manage-sam-cli-versions-upgrade"></a>

### Linux<a name="manage-sam-cli-versions-upgrade-linux"></a>

To upgrade the AWS SAM CLI on Linux, follow the installation instructions in [Installing the AWS SAM CLI](install-sam-cli.md#install-sam-cli-instructions), but add the \-\-update option to the install command, as follows:

```
sudo ./sam-installation/install --update
```

### macOS<a name="manage-sam-cli-versions-upgrade-macos"></a>

Upgrade the AWS SAM CLI through the same service that was used to install it\.

#### Homebrew<a name="manage-sam-cli-versions-upgrade-macos-homebrew"></a>

To upgrade the AWS SAM CLI on macOS using Homebrew, run the following command:

```
$ brew upgrade aws-sam-cli
```

**Note**  
To upgrade to AWS SAM v1\.70\.1 or newer, we recommend running brew upgrade aws/tap/aws\-sam\-cli instead\. 

#### Package installer<a name="manage-sam-cli-versions-upgrade-macos-pkg"></a>

 To upgrade the AWS SAM CLI using the package installer, install the latest package version\. For instructions, see [Installing the AWS SAM CLI](install-sam-cli.md#install-sam-cli-instructions)\. 

### Windows<a name="manage-sam-cli-versions-upgrade-windows"></a>

To upgrade the AWS SAM CLI, repeat the Windows installation steps in [Installing the AWS SAM CLI](install-sam-cli.md) again\.

## Uninstalling the AWS SAM CLI<a name="manage-sam-cli-versions-uninstall"></a>

### Linux<a name="manage-sam-cli-versions-uninstall-linux"></a>

To uninstall the AWS SAM CLI on Linux, you must delete the symlink and installation directory by running the following commands:

1. Locate the symlink and install paths\.
   + Find the symlink using the which command:

     ```
     which sam
     ```

     The output shows the path where the AWS SAM binaries are located, for example:

     ```
      /usr/local/bin/sam
     ```
   + Find the directory that the symlink points to using the ls command:

     ```
     ls -l /usr/local/bin/sam
     ```

     In the following example, the installation directory is `/usr/local/aws-sam-cli`\.

     ```
      lrwxrwxrwx 1 ec2-user ec2-user 49 Oct 22 09:49 /usr/local/bin/sam -> /usr/local/aws-sam-cli/current/bin/sam
     ```

1. Delete the symlink\.

   ```
   sudo rm /usr/local/bin/sam
   ```

1. Delete the installation directory\.

   ```
   sudo rm -rf /usr/local/aws-sam-cli
   ```

### macOS<a name="manage-sam-cli-versions-uninstall-macos"></a>

 Uninstall the AWS SAM CLI through the same service that was used to install it\. 

#### Homebrew<a name="manage-sam-cli-versions-uninstall-macos-homebrew"></a>

 If the AWS SAM CLI was installed using Homebrew or pip, uninstall it by running the following: 

```
$ pip uninstall aws-sam-cli && brew uninstall aws-sam-cli
```

 Verify that the AWS SAM CLI is uninstalled by running the following: 

```
$ sam --version
command not found: sam
```

#### Package installer<a name="manage-sam-cli-versions-uninstall-macos-pkg"></a>

 If the AWS SAM CLI was installed using the package installer, uninstall it with the following commands\. 

1.  Remove the AWS SAM CLI program by modifying and running the following: 

   ```
   $ sudo rm -rf /path-to/aws-sam-cli
   ```

   1.  *sudo* – If your user has write permissions to where the AWS SAM CLI program is installed, sudo is not required\. Otherwise, sudo is required\. 

   1.  */path\-to* – Path to where you installed the AWS SAM CLI program\. The default location is `/usr/local`\. 

1.  Remove the AWS SAM CLI `$PATH` by modifying and running the following: 

   ```
   $ sudo rm -rf /path-to-symlink-directory/sam
   ```

   1.  *sudo* – If your user has write permissions to `$PATH`, sudo is not required\. Otherwise, sudo is required\. 

   1.  *path\-to\-symlink\-directory* – Your `$PATH` environment variable\. The default location is `/usr/local/bin`\. 

1.  Verify that the AWS SAM CLI is uninstalled by running the following: 

   ```
   $ sam --version
   command not found: sam
   ```

### Windows<a name="manage-sam-cli-versions-uninstall-windows"></a>

To uninstall the AWS SAM CLI using Windows Settings, follow these steps:

1. From the Start menu, search for "Add or remove programs"\.

1. Choose the result named **AWS SAM Command Line Interface**, and then choose **Uninstall** to launch the uninstaller\.

1. Confirm that you want to uninstall the AWS SAM CLI\.

## Installing the AWS SAM CLI nightly build<a name="manage-sam-cli-versions-nightly-build"></a>

You can download and install the AWS SAM CLI nightly build\. It contains a pre\-release version of the AWS SAM CLI code that may be less stable than the production version\. When installed, you can use the nightly build with the sam\-nightly command\. You can install and use both the production and nightly build versions of the AWS SAM CLI at the same time\.

**Note**  
The nightly build does not contain a pre\-release version of the build image\. Because of that, building your serverless application with the \-\-use\-container option uses the latest production version of the build image\.

To install the AWS SAM CLI nightly build, follow these instructions\.

### Linux<a name="manage-sam-cli-versions-nightly-build-linux"></a>

------
#### [ Command line installer ]

The nightly build is available with this download link: [AWS SAM CLI nightly build](https://github.com/aws/aws-sam-cli/releases/download/sam-cli-nightly/aws-sam-cli-linux-x86_64.zip)\. To install the nightly build version of the AWS SAM CLI, perform the same steps as in the [Installing the AWS SAM CLI](install-sam-cli.md#install-sam-cli-instructions) section, but use the nightly build download link instead\. You can find the hash values for the nightly build installer files in the [AWS SAM CLI release notes for nightly builds](https://github.com/aws/aws-sam-cli/releases/tag/sam-cli-nightly) on GitHub\.

To verify that you have installed the nightly build version, run the sam\-nightly \-\-version command\. The output of this command is in the form `1.X.Y.dev<YYYYMMDDHHmm>`, for example:

```
SAM CLI, version 1.20.0.dev202103151200
```

------
#### [ Homebrew ]

To install the nightly build version of the AWS SAM CLI on Linux, using Homebrew, run the following commands:

```
brew tap aws/tap
brew install aws-sam-cli-nightly
```

To verify that you have installed the nightly build version, run the sam\-nightly \-\-version command\. The output of this command is in the form `1.X.Y.dev<YYYYMMDDHHmm>`, for example:

```
SAM CLI, version 1.20.0.dev202103151200
```

------

### macOS<a name="manage-sam-cli-versions-nightly-build-macos"></a>

To install the nightly build version of the AWS SAM CLI on macOS, using Homebrew, run the following commands:

```
brew tap aws/tap
brew install aws-sam-cli-nightly
```

To verify that you have installed the nightly build version, run the sam\-nightly \-\-version command\. The output of this command is in the form `1.X.Y.dev<YYYYMMDDHHmm>`, for example:

```
SAM CLI, version 1.20.0.dev202103151200
```

### Windows<a name="manage-sam-cli-versions-nightly-build-windows"></a>

The nightly build version of the AWS SAM CLI is available with this download link: [AWS SAM CLI nightly build](https://github.com/aws/aws-sam-cli/releases/download/sam-cli-nightly/AWS_SAM_CLI_64_PY3.msi)\. To install the nightly build on Windows, perform the same steps as in the [Installing the AWS SAM CLI](install-sam-cli.md), but use the nightly build download link instead\.

To verify that you have installed the nightly build version, run the sam\-nightly \-\-version command\. The output of this command is in the form `1.X.Y.dev<YYYYMMDDHHmm>`, for example:

```
SAM CLI, version 1.20.0.dev202103151200
```

## Installing the AWS SAM CLI into a virtual environment using pip<a name="manage-sam-cli-versions-install-virtual"></a>

We recommend using the native package installer to install the AWS SAM CLI\. If you must use pip, we recommend that you install the AWS SAM CLI into a virtual environment\. This ensures a clean installation environment and an isolated environment if errors occur\.

**To install the AWS SAM CLI into a virtual environment**

1. From a starting directory of your choice, create a virtual environment and name it\.

------
#### [ Linux / macOS ]

   ```
   $ mkdir project
   $ cd project
   $ python3 -m venv venv
   ```

------
#### [ Windows ]

   ```
   > mkdir project
   > cd project
   > py -3 -m venv venv
   ```

------

1. Activate the virtual environment

------
#### [ Linux / macOS ]

   ```
   $ . venv/bin/activate
   ```

   The prompt changes to show you that your virtual environment is active\.

   ```
   (venv) $ 
   ```

------
#### [ Windows ]

   ```
   > venv\Scripts\activate
   ```

   The prompt changes to show you that your virtual environment is active\.

   ```
   (venv) > 
   ```

------

1. Install the AWS SAM CLI into your virtual environment\.

   ```
   (venv) $ pip install --upgrade aws-sam-cli
   ```

1. Verify that the AWS SAM CLI is installed correctly\.

   ```
   (venv) $ sam --version
   SAM CLI, version 1.76.0
   ```

1. You can use the `deactivate` command to exit the virtual environment\. Whenever you start a new session, you must reactivate the environment\.

## Troubleshooting<a name="manage-sam-cli-versions-troubleshoot"></a>

If you come across errors when installing or using the AWS SAM CLI, see [AWS SAM CLI troubleshooting](sam-cli-troubleshooting.md)\.