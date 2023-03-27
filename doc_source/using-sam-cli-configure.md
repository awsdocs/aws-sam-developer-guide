# Configuring the AWS SAM CLI<a name="using-sam-cli-configure"></a>

Configure credentials, basic settings, and project settings for the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\)\.

**Topics**
+ [Configure credentials and basic settings](#using-sam-cli-configure-basic)
+ [Configure project settings](#using-sam-cli-configure-project)
+ [Configure and use different environments](#using-sam-cli-configure-project-env)
+ [Configure and use parameter values](#using-sam-cli-configure-project-parameter)
+ [Using the AWS SAM CLI with configuration files](#using-sam-cli-configure-cli)

## Configure credentials and basic settings<a name="using-sam-cli-configure-basic"></a>

Use the AWS Command Line Interface \(AWS CLI\) to configure basic settings such as AWS credentials, default region name, and default output format\. Once configured, you can use these settings with the AWS SAM CLI\. To learn more, see the following from the *AWS Command Line Interface User Guide*:
+ [Configuration basics](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)
+ [Configuration and credential file settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)
+ [Named profiles for the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)
+ [Using an IAM Identity Center enabled named profile](https://docs.aws.amazon.com/cli/latest/userguide/sso-using-profile.html)

For quick setup instructions, see [Step 5: Use the AWS CLI to configure AWS credentials](prerequisites.md#prerequisites-configure-credentials)\.

## Configure project settings<a name="using-sam-cli-configure-project"></a>

You can specify project\-specific settings, such as parameter values, in a configuration file to use with the AWS SAM CLI\.
+ This configuration file is in the `TOML` file format\. To learn more, see [https://toml.io/en/](https://toml.io/en/) in the *TOML documentation*\.
+ The default configuration file name is `samconfig.toml`\.
+ The default configuration file location is your project’s root directory\. This is the same location as your AWS SAM template file\.

The following is an example of a `samconfig.toml` file:

```
...
version = 0.1

[default]
[default.global]
[default.global.parameters]
stack_name = "sam-app"

[default.build.parameters]
cached = true
parallel = true

[default.deploy.parameters]
capabilities = "CAPABILITY_IAM"
confirm_changeset = true
resolve_s3 = true

[default.sync.parameters]
watch = true

[default.local_start_api.parameters]
warm_containers = "EAGER"

[prod]
[prod.sync]
[prod.sync.parameters]
watch = false
```

## Configure and use different environments<a name="using-sam-cli-configure-project-env"></a>

An **environment** is a named identifier that you can use to specify a collection of project settings\.
+ The default environment is `[default]`\.
+ To create new environments, specify a new table header\. For example, `[prod]`\.
+ The environment name should always be the first entry in a table header\.
+ After an environment has been created in your `samconfig.toml` file, you can specify it using the `--config-env` option\. The following is an example:

  ```
  $ sam build --config-env "prod"
  ```

## Configure and use parameter values<a name="using-sam-cli-configure-project-parameter"></a>

You can specify parameter values for each AWS SAM CLI command\.
+ The second entry in a table header identifies the AWS SAM CLI command\. For example, `[default.build]` specifies default environment values for the `sam build` command\.
+ When an AWS SAM CLI command includes a subcommand, such as `sam local`, use the `_` \(underscore\)\. For example, `[environment.local_invoke]`\.
+ When an AWS SAM CLI command or subcommand contains a `-` \(hyphen\), replace it with `_` \(underscore\)\. For example, `sam local start-api` becomes `[environment.local_start_api]`\.
+ To specify parameter values for the AWS SAM CLI, add the parameter entry to the TOML table header\. For example, `[environment.command.parameters]`\.
+ To specify parameter values for all commands, use `global` in place of the command\. For example, `[environment.global.parameters]`\.

When specifying parameter values:
+ Each configuration entry is a TOML key\-value pair\. For example, in the `watch = false` configuration entry, `watch` is the key and `false` is the value\.
+ The configuration key is the long\-form option name of the AWS SAM CLI command\.
  + For a list of commands and options, see the [AWS SAM CLI command reference](serverless-sam-cli-command-reference.md)\.
  + For example, `sam sync --template-file project.yaml` can be specified as follows:

    ```
    [default.sync.parameters]
    template_file = "project.yaml"
    ```
+ The configuration value can take the following forms:
  + Boolean values can be `true` or `false`\. For example, `confirm_changeset = true`\.
  + For options that take a single parameter in the form of a string value, use `" "` \(quotation marks\)\. For example, `region = "us-west-2"`\.
  + For options that take a list of parameter values, use `" "` \(quotation marks\) and separate each value using a ` ` \(space\)\. For example, `capabilities = "CAPABILITY_IAM CAPABILITY_NAMED_IAM"`\.
  + When the value contains a list of key\-value pairs, the pairs are space\-delimited and the value of each pair is surrounded by encoded `" "` \(quotation marks\)\. For example, `tags = "project=\"my-application\" stage=\"production\""`\.
  + For parameters that you can specify multiple times, the value is an array of arguments\. For example, `image_repositories = ["my-function-1=image-repo-1", "my-function-2=image-repo-2"]`\.

When using configured values, the following precedence takes place:
+ Parameter values that you provide at the command line take precedence over corresponding values in the configuration file and `Parameters` section of the template file\.
+ If the `--parameter-overrides` option is used at the command line or in your configuration file with the `parameter_overrides` key, its values take precedence over values in the `Parameters` section of the template file\.
+ In your configuration file, entries provided for a specific command table take precedence over entries in a `[environment.global]` section\. The following is an example `samconfig.toml` file:

  ```
  [default.global.parameters]
  stack_name = "common-stack"
  
  [default.deploy.parameters]
  stack_name = "my-app-stack"
  ```

  The `sam deploy` command will use the stack name `my-app-stack`\. Any other command will use the stack name `common-stack`\.

## Using the AWS SAM CLI with configuration files<a name="using-sam-cli-configure-cli"></a>

Some commands, such as `sam deploy --guided`, provide an interactive flow that you can use to set configuration values\. The following is an example of the `sam deploy --guided` interactive flow:

```
sam-app $ sam deploy --guided

Configuring SAM deploy
======================

    Looking for config file [samconfig.toml] :  Found
    Reading default arguments  :  Success

    Setting default arguments for 'sam deploy'
    =========================================
    Stack Name [sam-app]: ENTER
    AWS Region [us-west-2]: ENTER
    #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
    Confirm changes before deploy [Y/n]: n
    #SAM needs permission to be able to create roles to connect to the resources in your template
    Allow SAM CLI IAM role creation [Y/n]: ENTER
    #Preserves the state of previously provisioned resources when an operation fails
    Disable rollback [y/N]: ENTER
    HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
    Save arguments to configuration file [Y/n]: ENTER
    SAM configuration file [samconfig.toml]: ENTER
    SAM configuration environment [default]: ENTER
```

During the interactive flow, values that already exist in any of your configuration files will display in `[ ]` \(brackets\)\. For new values that you provide during the interactive flow, the AWS SAM CLI writes those values to your configuration files\.

From this example, the AWS SAM CLI writes the following to your configuration file:

```
[default.deploy]
[default.deploy.parameters]
capabilities = "CAPABILITY_IAM"
confirm_changeset = true
resolve_s3 = true
s3_bucket = "aws-sam-cli-managed-default-samclisourcebucket-1a4x26zabcde"
s3_prefix = "sam-app"
region = "us-west-2"
```

When writing values to your configuration file, the AWS SAM CLI handles global values as follows:
+ If the parameter value entered exists in a global command table and a specific command table, such as `[environment.deploy.parameters]`, AWS SAM doesn’t write the value to the specific command table\.
+ If the parameter value entered exists in both the global command table and specific command table, AWS SAM deletes the key\-value pair from the specific command table\. Here, AWS SAM assumes that you want to override your specific command value with the global command value\.