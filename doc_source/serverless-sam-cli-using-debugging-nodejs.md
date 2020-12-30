# Step\-through debugging Node\.js functions locally<a name="serverless-sam-cli-using-debugging-nodejs"></a>

The following is an example that shows how to debug a Node\.js function with Microsoft Visual Studio Code:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/images/sam-debug.gif)

To set up Microsoft Visual Studio Code for step\-through debugging Node\.js functions with the AWS SAM CLI, use the following launch configuration\. Before you do this, set the directory where the `template.yaml` file is located as the workspace root in Microsoft Visual Studio Code:

```
{
     "version": "0.2.0",
     "configurations": [
         {
             "name": "Attach to SAM CLI",
             "type": "node",
             "request": "attach",
             "address": "localhost",
             "port": 5858,
             // From the sam init example, it would be "${workspaceRoot}/hello-world"
             "localRoot": "${workspaceRoot}/{directory of node app}",
             "remoteRoot": "/var/task",
             "protocol": "inspector",
             "stopOnEntry": false
         }
     ]
 }
```

**Note**  
The `localRoot` is set based on what the CodeUri points at in the `template.yaml` file\. If there are nested directories within the CodeUri, that needs to be reflected in the `localRoot`\.

**Note**  
Node\.js versions earlier than 7 \(for example, Node\.js 4\.3 and Node\.js 6\.10\) use the `legacy` protocol, while Node\.js versions including and later than 7 \(for example, Node\.js 8\.10\) use the `inspector` protocol\. Be sure to specify the corresponding protocol in the `protocol` entry of your launch configuration\. This was tested with Microsoft Visual Studio Code versions 1\.26, 1\.27, and 1\.28 for the `legacy` and `inspector` protocols\.