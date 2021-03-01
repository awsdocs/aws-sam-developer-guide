# Step\-through debugging Python functions locally<a name="serverless-sam-cli-using-debugging-python"></a>

Python step\-through debugging requires you to enable remote debugging in your Lambda function code\. This is a two\-step process:

1. Install the [ptvsd library](https://pypi.org/project/ptvsd/) and enable it within your code\.

1. Configure your IDE to connect to the debugger that you configured for your function\.

Because this might be your first time using the AWS SAM CLI, start with a boilerplate Python application, and install both the application's dependencies and ptvsd:

```
sam init --runtime python3.6 --name python-debugging
cd python-debugging/

# Install dependencies of our boilerplate app
pip install -r hello_world/requirements.txt -t hello_world/build/

# Install ptvsd library for step through debugging
pip install ptvsd -t hello_world/build/

cp hello_world/app.py hello_world/build/
```

## Ptvsd configuration<a name="serverless-sam-cli-using-debugging-python-ptvsd"></a>

Next, you need to enable ptvsd within your code\. To do this, open `hello_world/build/app.py`, and add the following ptvsd specifics:

```
import ptvsd

# Enable ptvsd on 0.0.0.0 address and on port 5890 that we'll connect later with our IDE
ptvsd.enable_attach(address=('0.0.0.0', 5890), redirect_output=True)
ptvsd.wait_for_attach()
```

Use `0.0.0.0` instead of `localhost` for listening across all network interfaces\. `5890` is the debugging port that you want to use\.

## Microsoft Visual Studio Code<a name="serverless-sam-cli-using-debugging-python-vs-code"></a>

Now that you have the dependencies and ptvsd enabled within your code, you can configure Microsoft Visual Studio Code debugging\. Assuming that you're still in the application folder and have the code command in your path, open Microsoft Visual Studio Code by using this command:

```
code .
```

**Note**  
 If you don't have code in your path, open a new instance of Microsoft Visual Studio Code from the `python-debugging/` folder that you created earlier\.

To set up Microsoft Visual Studio Code for debugging with the AWS SAM CLI, use the following launch configuration:

```
{
    "version": "0.2.0",
    "configurations": [
        {
           "name": "SAM CLI Python Hello World",
           "type": "python",
           "request": "attach",
           "port": 5890,
           "host": "localhost",
           "pathMappings": [
               {
                   "localRoot": "${workspaceFolder}/hello_world/build",
                   "remoteRoot": "/var/task"
               }
           ]
       }
   ]
 }
```

For Microsoft Visual Studio Code, the property `localRoot` under the `pathMappings` key is important\. There are two reasons that help explain this setup:
+ **localRoot**: This path is to be mounted in the Docker container, and needs to have both the application and dependencies at the root level\.
+ **workspaceFolder**: This path is the absolute path where the Microsoft Visual Studio Code instance was opened\.

If you opened Microsoft Visual Studio Code in a different location other than `python-debugging/`, you need to replace it with the absolute path where `python-debugging/` is located\.

After the Microsoft Visual Studio Code debugger configuration is complete, make sure to add a breakpoint anywhere you want to in `hello_world/build/app.py`, and then proceed as follows:

1. Run the AWS SAM CLI to invoke your function\.

1. Send a request to the URL to invoke the function and initialize ptvsd code execution\.

1. Start the debugger within Microsoft Visual Studio Code\.

```
# Remember to hit the URL before starting the debugger in Microsoft Visual Studio Code
sam local start-api -d 5890

# OR

# Change HelloWorldFunction to reflect the logical name found in template.yaml
sam local generate-event apigateway aws-proxy | sam local invoke HelloWorldFunction -d 5890
```