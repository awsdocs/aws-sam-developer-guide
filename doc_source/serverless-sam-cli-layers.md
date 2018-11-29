# Working with Layers<a name="serverless-sam-cli-layers"></a>

AWS SAM CLI supports applications that include Layers\. For more information about Layers see [Lambda Layers](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html)\.

Below is an example AWS SAM template with a Lambda function that includes a Layer:

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

For more information about including Layers in your application, see either [AWS::Serverless::Function](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessfunction) in the AWS SAM GitHub repository, or [AWS::Lambda::Function](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html) in the *AWS CloudFormation User Guide*\.

When you invoke your function using one of the sam local subcommands, the Layers package your function is downloaded and cached on your local host\. See the chart below for default cache directory locations\. Once cached, AWS SAM CLI will overlay the layers onto a Docker image that will be used to invoke your function\. AWS SAM CLI will generate the names of the images it builds as well as the LayerVersions held in the cache\. You can find more detail about the schema followed below\.

To inspect the overlaid layers, execute the following command to start a bash session in the image you want to inspect:

```
docker run -it --entrypoint=/bin/bash samcli/lambda:<Tag following the schema outlined in Docker Image Tag Schema> -i
```

**Layer Caching Directory name schema**

Given a LayerVersionArn defined in your template, AWS SAM CLI will extract the LayerName and Version from the ARN and create a directory to place the layer contents in named `LayerName-Version-<first 10 characters of sha256 of ARN>`\.

Example:

```
ARN = arn:aws:lambda:us-west-2:111111111111:layer:myLayer:1
Directory name = myLayer-1-926eeb5ff1
```

**Docker Images tag schema**

To compute the unique layers hash we combine all unique layer names with a delimiter of '\-' and take the sha256 has and take the first 25 characters

Example:

```
ServerlessFunction:
  Type: AWS::Serverless::Function
  Properties:
    CodeUri: .
    Hanlder: my_hanlder
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

To compute the unique layers hash we combine all unique layer names with a delimiter of '\-' and take the sha256 has and take the first 25 characters:

```
myLayer-1-926eeb5ff1-mySecondLayer-1-6bc1022bdf = 2dd7ac5ffb30d515926aef
```

Then combine this value with the Function's runtime with a delimiter of '\-':

```
python3.7-2dd7ac5ffb30d515926aefffd
```

**Default Cache Directory Locations**


****  

| OS | Location | 
| --- | --- | 
| Windows 7 | C:\\Users\\<user>\\AppData\\Roaming\\AWS SAM | 
| Windows 8 | C:\\Users\\<user>\\AppData\\Roaming\\AWS SAM | 
| Windows 10 | C:\\Users\\<user>\\AppData\\Roaming\\AWS SAM | 
| Mac OSX | \~/\.aws\-sam/layers\-pkg | 
| Unix | \~/\.aws\-sam/layers\-pkg | 