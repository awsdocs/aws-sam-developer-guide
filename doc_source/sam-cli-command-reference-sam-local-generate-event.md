# sam local generate\-event<a name="sam-cli-command-reference-sam-local-generate-event"></a>

Generates sample payloads from different event sources, such as Amazon S3, Amazon API Gateway, and Amazon SNS\. These payloads contain the information that the event sources send to your Lambda functions\.

**Usage:**

```
sam local generate-event [OPTIONS] COMMAND [ARGS]...
```

**Examples:**

```
Generate the event that S3 sends to your Lambda function when a new object is uploaded
sam local generate-event s3 [put/delete]

# You can even customize the event by adding parameter flags. To find which flags apply to your command,
run:

sam local generate-event s3 [put/delete] --help

# Then you can add in those flags that you wish to customize using

sam local generate-event s3 [put/delete] --bucket <bucket> --key <key>

# After you generate a sample event, you can use it to test your Lambda function locally
sam local generate-event s3 [put/delete] --bucket <bucket> --key <key> | sam local invoke -e - <function logical id>
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-config\-file PATH | The path and file name of the configuration file containing default parameter values to use\. The default value is "samconfig\.toml" in the root of the project directory\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-config\-env TEXT | The environment name specifying the default parameter values in the configuration file to use\. The default value is "default"\. For more information about configuration files, see [AWS SAM CLI configuration file](serverless-sam-cli-config.md)\. | 
| \-\-help | Shows this message and exits\. | 

**Commands:**
+ `alexa-skills-kit`
+ `alexa-smart-home`
+ `apigateway`
+ `batch`
+ `cloudformation`
+ `cloudfront`
+ `cloudwatch`
+ `codecommit`
+ `codepipeline`
+ `cognito`
+ `config`
+ `dynamodb`
+ `kinesis`
+ `lex`
+ `rekognition`
+ `s3`
+ `ses`
+ `sns`
+ `sqs`
+ `stepfunctions`