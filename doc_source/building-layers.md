# Building layers<a name="building-layers"></a>

You can use AWS SAM to build custom layers\. For information about layers, see [AWS Lambda layers](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html) in the *AWS Lambda Developer Guide*\.

To build a custom layer, declare it in your AWS Serverless Application Model \(AWS SAM\) template file and include a `Metadata` resource attribute section with a `BuildMethod` entry\. Valid values for `BuildMethod` are identifiers for an [AWS Lambda runtime](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html), or `makefile`\. Include a `BuildArchitecture` entry to specify the instruction set architectures that your layer supports\. Valid values for `BuildArchitecture` are [Lambda instruction set architectures](https://docs.aws.amazon.com/lambda/latest/dg/foundation-arch.html)\.

If you specify `makefile`, provide the custom makefile, where you declare a build target of the form `build-layer-logical-id` that contains the build commands for your layer\. Your makefile is responsible for compiling the layer if necessary, and copying the build artifacts into the proper location required for subsequent steps in your workflow\. The location of the makefile is specified by the `ContentUri` property of the layer resource, and must be named `Makefile`\.

**Note**  
When you create a custom layer, AWS Lambda depends on environment variables to find your layer code\. Lambda runtimes include paths in the `/opt` directory where your layer code is copied into\. Your project's build artifact folder structure must match the runtime's expected folder structure so your custom layer code can be found\.  
For example, for Python you can place your code in the `python/` subdirectory\. For NodeJS, you can place your code in the `nodejs/node_modules/` subdirectory\.  
For more information, see [Including library dependencies in a layer](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html#configuration-layers-path) in the *AWS Lambda Developer Guide*\.

The following is an example `Metadata` resource attribute section\.

```
    Metadata:
      BuildMethod: python3.8
      BuildArchitecture: arm64
```

**Note**  
If you don't include the `Metadata` resource attribute section, AWS SAM doesn't build the layer\. Instead, it copies the build artifacts from the location specified in the `CodeUri` property of the layer resource\. For more information, see the [ContentUri](sam-resource-layerversion.md#sam-layerversion-contenturi) property of the `AWS::Serverless::LayerVersion` resource type\.

When you include the `Metadata` resource attribute section, you can use the `sam build` command to build the layer, both as an independent object, or as a dependency of an AWS Lambda function\.
+ ****As an independent object\.**** You might want to build just the layer object, for example when you're locally testing a code change to the layer and don't need to build your entire application\. To build the layer independently, specify the layer resource with the `sam build layer-logical-id` command\.
+ **As a dependency of a Lambda function\.** When you include a layer's logical ID in the `Layers` property of a Lambda function in the same AWS SAM template file, the layer is a dependency of that Lambda function\. When that layer also includes a `Metadata` resource attribute section with a `BuildMethod` entry, you build the layer either by building the entire application with the `sam build` command or by specifying the function resource with the `sam build function-logical-id` command\.

## Examples<a name="building-applications-examples"></a>

### Template example 1: Build a layer against the Python 3\.9 runtime environment<a name="building-applications-examples-python"></a>

The following example AWS SAM template builds a layer against the Python 3\.6 runtime environment\.

```
Resources:
  MyLayer:
    Type: AWS::Serverless::LayerVersion
    Properties:
      ContentUri: my_layer
      CompatibleRuntimes:
        - python3.9
    Metadata:
      BuildMethod: python3.9              # Required to have AWS SAM build this layer
```

### Template example 2: Build a layer using a custom makefile<a name="building-applications-examples-makefile"></a>

The following example AWS SAM template uses a custom `makefile` to build the layer\.

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

The following `makefile` contains the build target and commands that will be executed\. Note that the `ContentUri` property is set to `my_layer`, so the makefile must be located in the root of the `my_layer` subdirectory, and the filename must be `Makefile`\. Note also that the build artifacts are copied into the `python/` subdirectory so that AWS Lambda will be able to find the layer code\.

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
