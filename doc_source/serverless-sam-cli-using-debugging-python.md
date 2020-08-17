# Step\-Through Debugging Python Functions Locally<a name="serverless-sam-cli-using-debugging-python"></a>

Python step\-through debugging requires you to enable remote debugging in your Lambda function code\. This is a two\-step process:

1. Install the [debugpy library](https://pypi.org/project/debugpy/) and enable it within your code\.

2. Configure your IDE to connect to the debugger that you configured for your function\.

If this is your first time using the AWS SAM CLI, start with a boilerplate Python application.

```
sam init --runtime python3.7 --name python-debugging
cd python-debugging/
```

## DebugPy Configuration<a name="serverless-sam-cli-using-debugging-python-ptvsd"></a>

Because SAM runs the code in a docker container, we will need to use a debugging library to listen for a debugging connection. Add `debugpy` to the `hello_world/requirements.txt` file.

Next, you need to enable ptvsd within your code\. To do this, open `hello_world/build/app.py`, and add the following code:

```
import debugpy

# Enable debugpy on all network interfaces within the docker containter (0.0.0.0) and on port 5890 that we'll connect to later with our IDE
debugpy.listen(("0.0.0.0",5678))
# Pause code execution until a debugger is connected
debugpy.wait_for_client()
```

Use `0.0.0.0` instead of `localhost` for listening across all network interfaces since port forwarding to the Docker container will not be picked up if you are listening on `localhost`\. `5890` is the debugging port that you want to use\.

Now run `sam build` to download the dependencies and build a code package. This will create a folder `/.aws-sam/build/` which contains the lambda code and all of the dependencies found in `requirements.txt`.

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
                   "localRoot": "${workspaceFolder}/.aws-sam/build",
                   "remoteRoot": "/var/task"
               }
           ]
       }
   ]
 }
```

For Microsoft Visual Studio Code, the property `localRoot` under the `pathMappings` key is important\.
+ **localRoot**: This is the path to the "local" code that needs to be an exactly copy of the code running "remoptely" (in the Docker container). `/.aws-sam/build` is the default that SAM builds to and mounts from, so that is what we use here\.
+ **remoteRoot**: this is the location in the SAM-run docker container where the code is located.
+ **workspaceFolder**: This path variable represents the absolute path where the Microsoft Visual Studio Code instance was opened\.

If you opened Microsoft Visual Studio Code in a different location other than `python-debugging/`, you need to replace it with the absolute path where `python-debugging/` is located\.

After the Microsoft Visual Studio Code debugger configuration is complete, make sure to add a breakpoint anywhere you want to in the built copy of your code at`.aws-sam/build/HelloWorldFunction/app.py`, and then proceed as follows:

1. Run the AWS SAM CLI to invoke your function with a `-d` option to tell SAM what port you will be listening on so that is knows to set up port forwarding\.

```
sam local start-api -d 5890

# OR

sam local invoke HelloWorldFunction --event events/event.json --d 5890 
```

2. If using `start-api`, send a request to the URL to invoke the function and initialize debugpy code execution\.

3. Start the debugger within Microsoft Visual Studio Code using the "SAM CLI Python Hello World" configuration\.

NOTE: Make sure your breakpoints are in the built version of your code, not the editable version of your code. You will need to rerun `sam build` any time you make changes to the code so that they are propigated into the build folder, which you should never edit directly.
