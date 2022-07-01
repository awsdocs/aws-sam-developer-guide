# sam sync<a name="sam-cli-command-reference-sam-sync"></a>

The `sync` command deploys your local changes to the AWS Cloud\. Use `sync` to build, package, and deploy changes to your development environment as you iterate on your application\.

**Usage:**

```
sam sync [OPTIONS]
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-t, \-\-template\-file, \-\-template PATH | The path and file name where your AWS SAM template is located\.**Note:** If you specify this option, AWS SAM deploys only the template and the local resources that it points to\. | 
| \-\-code | By default, AWS SAM syncs all resources in your application\. Specify this option to sync only code resources\. Code resources include the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-sync.html) To sync code resources, AWS SAM uses AWS service APIs directly, instead of deploying through AWS CloudFormation\. Run sam sync \-\-watch or sam deploy to update your AWS CloudFormation stack\.  | 
| \-\-watch | Starts a process that watches your local application for changes and automatically syncs them to the AWS Cloud\. By default, when you specify this option, AWS SAM syncs all resources in your application as you update them\. When you provide this option, AWS SAM performs an initial AWS CloudFormation deployment\. Then, AWS SAM uses AWS service APIs to update code resources\. AWS SAM uses AWS CloudFormation to update infrastructure resources when you update your AWS SAM template\. | 
| \-\-resource\-id TEXT | Specifies the resource ID to sync\. You can specify this option multiple times to sync multiple resources\. Supported with the \-\-code option\. For example \-\-resource\-id Function1 \-\-resource\-id Function2\. | 
| \-\-resource TEXT | Specifies the resource type to sync\. You can specify this option multiple times to sync multiple resources\. Supported with the \-\-code option\. The value must be one of the listed resources under \-\-code\. For example \-\-resource AWS::Serverless::Function \-\-resouce AWS::Serverless::LayerVersion\. | 
| \-\-stack\-name TEXT | Required\. The AWS CloudFormation stack for your application\. | 
| \-\-s3\-bucket TEXT | The name of the Amazon S3 bucket where this command uploads your AWS CloudFormation template\. If your template is larger than 51,200 bytes, then either the \-\-s3\-bucket or the \-\-resolve\-s3 option is required\. If you specify both the \-\-s3\-bucket and \-\-resolve\-s3 options, then an error will result\. | 
| \-\-capabilities LIST | A list of capabilities that you specify to allow AWS CloudFormation to create certain stacks\. Some stack templates might include resources that can affect permissions in your AWS account, for example, by creating new AWS Identity and Access Management \(IAM\) users\. The default capabilities are CAPABILITY\_NAMED\_IAM and CAPABILITY\_AUTO\_EXPAND\. Specify this option to override the default values\. Valid values are: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-sync.html)  | 
| \-s, \-\-base\-dir DIRECTORY | Resolves relative paths to the function's or layer's source code with respect to this directory\. Use this option if you want to change how relative paths to source code folders are resolved\. By default, relative paths are resolved with respect to the AWS SAM template's location\.In addition to the resources in the root application or stack you are building, this option also applies nested applications or stacks\.This option applies to the following resource types and properties:[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-sync.html) | 
| \-\-parameter\-overrides | A string that contains AWS CloudFormation parameter overrides encoded as key\-value pairs\. Use the same format as the AWS Command Line Interface \(AWS CLI\)\. For example, ParameterKey=ParameterValue InstanceType=t1\.micro\. | 
| \-\-image\-repository TEXT | The name of the Amazon Elastic Container Registry \(Amazon ECR\) repository where this command uploads your function's image\. Required for functions declared with the Image package type\. | 
| \-\-s3\-prefix TEXT | Prefix added to the artifacts name that are uploaded to the Amazon S3 bucket\. The prefix name is a path name \(folder name\) for the Amazon S3 bucket\. This only applies for functions declared with Zip package type\. | 
| \-\-kms\-key\-id TEXT | The ID of an AWS Key Management Service \(AWS KMS\) key used to encrypt artifacts that are at rest in the Amazon S3 bucket\. If this option is not specified, then AWS SAM uses Amazon S3\-managed encryption keys\. | 
| \-\-role\-arn TEXT | The Amazon Resource Name \(ARN\) of an IAM role that AWS CloudFormation assumes when executing the changeset\. | 
| \-\-notification\-arns LIST | A list of Amazon Simple Notification Service \(Amazon SNS\) topic ARNs that AWS CloudFormation associates with the stack\. | 
| \-\-tags LIST | A list of tags to associate with the stack that is created or updated\. AWS CloudFormation also propagates these tags to resources in the stack that support it\. | 
| \-\-metadata | A map of metadata to attach to all artifacts that are referenced in your template\. | 

## Examples<a name="accelerate-sync-examples"></a>

Run the following command to start a process that automatically deploy changes from your local environment to your development environment in the AWS Cloud\.

```
sam sync --stack-name sam-app --watch
```

Run the following command to deploy code changes to a specific Lambda function and Lambda layer\. AWS SAM uses Lambda APIs to update your code in the AWS Cloud\.

```
sam sync --stack-name sam-app --code --resource-id HelloWorldFunction --resource-id HelloWorldLayer
```

Run the following command to deploy your latest local changes to your application's AWS CloudFormation stack\.

```
sam sync --stack-name sam-app
```

## Nested stack example<a name="accelerate-nested-stack-example"></a>

**Note**  
We currently only support referencing a stack using the following two methods: `!Ref LayerName` or `!GetAttr Stack.Output.LayerName`\.

AWS SAM Accelerate now supports nested stacks\. To sync a resource from a child stack, continue providing the root stack for the `--stack-name` parameter\. For the `--resource-id` parameter, specify the child stack and resource in the following format `ChildStack/resourceId`\. Additional child stacks can be defined by subsequent delineation of the stack name with a `/`\. For more information about creating nested applications, see [Using nested applications](serverless-sam-template-nested-applications.md)

```
sam sync --code --stack-name sam-app --resource-id mystack/HelloWorldFunction
```