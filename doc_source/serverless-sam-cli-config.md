# AWS SAM CLI configuration file<a name="serverless-sam-cli-config"></a>

The AWS SAM CLI supports a project\-level configuration file that stores default parameters for its commands\. This configuration file is in the [TOML file format](https://toml.io/en/), and the default file name is `samconfig.toml`\. The file's default location is your project's root directory, which contains your project's AWS SAM template file\.

You can manually edit this file to set default parameters for any AWS SAM CLI command\. In addition, the `sam deploy --guided` command writes a subset of parameters to your configuration file\. For more information about this command, see [Writing configurations with `sam deploy --guided`](#deploy-guided) later in this topic\.

## Example<a name="example"></a>

Here's an example configuration file that contains three sets of parameters for the `default` environment\. One set is for all commands, one is for the `deploy` command, and one is for the `build` command\.

```
 version=0.1
 [default.global.parameters]
 stack_name = "common-stack"
 
 [default.deploy.parameters]
 stack_name = "my-app-stack"
 s3_bucket = "my-source-bucket"
 s3_prefix = "my-s3-prefix"
 image_repositories = ["my-function-1=image-repo-1", "my-function-2=image-repo-2"]
 region = "us-west-2"
 confirm_changeset = true
 capabilities = "CAPABILITY_IAM"
 tags = "project=\"my-application\" stage=\"production\""

 [default.build.parameters]
 container_env_var = ["Function1.GITHUB_TOKEN=TOKEN1", "Function2.GITHUB_TOKEN=TOKEN2"]
 container_env_var_file = "env.json"
 no_beta_features = true
```

## Configuration file rules<a name="rules"></a>

The AWS SAM CLI applies the following rules to configuration files:

### File name and location<a name="rules-name-location"></a>
+ The default configuration file is named `samconfig.toml` and is located in your project's root directory\.
+ You can override the default file name and location using the `--config-file` parameter\.

### Tables<a name="rules-tables"></a>
+ The AWS SAM CLI uses TOML tables to group configuration entries by environment and command\. A single configuration file can contain tables for multiple environments, commands, and subcommands\.
+ The default environment name is named `default`\. You can override the default environment name using the `--config-env` parameter\.
+ For commands, the format of the table header is `[environment.command.parameters]`\. For example, for the `sam deploy` command for the `default` environment, the configuration table header is `[default.deploy.parameters]`\.
+ For subcommands, the format of the table header is `[environment.command_subcommand.parameters]`\. That is, delimit the command and subcommand with `_` \(underscore\)\. For example, for the `sam local invoke` command for the `default` environment, the configuration table header is `[default.local_invoke.parameters]`\.
+ If any command or subcommand contains a `-` \(hyphen\) character, replace it with `_` \(underscore\)\. For example, for the `sam local start-api` command, the configuration table header is `[default.local_start_api.parameters]`\.
+ To specify parameters for all commands, use the `global` keyword as the command in the table header \(`[environment.global.parameters]`\)\. For example, the global table header for the `default` environment is `[default.global.parameters]`\.

### Configuration entries<a name="rules-entries"></a>
+ Each configuration entry is a TOML key\-value pair\.
+ The configuration key is the long\-form parameter name with the `-` \(hyphen\) character replaced with `_` \(underscore\)\. For the list of available parameters for each command, see the [AWS SAM CLI command reference](serverless-sam-cli-command-reference.md), or run `sam command --help`\.
+ The configuration value can take the following forms:
  + For toggle parameters, the value can be `true` or `false` \(no quotation marks\)\. For example, `confirm_changeset = true`\.
  + For parameters that take a single argument, the value is the argument surrounded by `" "` \(quotation marks\)\. For example, `region = "us-west-2"`\.
  + For parameters that take a list of arguments, the arguments are space\-delimited within `" "` \(quotation marks\)\. For example, `capabilities = "CAPABILITY_IAM CAPABILITY_NAMED_IAM"`\.
    + To specify a list of key\-value pairs, the pairs are space\-delimited, and the value of each pair is surrounded by encoded `" "` \(quotation marks\)\. For example, `tags = "project=\"my-application\" stage=\"production\""`\.
  + For parameters that you can specify multiple times, the value is an array of arguments\. For example, `image_repositories = ["my-function-1=image-repo-1", "my-function-2=image-repo-2"]`\.

### Precedence<a name="rules-precedence"></a>
+ Parameter values that you provide on the command line take precedence over corresponding entries in the configuration file\. For example, if your configuration file contains the entry `stack_name = "DefaultStack"` and you run the command `sam deploy --stack-name MyCustomStack`, then the deployed stack name is `MyCustomStack`\.
+ For the `parameter_overrides` entry, both the parameter values that you provide on the command line and entries in the configuration file take precedence over corresponding objects declared in the `Parameters` section of the template file\.
+ Entries that you provide in a specific command table take precedence over entries in a `global` command section\. For example, suppose that your configuration file contains the following tables and entries:

  ```
   [default.global.parameters]
   stack_name = "common-stack"
  
   [default.deploy.parameters]
   stack_name = "my-app-stack"
  ```

  In this case, the `sam deploy` command uses the stack name `my-app-stack`, and any other command \(for example, `sam logs`\) uses the stack name `common-stack`\.

## Writing configurations with `sam deploy --guided`<a name="deploy-guided"></a>

When you run the `sam deploy --guided` command, the AWS SAM CLI guides you through the deployment with a series of prompts\.

These prompts include the question `"Save arguments to samconfig.toml [Y/n]:"`\. If you respond **Y** to this prompt, the AWS SAM CLI updates the configuration file with values for the `deploy` command\. For example, for the `default` environment, AWS SAM updates the `[default.deploy.parameters]` table\.

The list of entries in the `deploy` command table that AWS SAM can update include the following:
+ `stack_name`
+ `s3_bucket`
+ `s3_prefix`
+ `image_repository`
+ `region`
+ `confirm_changeset`
+ `capabilities`
+ `signing_profiles`
+ `disable_rollback`
+ `parameter_overrides`
**Note**  
There's a special case for a configuration file that contains entries for the same parameter in both the `deploy` and `global` command tables\. In this case, if you run `sam deploy --guided` and provide the same value for that parameter as the `global` command table entry, then the `deploy` command table entry is removed\.  
By specifying at the `sam deploy --guided` prompt the same value that's already specified in the `global` command table, AWS SAM assumes that you want to default to the value in the `global` command table\.

### Rules for guided prompt default values<a name="deploy-guided-rules"></a>

To control the default values for the prompts that the AWS SAM CLI displays when you run `sam deploy --guided`, you can specify parameters on the command line, or entries in an existing configuration file\.

The rules for these prompts are as follows:
+ If you specify values on the command line, the AWS SAM CLI uses those command line values as the defaults for the corresponding prompts\.
+ If there's an existing configuration file, the AWS SAM CLI uses entries from the matching table in that file as the default values for the corresponding prompts\.

The precedence rules between the command line and configuration file are the same as stated in the **Precedence** section earlier in this topic\.