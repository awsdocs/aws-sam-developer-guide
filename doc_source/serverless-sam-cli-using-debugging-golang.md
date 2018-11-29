# Step\-through Debugging Golang Functions Locally<a name="serverless-sam-cli-using-debugging-golang"></a>

Golang function step\-through debugging is slightly different when compared to Node\.js, Java, and Python\. We require [delve](https://github.com/derekparker/delve) as the debugger, and wrap your function with it at runtime\. The debugger is run in headless mode, listening on the debug port\.

When you're debugging, you must compile your function in debug mode:

```
GOARCH=amd64 GOOS=linux go build -gcflags='-N -l' -o <output path> <path to code directory>
```

You must compile delve to run in the container and provide its local path with the `--debugger-path` argument\. Build delve locally as follows:

```
GOARCH=amd64 GOOS=linux go build -o <delve folder path>/dlv github.com/derekparker/delve/cmd/dlv
```

**Note**  
The output path needs to end in `/dlv`\. The Docker container expects the dlv binary file to be in the `<delve folder path>`\. If it's not, a mounting issue occurs\.

Then invoke AWS SAM similar to the following:

```
sam local start-api -d 5986 --debugger-path <delve folder path>
```

**Note**  
The `--debugger-path` is the path to the directory that contains the dlv binary file that's compiled from the previous code\.

The following is an example launch configuration for Microsoft Visual Studio Code to attach to a debug session\.

```
{
  "version": "0.2.0",
  "configurations": [
  {
      "name": "Connect to Lambda container",
      "type": "go",
      "request": "launch",
      "mode": "remote",
      "remotePath": "",
      "port": <debug port>,
      "host": "127.0.0.1",
      "program": "${workspaceRoot}",
      "env": {},
      "args": [],
    },
  ]
}
```