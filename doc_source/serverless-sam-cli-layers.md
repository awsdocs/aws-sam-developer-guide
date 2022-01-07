# Working with layers<a name="serverless-sam-cli-layers"></a>

Using AWS SAM, you can include layers in your serverless applications\. For more information about layers, see [AWS Lambda layers](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html) in the *AWS Lambda Developer Guide*\.

This topic provides information about the following:
+ Including layers in your application
+ How layers are cached locally

For information about building custom layers, see [Building layers](building-layers.md)\.

## Including layers in your application<a name="including-layers"></a>

To include layers in your application, use the `Layers` property of the [AWS::Serverless::Function](sam-resource-function.md) resource type\.

Following is an example AWS SAM template with a Lambda function that includes a layer:

```
ServerlessFunction:
  Type: AWS::Serverless::Function
  Properties:
    CodeUri: .
    Handler: my_handler
    Runtime: Python3.7
    Layers:
        - <LayerVersion ARN>
```

## How layers are cached locally<a name="local-testing-with-layers"></a>

When you invoke your function using one of the `sam local` commands, the layers package of your function is downloaded and cached on your local host\.

The following table shows the default cache directory locations for different operating systems\.


****  

| OS | Location | 
| --- | --- | 
| Windows 7 | C:\\Users\\<user>\\AppData\\Roaming\\AWS SAM | 
| Windows 8 | C:\\Users\\<user>\\AppData\\Roaming\\AWS SAM | 
| Windows 10 | C:\\Users\\<user>\\AppData\\Roaming\\AWS SAM | 
| macOS | \~/\.aws\-sam/layers\-pkg | 
| Unix | \~/\.aws\-sam/layers\-pkg | 

After the package is cached, the AWS SAM CLI overlays the layers onto a Docker image that's used to invoke your function\. The AWS SAM CLI generates the names of the images it builds, as well as the LayerVersions that are held in the cache\. You can find more details about the schema in the following sections\.

To inspect the overlaid layers, execute the following command to start a bash session in the image that you want to inspect:

```
docker run -it --entrypoint=/bin/bash samcli/lambda:<Tag following the schema outlined in Docker Image Tag Schema> -i
```

**Layer Caching Directory name schema**

Given a LayerVersionArn that's defined in your template, the AWS SAM CLI extracts the LayerName and Version from the ARN\. It creates a directory to place the layer contents in named `LayerName-Version-<first 10 characters of sha256 of ARN>`\.

Example:

```
ARN = arn:aws:lambda:us-west-2:111111111111:layer:myLayer:1
Directory name = myLayer-1-926eeb5ff1
```

**Docker Images tag schema**

To compute the unique layers hash, combine all unique layer names with a delimiter of '\-', take the SHA256 hash, and then take the first 10 characters\.

Example:

```
ServerlessFunction:
  Type: AWS::Serverless::Function
  Properties:
    CodeUri: .
    Handler: my_handler
    Runtime: Python3.7
    Layers:
        - arn:aws:lambda:us-west-2:111111111111:layer:myLayer:1
        - arn:aws:lambda:us-west-2:111111111111:layer:mySecondLayer:1
```

Unique names are computed the same as the Layer Caching Directory name schema:

```
arn:aws:lambda:us-west-2:111111111111:layer:myLayer:1 = myLayer-1-926eeb5ff1
arn:aws:lambda:us-west-2:111111111111:layer:mySecondLayer:1 = mySecondLayer-1-6bc1022bdf
```

To compute the unique layers hash, combine all unique layer names with a delimiter of '\-', take the sha256 hash, and then take the first 25 characters:

```
myLayer-1-926eeb5ff1-mySecondLayer-1-6bc1022bdf = 2dd7ac5ffb30d515926aef
```

Then combine this value with the function's runtime and architecture, with a delimiter of '\-':

```
python3.7-x86_64-2dd7ac5ffb30d515926aefffd
```