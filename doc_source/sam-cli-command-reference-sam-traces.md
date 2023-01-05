# sam traces<a name="sam-cli-command-reference-sam-traces"></a>

Fetches AWS X\-Ray traces in your AWS account in the AWS Region\.

**Usage:**

```
sam traces [OPTIONS]
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
| \-\-trace\-id TEXT | The unique identifier for an X\-Ray trace\. | 
| \-\-start\-time TEXT |  Fetches traces starting at this time\. The time can be relative values like '5mins ago', 'yesterday', or a formatted timestamp like '2018\-01\-01 10:10:10'\. It defaults to '10mins ago'\.  | 
| \-\-end\-time TEXT |  Fetches traces up to this time\. The time can be relative values like '5mins ago', 'tomorrow', or a formatted timestamp like '2018\-01\-01 10:10:10'\.  | 
| \-\-tail | Tails the trace output\. This ignores the end time argument and continues to display traces as they become available\. | 
| \-\-output TEXT | Specifies the output format for logs\. To print formatted logs, specify `text`\. To print the logs as JSON, specify `json`\. | 

## Examples<a name="accelerate-traces-examples"></a>

Run the following command to fetch X\-Ray traces by ID\.

```
sam traces --trace-id tracing-id-1 --trace-id tracing-id-2
```

Run the following command to tail X\-Ray traces as they become available\.

```
sam traces --tail
```