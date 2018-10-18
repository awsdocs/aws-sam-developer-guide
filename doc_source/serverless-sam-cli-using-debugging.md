# Debugging Lambda Functions Locally<a name="serverless-sam-cli-using-debugging"></a>

The commands `sam local invoke` and `sam local start-api` both support local debugging of your functions\.

To run AWS SAM locally with debugging support enabled, specify `--debug-port` or `-d` on the command line\. For example:

```
# Invoke a function locally in debug mode on port 5858
$ sam local invoke -d 5858 <function logical id>

# Start local API Gateway in debug mode on port 5858
$ sam local start-api -d 5858
```

**Note**  
If you're using `sam local start-api`, the local API Gateway instance exposes all of your Lambda functions\. However, because you can specify a single debug port, you can only debug one function at a time\. You need to call your API before the AWS SAM CLI binds to the port, which allows the debugger to connect\.

**Topics**
+ [Debugging Node\.js Functions Locally](serverless-sam-cli-using-debugging-nodejs.md)
+ [Debugging Python Functions Locally](serverless-sam-cli-using-debugging-python.md)
+ [Debugging Golang Functions Locally](serverless-sam-cli-using-debugging-golang.md)