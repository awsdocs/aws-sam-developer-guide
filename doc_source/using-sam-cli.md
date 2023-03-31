# Using the AWS SAM CLI<a name="using-sam-cli"></a>

Use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) with AWS SAM templates and supported third\-party integrations to build and run your serverless applications\.

For an introduction to AWS SAM, see [What is AWS SAM?](what-is-sam.md)

**Topics**
+ [How AWS SAM CLI commands are documented](#using-sam-cli-documentation)
+ [Configuring the AWS SAM CLI](using-sam-cli-configure.md)
+ [Using sam build](using-sam-cli-build.md)
+ [Using sam init](using-sam-cli-init.md)
+ [Using sam sync](using-sam-cli-sync.md)

## How AWS SAM CLI commands are documented<a name="using-sam-cli-documentation"></a>

AWS SAM CLI commands are documented using the following format:
+ **Prompt** – The Linux prompt is documented by default and is displayed as \(`$ `\)\. For commands that are Windows specific, \(`> `\) is used as the prompt\. Do not include the prompt when you type commands\.
+ **Directory** – When commands must be executed from a specific directory, the directory name is shown before the prompt symbol\.
+ **User input** – Command text that you enter at the command line is formatted as **user input**\.
+ **Replaceable text** – Variable text, such as file names and parameters are formatted as *replaceable text*\. In multiple\-line commands or commands where specific keyboard input is required, keyboard input can also be shown as replaceable text\. For example, *ENTER*\.
+ **Output** – Output returned as a response to the command is formatted as `computer output`\.

The following `sam deploy` command and output is an example:

```
$ sam deploy --guided --template template.yaml

Configuring SAM deploy
======================

    Looking for config file [samconfig.toml] :  Found
    Reading default arguments  :  Success

    Setting default arguments for 'sam deploy'
    =========================================
    Stack Name [sam-app]: ENTER
    AWS Region [us-west-2]: ENTER
    #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
    Confirm changes before deploy [y/N]: ENTER
    #SAM needs permission to be able to create roles to connect to the resources in your template
    Allow SAM CLI IAM role creation [Y/n]: ENTER
    #Preserves the state of previously provisioned resources when an operation fails
    Disable rollback [y/N]: ENTER
    HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
    Save arguments to configuration file [Y/n]: ENTER
    SAM configuration file [samconfig.toml]: ENTER
    SAM configuration environment [default]: ENTER
```

1. `sam deploy --guided --template template.yaml` is the command you enter at the command line\.

1. **sam deploy \-\-guided \-\-template** should be provided as is\.

1. *template\.yaml* can be replaced with your specific file name\.

1. The output starts at `Configuring SAM deploy`\.

1. In the output, *ENTER* and *y* indicate replaceable values that you provide\.