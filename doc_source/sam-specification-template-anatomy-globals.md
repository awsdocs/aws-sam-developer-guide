# Globals Section of the Template<a name="sam-specification-template-anatomy-globals"></a>

Resources in an AWS SAM template tend to have shared configuration, such as `Runtime`, `Memory`, `VPCConfig`, `Environment`, and `Cors`\. Instead of duplicating this information in every resource, you can write them once in the `Globals` section and let your resources inherit them\.

The `Globals` section is supported by the `AWS::Serverless::Function`, `AWS::Serverless::Api`, and `AWS::Serverless::SimpleTable` resources\.

Example:

```
Globals:
  Function:
    Runtime: nodejs6.10
    Timeout: 180
    Handler: index.handler
    Environment:
      Variables:
        TABLE_NAME: data-table

Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function
    Properties:
      Environment:
        Variables:
          MESSAGE: "Hello From SAM"

  ThumbnailFunction:
    Type: AWS::Serverless::Function
    Properties:
      Events:
        Thumbnail:
          Type: Api
          Properties:
            Path: /thumbnail
            Method: POST
```

In this example, both `HelloWorldFunction` and `ThumbnailFunction` use "nodejs6\.10" for `Runtime`, "180" seconds for `Timeout`, and "index\.handler" for `Handler`\. `HelloWorldFunction` adds the MESSAGE environment variable, in addition to the inherited TABLE\_NAME\. `ThumbnailFunction` inherits all the `Globals` properties and adds an API event source\.

## Supported Resources and Properties<a name="sam-specification-template-anatomy-globals-supported-resources-and-properties"></a>

Currently, AWS SAM supports the following resources and properties:

```
Globals:
  Function:
    # Properties of AWS::Serverless::Function
    Handler:
    Runtime:
    CodeUri:
    DeadLetterQueue:
    Description:
    MemorySize:
    Timeout:
    VpcConfig:
    Environment:
    Tags:
    Tracing:
    KmsKeyArn:
    Layers:
    AutoPublishAlias:
    DeploymentPreference:
    PermissionsBoundary:
    ReservedConcurrentExecutions:

  Api:
    # Properties of AWS::Serverless::Api
    # Also works with Implicit APIs
    Auth:
    Name:
    DefinitionUri:
    CacheClusterEnabled:
    CacheClusterSize:
    Variables:
    EndpointConfiguration:
    MethodSettings:
    BinaryMediaTypes:
    MinimumCompressionSize:
    Cors:
    GatewayResponses:
    AccessLogSetting:
    CanarySetting:
    TracingEnabled:
    OpenApiVersion:

  SimpleTable:
    # Properties of AWS::Serverless::SimpleTable
    SSESpecification:
```

## Implicit APIs<a name="sam-specification-template-anatomy-globals-implicit-apis"></a>

*Implicit APIs* are APIs that are created by AWS SAM when you declare an API in the `Events` section\. You can use `Globals` to override all the properties of implicit APIs\.

## Unsupported Properties<a name="sam-specification-template-anatomy-globals-unsupported-properties"></a>

The following properties are **not** supported in the `Globals` section\. We made the explicit call to not support them because it either made the template hard to understand, or opened a scope for potential security issues\.

```
  Function:
    Role:
    Policies:
    FunctionName:
    Events:

  Api:
    StageName:
    DefinitionBody:
```

## Overridable Properties<a name="sam-specification-template-anatomy-globals-overrideable"></a>

Properties that are declared in the `Globals` section can be overridden by the resource\. For example, you can add new variables to an environment variable map, or you can override globally declared variables\. But the resource **cannot** remove a property that's specified in the Globals environment variables map\. More generally, the Globals section declares properties that are shared by all your resources\. Some resources can provide new values for globally declared properties, but they can't completely remove them\. If some resources use a property but others don't, then you must not declare them in the Globals section\.

The following sections describe how overriding works for different data types\.

### Primitive Data Types Are Replaced<a name="sam-specification-template-anatomy-globals-overrideable-primitives"></a>

Primitive data types include strings, numbers, Booleans, and so on\.

The value specified in the Resources section **replaces** the value in the Globals section\.

Example:

```
Globals:
  Function:
    Runtime: nodejs4.3

Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      Runtime: python3.6
```

The `Runtime` for `MyFunction` is set to `python3.6`\.

### Maps Are Merged<a name="sam-specification-template-anatomy-globals-overrideable-maps"></a>

Maps are also known as dictionaries or collections of key\-value pairs\.

Map entries in the resource are **merged** with global map entries\. If there are duplicates, the resource entry overrides the global entry\.

Example:

```
Globals:
  Function:
    Environment:
      Variables:
        STAGE: Production
        TABLE_NAME: global-table

Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      Environment:
        Variables:
          TABLE_NAME: resource-table
          NEW_VAR: hello
```

The environment variables of `MyFunction` are set to the following:

```
{
  "STAGE": "Production",
  "TABLE_NAME": "resource-table",
  "NEW_VAR": "hello"
}
```

### Lists Are Additive<a name="sam-specification-template-anatomy-globals-overrideable-lists"></a>

Lists are also known as arrays\.

Entries in the Globals section are **prepended** to the list in the Resource section\.

Example:

```
Globals:
  Function:
    VpcConfig:
      SecurityGroupIds:
        - sg-123
        - sg-456

Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      VpcConfig:
        SecurityGroupIds:
          - sg-first
```

The `SecurityGroupIds` for `MyFunction`'s `VpcConfig` are set to the following:

```
[ "sg-123", "sg-456", "sg-first" ]
```