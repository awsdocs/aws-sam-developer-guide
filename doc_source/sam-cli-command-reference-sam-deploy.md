# sam deploy<a name="sam-cli-command-reference-sam-deploy"></a>

Deploys an AWS SAM application\. This is an alias for [ `aws cloudformation deploy`](http://docs.aws.amazon.com/cli/latest/reference/cloudformation/deploy/index.html)\.

**Usage:**

```
sam deploy [OPTIONS] [ARGS]...
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-template\-file PATH | Required\. The path where your AWS SAM template file is located\. | 
| \-\-stack\-name TEXT | Required\. The name of the AWS CloudFormation stack you're deploying to\. If you specify an existing stack, the command updates the stack\. If you specify a new stack, the command creates it\. | 
| \-\-profile TEXT | Select a specific profile from your credential file to get AWS credentials\. | 
| \-\-region TEXT | Sets the AWS Region of the service \(for example, us\-east\-1\)\. | 
| \-\-debug | Turns on debug logging\. | 
| \-\-help | Shows this message and exits\. | 