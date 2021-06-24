# Passing additional runtime debug arguments<a name="serverless-sam-cli-using-debugging-additional-arguments"></a>

To pass additional runtime arguments when you're debugging your function, use the environment variable `DEBUGGER_ARGS`\. This passes a string of arguments directly into the run command that the AWS SAM CLI uses to start your function\.

For example, if you want to load a debugger like iKPdb at the runtime of your Python function, you could pass the following as `DEBUGGER_ARGS: -m ikpdb --ikpdb-port=5858 --ikpdb-working-directory=/var/task/ --ikpdb-client-working-directory=/myApp --ikpdb-address=0.0.0.0`\. This would load iKPdb at runtime with the other arguments you’ve specified\.

In this case, your full AWS SAM CLI command would be:

```
DEBUGGER_ARGS="-m ikpdb --ikpdb-port=5858 --ikpdb-working-directory=/var/task/ --ikpdb-client-working-directory=/myApp --ikpdb-address=0.0.0.0" echo {} | sam local invoke -d 5858 myFunction
```

You can pass debugger arguments to the functions of all runtimes\.