# AWS SAM CLI configuration file<a name="serverless-sam-cli-config"></a>

The AWS SAM CLI supports a project\-level configuration file that stores default parameters for its commands\. This configuration file is in the [TOML file format](https://toml.io/en/)\. The default file name is `samconfig.toml`, and the file's default location is your project's root directory, which is the directory that contains your project's AWS SAM template file\.

You can manually edit this file to set default parameters for any AWS SAM CLI command\.

In addition, the `sam deploy --guided` command writes a subset of parameters to your configuration file\. For more details about this functionality, see [Writing configurations with `sam deploy --guided`](#deploy-guided) later in this topic\.

## Example<a name="example"></a>

Here is an example configuration file that contains seven parameters for the `default` environment and the `deploy` command:

```
 
 version=0.1
 [default.deploy.parameters]
 stack_name = "my-app-stack"
 s3_bucket = "my-source-bucket"
 s3_prefix = "my-s3-prefix"
 region = "us-west-2"
 confirm_changeset = true
 capabilities = "CAPABILITY_IAM"
 tags = "project=\"my-application\" stage=\"production\""
```

## Configuration file rules<a name="rules"></a>

The configuration file is in the [TOML file format](https://toml.io/en/)\. The AWS SAM CLI applies the following rules to configuration files:

### File name and location<a name="rules-name-location"></a>
+ The default configuration file is named `samconfig.toml` and is located in your project's root directory\.
+ You can override the default file name and location using the `--config-file` parameter\.

### Tables<a name="rules-tables"></a>
+ The AWS SAM CLI uses TOML tables to group configuration entries by environment and command\.
+ The format of the table header is `[environment.command.parameters]`\. For example, for the `sam deploy` command, the configuration table header is `[default.deploy.parameters]`\.
+ For subcommands, the format of the table header is `[environment.command_subcommand.parameters]`\. For example, for the `sam local invoke` command, the configuration table header is `[default.local_invoke.parameters]`\.
+ The default environment name is `default`\. You can override the default environment name using the `--config-env` parameter\.
+ A single configuration file can contain tables for multiple environments and multiple commands/subcommands\.

### Configuration entries<a name="rules-entries"></a>
+ Each configuration entry is a TOML key\-value pair\.
+ The configuration key is the long\-form parameter name with the `-` \(hyphen\) character replaced with `_` \(underscore\)\. For the list of available parameters for each command, see the [AWS SAM CLI command reference](serverless-sam-cli-command-reference.md), or run `sam command --help`\.
+ The configuration value can take the following forms:

  1. For parameters that take an argument, the entry value is the argument surrounded by double quotes\. For example, `region = "us-west-2"`\.

  1. For parameters that take key\-value pairs, the pairs are space\-delimited and value of each pair is surrounded by encoded double quotes\. For example, `tags = "project=\"my-application\" stage=\"production\""`\.

  1. For toggle parameters, the value can be `true` or `false` \(no quotes\)\. For example, `confirm_changeset = true`\.

### Precedence<a name="rules-precedence"></a>
+ Parameter values that you provide on the command line take precedence over corresponding entries in the configuration file\. For example, if your configuration file contains the entry `stack_name = "DefaultStack"` and you run the command `sam deploy --stack-name MyCustomStack`, then the deployed stack name is `MyCustomStack`\.
+ For the `parameter_overrides` entry, both the parameter values that you provide on the command line and entries in the configuration file take precedence over corresponding objects declared in the `Parameters` section of the template file\.

## Writing configurations with `sam deploy --guided`<a name="deploy-guided"></a>

When you run the `sam deploy --guided` command, the AWS SAM CLI guides you through the deployment with a series of prompts\.

These prompts include the question `"Save arguments to samconfig.toml [Y/n]:"`\. If you respond `Y` to this prompt, the AWS SAM CLI updates the configuration file with values for the following parameters:
+ `stack_name`
+ `s3_bucket`
+ `s3_prefix`
+ `region`
+ `config_changeset`
+ `capabilities`
+ `parameter_overrides`

If you've previously written a configuration file, the AWS SAM CLI reads it and uses those parameter values as the default values for the corresponding prompts\. If you specify values on the command line for any of these parameters, the AWS SAM CLI uses those values as the default values\.

To set any parameter other than those previously listed, you must manually edit the configuration file\.