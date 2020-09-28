# Building layers<a name="building-layers"></a>

To build layers that you have declared in your AWS Serverless Application Model \(AWS SAM\) template file, include a `Metadata` resource attribute section with a `BuildMethod` entry\. Valid values for `BuildMethod` are identifiers for an [AWS Lambda runtime](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html), or `makefile`\.

If you specify `makefile`, provide the custom makefile, where you declare a build target of the form `build-layer-logical-id` that contains the build commands for your layer\. Your makefile is responsible for compiling the layer if necessary, and copying the build artifacts into the proper location required for subsequent steps in your workflow\.

The following is an example `Metadata` resource attribute section\.

```
    Metadata:
      BuildMethod: python3.6
```

**Note**  
If you don't include the `Metadata` resource attribute section, AWS SAM doesn't build the layer\. Instead, it copies the build artifacts from the location specified in the `CodeUri` property of the layer resource\. For more information, see the [ContentUri](sam-resource-layerversion.md#sam-layerversion-contenturi) property of the `AWS::Serverless::LayerVersion` resource type\.

When you include the `Metadata` resource attribute section, you can use the `` command to build the layer, both as an independent object, or as a dependency of an AWS Lambda function\.
+ ****As an independent object\.**** You might want to build just the layer object, for example when you're locally testing a code change to the layer and don't need to build your entire application\. To build the layer independently, specify the layer resource with the `sam build layer-logical-id` command\.
+ **As a dependency of a Lambda function\.** When you include a layer's logical ID in the `Layers` property of a Lambda function in the same AWS SAM template file, the layer is a dependency of that Lambda function\. When that layer also includes a `Metadata` resource attribute section with a `BuildMethod` entry, you build the layer either by building the entire application with the `sam build` command or by specifying the function resource with the `sam build function-logical-id` command\.

## Examples<a name="building-applications-examples"></a>

### Template example 1: Build a layer against the Python 3\.6 runtime environment<a name="building-applications-examples-python"></a>

The following example AWS SAM template builds a layer against the Python 3\.6 runtime environment\.

```
Resources:
  MyLayer:
    Type: AWS::Serverless::LayerVersion
    Properties:
      ContentUri: my_layer
      CompatibleRuntimes:
        - python3.6
    Metadata:
      BuildMethod: python3.6              # Required to have AWS SAM build this layer
```

### Template example 2: Build a layer using a custom makefile<a name="building-applications-examples-makefile"></a>

The following example AWS SAM template uses a custom makefile to build the layer\.

```
Resources:
  MyLayer:
    Type: AWS::Serverless::LayerVersion
    Properties:
      ContentUri: my_layer
      CompatibleRuntimes:
        - python3.8
    Metadata:
      BuildMethod: makefile
```

The following makefile contains the build target and commands that will be executed\.

```
build-MyLayer:
    mkdir -p "$(ARTIFACTS_DIR)/python"
    cp *.py "$(ARTIFACTS_DIR)/python"
    python -m pip install -r requirements.txt -t "$(ARTIFACTS_DIR)/python"
```

### Example sam build commands<a name="building-applications-examples-commands"></a>

The following `sam build` commands build layers that include the `Metadata` resource attribute sections\.

```
# Build the 'layer-logical-id' resource independently
sam build layer-logical-id
            
# Build the 'function-logical-id' resource and layers that this function depends on
sam build function-logical-id

# Build the entire application, including the layers that any function depends on
sam build
```