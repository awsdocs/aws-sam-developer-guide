# Validating AWS SAM template files<a name="serverless-sam-cli-using-validate"></a>

Validate your templates with ``\. Currently, this command validates that the template provided is valid JSON / YAML\. As with most AWS SAM CLI commands, it looks for a `template.[yaml|yml]` file in your current working directory by default\. You can specify a different template file/location with the `-t` or `--template` option\.

Example:

```
sam validate
<path-to-file>/template.yml is a valid SAM Template
```

**Note**  
The `sam validate` command requires AWS credentials to be configured\. For more information, see [Configuration and Credential Files](https://docs.aws.amazon.com/cli/latest/userguide/cli-config-files.html)\.