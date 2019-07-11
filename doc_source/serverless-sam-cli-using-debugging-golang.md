# Step\-Through Debugging Golang Functions Locally<a name="serverless-sam-cli-using-debugging-golang"></a>

Golang function step\-through debugging is slightly different when compared to Node\.js, Java, and Python\. We require [Delve](https://github.com/go-delve/delve) as the debugger, and wrap your function with it at runtime\. The debugger is run in headless mode, listening on the debug port\.

When you're debugging, you must compile your function in debug mode:

```
GOARCH=amd64 GOOS=linux go build -gcflags='-N -l' -o <output path> <path to code directory>
```

## Delve debugger

You must compile [Delve](https://github.com/go-delve/delve) to run in the container and provide its local path with the `--debugger-path` argument\. 

Build [Delve](https://github.com/go-delve/delve) locally as follows:

```
GOARCH=amd64 GOOS=linux go build -o <delve folder path>/dlv github.com/go-delve/delve/cmd/dlv
```

### Delve debugger path 
The output path needs to end in `/dlv`\. The Docker container expects the dlv binary file to be in the `<delve folder path>`\. If it's not, a mounting issue occurs\.

**Note**

 >The `--debugger-path` is the path to the directory that contains the dlv binary file that's compiled from the previous code\.

**Example**

Invoke AWS SAM similar to the following:

```
sam local start-api -d 5986 --debugger-path <delve folder path>
```

### Delve debugger API version 

To run the [Delve](https://github.com/go-delve/delve) debugger with an API verison of your choice, please
specifiy the desired API verison via an [additional debug argument](serverless-sam-cli-using-debugging-additional-arguments.md) '**-delveAPI**'.

**Note**  
> For IDEs such as GoLand, Microsoft Visual Studio Code, etc. It is important to run [Delve](https://github.com/go-delve/delve) in API version **2** mode.

**Example**

See below for an example of how to run [Delve](https://github.com/go-delve/delve)
in API verison **2** mode.
```
sam local start-api -d 5986 --debugger-path <delve folder path> --debug-args "-delveAPI=2"
```

## Example
> The following is an example launch configuration for Microsoft Visual Studio Code to attach to a debug session\.
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