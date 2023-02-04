# sam list<a name="sam-cli-command-reference-sam-list"></a>

Outputs important information about the resources in your serverless application and the state of your serverless application\. Use sam list before and after deployment to assist during local and cloud development\.

## Usage<a name="sam-cli-command-reference-sam-list-usage"></a>

```
sam list <option> <command> ...
```

## Options<a name="sam-cli-command-reference-sam-list-options"></a>


| Option | Description | 
| --- | --- | 
|  `-h`, `--help`  |  Show this message and exit\.  | 

## Commands<a name="sam-cli-command-reference-sam-list-commands"></a>


| Command | Description | 
| --- | --- | 
|  `endpoints`  |  Displays a list of cloud and local endpoints from your AWS CloudFormation stack\. For more information, see [sam list endpoints](sam-cli-command-reference-sam-list-endpoints.md)\.  | 
|  `resources`  |  Displays the resources in your AWS Serverless Application Model \(AWS SAM\) template that are created in AWS CloudFormation at deployment\. For more information, see [sam list resources](sam-cli-command-reference-sam-list-resources.md)\.  | 
|  `stack-outputs`  |  Displays the outputs of your AWS CloudFormation stack from an AWS SAM or AWS CloudFormation template\. For more information, see [sam list stack\-outputs](sam-cli-command-reference-sam-list-stack-outputs.md)\.  | 