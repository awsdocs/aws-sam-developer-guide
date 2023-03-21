# Installing the AWS SAM CLI<a name="install-sam-cli"></a>

Install the latest release of the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) on supported operating systems\.

To learn how to manage a currently installed version of the AWS SAM CLI, including how to upgrade, uninstall, or manage nightly builds, see [Managing AWS SAM CLI versions](manage-sam-cli-versions.md)\.

**Is this your first time installing the AWS SAM CLI?**  
Complete all [prerequisites](prerequisites.md) in the previous section before moving forward\. This includes:  
Signing up for an AWS account\.
Creating an administrative IAM user\.
Creating an access key ID and secret access key\.
Installing the AWS CLI\.
Configuring AWS credentials\.

**Topics**
+ [Installing the AWS SAM CLI](#install-sam-cli-instructions)
+ [Troubleshooting](#install-sam-cli-troubleshooting)
+ [Next steps](#install-sam-cli-next-steps)

## Installing the AWS SAM CLI<a name="install-sam-cli-instructions"></a>

 To install the AWS SAM CLI, follow the instructions for your operating system\. 

### Linux<a name="install-sam-cli-instructions-linux"></a>

------
#### [ x86\_64 \- command line installer ]

1. Download the [AWS SAM CLI \.zip file](https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-linux-x86_64.zip) to a directory of your choice\.

1. Verify the integrity and authenticity of the downloaded installer files by generating a hash value using the following command:

   ```
   $ sha256sum aws-sam-cli-linux-x86_64.zip
   ```

   The output should look like the following example:

   ```
    <64-character SHA256 hash value> aws-sam-cli-linux-x86_64.zip
   ```

   Compare the 64\-character SHA\-256 hash value with the one for your desired AWS SAM CLI version in the [AWS SAM CLI release notes](https://github.com/aws/aws-sam-cli/releases/latest) on GitHub\.

1. Unzip the installation files into the `sam-installation/` subdirectory\.
**Note**  
If your operating system doesn't have the built\-in unzip command, use an equivalent\.

   ```
   $ unzip aws-sam-cli-linux-x86_64.zip -d sam-installation
   ```

1. Install the AWS SAM CLI\.

   ```
   $ sudo ./sam-installation/install
   ```

1. Verify the installation\.

   ```
   $ sam --version
   ```

   On successful installation, you should see output like the following:

   ```
    SAM CLI, version 1.58.0
   ```

------
#### [ ARM \- command line installer ]

**Note**  
We recommend installing the AWS SAM CLI into a virtual environment to ensure a clean starting environment and an isolated environment when troubleshooting\. For more information, see [Installing the AWS SAM CLI into a virtual environment using pip](manage-sam-cli-versions.md#manage-sam-cli-versions-install-virtual)\.

1. Use `pip` to install the AWS SAM CLI\.

   ```
   $ pip install aws-sam-cli
   ```

1. Verify the installation\.

   ```
   $ sam --version
   ```

   On successful installation, you should see output like the following:

   ```
    SAM CLI, version 1.58.0
   ```

------
#### [ Homebrew ]

**Important**  
You must have Homebrew installed on your Linux machine\. For install instructions, see [Installing Homebrew to use with the AWS SAM CLI](install-homebrew.md)\.

To install the AWS SAM CLI using Homebrew, run the following command:

```
$ brew install aws/tap/aws-sam-cli
```

Verify the installation\.

```
$ sam --version
```

On successful installation of the AWS SAM CLI, you should see output like the following:

```
SAM CLI, version 1.58.0
```

------

### macOS<a name="install-sam-cli-instructions-macos"></a>

Install the AWS SAM CLI using its package installer or through Homebrew\. We recommend using the package installer\.

#### Using the package installer<a name="install-sam-cli-instructions-macos-package"></a>

The package installer has two installation methods that you can choose from:

1. GUI

1. Command line

You can install for all users or just your current user\. To install for all users, superuser authorization is required\.

#### Installation steps<a name="install-sam-cli-instructions-macos-steps"></a>

 Install the AWS SAM CLI using any of the following options\. 

------
#### [ GUI \- All users ]

**Download the package installer**
**Note**  
 If you previously installed the AWS SAM CLI through Homebrew or pip, you need to uninstall it first\. For instructions, see [Uninstalling the AWS SAM CLI](manage-sam-cli-versions.md#manage-sam-cli-versions-uninstall)\. 

1.  To begin installation, download the macOS `pkg` to a directory of your choice: 
   +  x86\_64 \(Intel\) – [ aws\-sam\-cli\-macos\-x86\_64\.pkg](https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-macos-x86_64.pkg) 
   +  arm64 \(Apple\) – [ aws\-sam\-cli\-macos\-arm64\.pkg](https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-macos-arm64.pkg) 

1.  Verify the integrity and authenticity of the downloaded installer by generating a hash value using the following command: 

   ```
   $ shasum -a 256 path-to-pkg-installer/name-of-pkg-installer
   
   # Examples
   $ shasum -a 256 /Users/myUser/Downloads/aws-sam-cli-macos-arm64.pkg
   $ shasum -a 256 /Users/myUser/Downloads/aws-sam-cli-macos-x86_64.pkg
   ```

    Compare your 64\-character SHA\-256 hash value with the corresponding value in the [AWS SAM CLI release notes](https://github.com/aws/aws-sam-cli/releases/latest) GitHub repository\. 

**Install the AWS SAM CLI**

1.  Run your downloaded file and follow the on\-screen instructions to continue through the **Introduction**, **Read Me**, and **License** steps\. 

1.  For **Destination Select**, select **Install for all users of this computer**\. 

1.  For **Installation Type**, choose where the AWS SAM CLI will be installed and press **Install**\. The recommended default location is `/usr/local/aws-sam-cli`\. 
**Note**  
 To invoke the AWS SAM CLI with the sam command, the installer automatically creates a symlink between `/usr/local/bin/sam` and either `/usr/local/aws-sam-cli/sam` or the installation folder you chose\. 

1.  The AWS SAM CLI will install and **The installation was successful** message will display\. Press **Close**\. 

**Verify the install**
+  Verify that the AWS SAM CLI has properly installed and that your symlink is configured by running: 

  ```
  $ which sam
  /usr/local/bin/sam
  $ sam --version
  SAM CLI, version 1.66.0
  ```

------
#### [ GUI \- Current user ]

**Download the package installer**
**Note**  
 If you previously installed the AWS SAM CLI through Homebrew or pip, you need to uninstall it first\. For instructions, see [Uninstalling the AWS SAM CLI](manage-sam-cli-versions.md#manage-sam-cli-versions-uninstall)\. 

1.  To begin installation, download the macOS `pkg` to a directory of your choice: 
   +  x86\_64 \(Intel\) – [ aws\-sam\-cli\-macos\-x86\_64\.pkg](https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-macos-x86_64.pkg) 
   +  arm64 \(Apple\) – [ aws\-sam\-cli\-macos\-arm64\.pkg](https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-macos-arm64.pkg) 

1.  Verify the integrity and authenticity of the downloaded installer by generating a hash value using the following command: 

   ```
   $ shasum -a 256 path-to-pkg-installer/name-of-pkg-installer
   
   # Examples
   $ shasum -a 256 /Users/myUser/Downloads/aws-sam-cli-macos-arm64.pkg
   $ shasum -a 256 /Users/myUser/Downloads/aws-sam-cli-macos-x86_64.pkg
   ```

    Compare your 64\-character SHA\-256 hash value with the corresponding value in the [AWS SAM CLI release notes](https://github.com/aws/aws-sam-cli/releases/latest) GitHub repository\. 

**Install the AWS SAM CLI**

1.  Run your downloaded file and follow the on\-screen instructions to continue through the **Introduction**, **Read Me**, and **License** steps\. 

1.  For **Destination Select**, select **Install for me only**\. If you don't see this option, go to the next step\. 

1.  For **Installation Type**, do the following: 

   1. Choose where the AWS SAM CLI will be installed\. The default location is `/usr/local/aws-sam-cli`\. Select a location that you have write permissions for\. To change the installation location, select **local** and choose your location\. Press **Continue** when done\. 

   1.  If you didn't get the option to choose **Install for me only** in the previous step, select **Change Install Location** > **Install for me only** and press **Continue**\. 

   1.  Press **Install**\. 

1.  The AWS SAM CLI will install and **The installation was successful** message will display\. Press **Close**\. 

**Create a symlink**
+  To invoke the AWS SAM CLI with the sam command, you must manually create a symlink between the AWS SAM CLI program and your `$PATH`\. Create your symlink by modifying and running the following command: 

  ```
  $ sudo ln -s /path-to/aws-sam-cli/sam /path-to-symlink-directory/sam
  ```
  +  *sudo* – If your user has write permissions to `$PATH`, sudo is not required\. Otherwise, sudo is required\. 
  +  *path\-to* – Path to where you installed the AWS SAM CLI program\. For example, `/Users/myUser/Desktop`\. 
  +  *path\-to\-symlink\-directory* – Your `$PATH` environment variable\. The default location is `/usr/local/bin`\. 

**Verify the install**
+  Verify that the AWS SAM CLI has properly installed and that your symlink is configured by running: 

  ```
  $ which sam
  /usr/local/bin/sam
  $ sam --version
  SAM CLI, version 1.66.0
  ```

------
#### [ Command line \- All users ]

**Download the package installer**
**Note**  
 If you previously installed the AWS SAM CLI through Homebrew or pip, you need to uninstall it first\. For instructions, see [Uninstalling the AWS SAM CLI](manage-sam-cli-versions.md#manage-sam-cli-versions-uninstall)\. 

1.  To begin installation, download the macOS `pkg` to a directory of your choice: 
   +  x86\_64 \(Intel\) – [ aws\-sam\-cli\-macos\-x86\_64\.pkg](https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-macos-x86_64.pkg) 
   +  arm64 \(Apple\) – [ aws\-sam\-cli\-macos\-arm64\.pkg](https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-macos-arm64.pkg) 

1.  Verify the integrity and authenticity of the downloaded installer by generating a hash value using the following command: 

   ```
   $ shasum -a 256 path-to-pkg-installer/name-of-pkg-installer
   
   # Examples
   $ shasum -a 256 /Users/myUser/Downloads/aws-sam-cli-macos-arm64.pkg
   $ shasum -a 256 /Users/myUser/Downloads/aws-sam-cli-macos-x86_64.pkg
   ```

    Compare your 64\-character SHA\-256 hash value with the corresponding value in the [AWS SAM CLI release notes](https://github.com/aws/aws-sam-cli/releases/latest) GitHub repository\. 

**Install the AWS SAM CLI**
+  Modify and run the installation script: 

  ```
  $ sudo installer -pkg path-to-pkg-installer/name-of-pkg-installer -target /
  installer: Package name is AWS SAM CLI
  installer: Upgrading at base path /
  installer: The upgrade was successful.
  ```
**Note**  
 To invoke the AWS SAM CLI with the sam command, the installer automatically creates a symlink between `/usr/local/bin/sam` and `/usr/local/aws-sam-cli/sam`\. 

**Verify the install**
+  Verify that the AWS SAM CLI has properly installed and that your symlink is configured by running: 

  ```
  $ which sam
  /usr/local/bin/sam
  $ sam --version
  SAM CLI, version 1.66.0
  ```

------
#### [ Command line \- Current user ]

**Download the package installer**
**Note**  
 If you previously installed the AWS SAM CLI through Homebrew or pip, you need to uninstall it first\. For instructions, see [Uninstalling the AWS SAM CLI](manage-sam-cli-versions.md#manage-sam-cli-versions-uninstall)\. 

1.  To begin installation, download the macOS `pkg` to a directory of your choice: 
   +  x86\_64 – [ aws\-sam\-cli\-macos\-x86\_64\.pkg](https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-macos-x86_64.pkg) 
   +  arm64 – [ aws\-sam\-cli\-macos\-arm64\.pkg](https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-macos-arm64.pkg) 

1.  Verify the integrity and authenticity of the downloaded installer by generating a hash value using the following command: 

   ```
   $ shasum -a 256 path-to-pkg-installer/name-of-pkg-installer
   
   # Examples
   $ shasum -a 256 /Users/myUser/Downloads/aws-sam-cli-macos-arm64.pkg
   $ shasum -a 256 /Users/myUser/Downloads/aws-sam-cli-macos-x86_64.pkg
   ```

    Compare your 64\-character SHA\-256 hash value with the corresponding value in the [AWS SAM CLI release notes](https://github.com/aws/aws-sam-cli/releases/latest) GitHub repository\. 

**Install the AWS SAM CLI**

1.  Determine an installation directory that you have write permissions to\. Then, create an `xml` file using the template and modify it to reflect your installation directory\. The directory must already exist\. 

    For example, if you replace *path\-to\-my\-directory* with `/Users/myUser/Desktop`, the `aws-sam-cli` program folder will be installed there\. 

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
   <plist version="1.0">
     <array>
       <dict>
         <key>choiceAttribute</key>
         <string>customLocation</string>
         <key>attributeSetting</key>
         <string>path-to-my-directory</string>
         <key>choiceIdentifier</key>
         <string>default</string>
       </dict>
     </array>
   </plist>
   ```

1.  Save the `xml` file and verify that its valid by running the following: 

   ```
   $ installer -pkg path-to-pkg-installer \
   -target CurrentUserHomeDirectory \
   -showChoicesAfterApplyingChangesXML path-to-your-xml-file
   ```

    The output should display the preferences that will be applied to the AWS SAM CLI program\. 

1.  Run the following to install the AWS SAM CLI: 

   ```
   $ installer -pkg path-to-pkg-installer \
   -target CurrentUserHomeDirectory \
   -applyChoiceChangesXML path-to-your-xml-file
   
   # Example output
   installer: Package name is AWS SAM CLI
   installer: choices changes file 'path-to-your-xml-file' applied
   installer: Upgrading at base path base-path-of-xml-file
   installer: The upgrade was successful.
   ```

**Create a symlink**
+  To invoke the AWS SAM CLI with the sam command, you must manually create a symlink between the AWS SAM CLI program and your `$PATH`\. Create your symlink by modifying and running the following command: 

  ```
  $ sudo ln -s /path-to/aws-sam-cli/sam /path-to-symlink-directory/sam
  ```
  +  *sudo* – If your user has write permissions to `$PATH`, sudo is not required\. Otherwise, sudo is required\. 
  +  *path\-to* – Path to where you installed the AWS SAM CLI program\. For example, `/Users/myUser/Desktop`\. 
  +  *path\-to\-symlink\-directory* – Your `$PATH` environment variable\. The default location is `/usr/local/bin`\. 

**Verify the install**
+  Verify that the AWS SAM CLI has properly installed and that your symlink is configured by running: 

  ```
  $ which sam
  /usr/local/bin/sam
  $ sam --version
  SAM CLI, version 1.66.0
  ```

------
#### [ Homebrew ]

**Important**  
You must have Homebrew installed on your machine\. For install instructions, see [Installing Homebrew to use with the AWS SAM CLI](install-homebrew.md)\.

Follow these steps to install the AWS SAM CLI using Homebrew:

```
$ brew install aws/tap/aws-sam-cli
```

Verify the installation:

```
$ sam --version
```

After successful installation of the AWS SAM CLI, you should see output like the following:

```
SAM CLI, version 1.58.0
```

------

### Windows<a name="install-sam-cli-instructions-windows"></a>

Windows Installer \(MSI\) files are the package installer files for the Windows operating system\.

Follow these steps to install the AWS SAM CLI using the MSI file\.

1. Install the AWS SAM CLI [64\-bit](https://github.com/aws/aws-sam-cli/releases/latest/download/AWS_SAM_CLI_64_PY3.msi)\.
**Note**  
If you use a 32\-bit version of Windows, see [Installing AWS SAM CLI on 32\-bit Windows](important-notes.md#important-notes-32-bit-windows)\.

1. Verify the installation\.

   After completing the installation, verify it by opening a new command prompt or PowerShell prompt\. You should be able to invoke `sam` from the command line\.

   ```
   sam --version
   ```

   After successful installation of the AWS SAM CLI, you should see output like the following:

   ```
   SAM CLI, version 1.58.0
   ```

1. Enable long paths \(Windows 10 and newer only\)\.
**Important**  
The [AWS SAM CLI app templates repository](https://github.com/aws/aws-sam-cli-app-templates) contains some long file paths which may cause errors when running `sam init` due to Windows 10 MAX\_PATH limitations\. To resolve this issue, the new long paths behavior must be configured\.

   To enable long paths, see [Enable Long Paths in Windows 10, Version 1607, and Later](https://learn.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation?tabs=powershell#enable-long-paths-in-windows-10-version-1607-and-later) in the *Microsoft Windows App Development Documentation*\.

1. Install Git\.

   To download sample applications using the `sam init` command, you must also install Git\. For instructions, see [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)\.

## Troubleshooting<a name="install-sam-cli-troubleshooting"></a>

If you come across issues while installing the AWS SAM CLI, see [Installation errors](sam-cli-troubleshooting.md#sam-cli-troubleshoot-install)\.

## Next steps<a name="install-sam-cli-next-steps"></a>

To learn more about the AWS SAM CLI and to begin building your own serverless applications, see the following:
+ [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md) – Step\-by\-step instructions to download, build, and deploy a basic serverless application\.
+ [The Complete AWS SAM Workshop](https://catalog.workshops.aws/complete-aws-sam/en-US) – A workshop designed to teach you many of the major features that AWS SAM provides\.
+ [AWS SAM example applications and patterns](https://serverlessland.com/patterns?framework=SAM) – Sample applications and patterns from community authors that you can further experiment with\.