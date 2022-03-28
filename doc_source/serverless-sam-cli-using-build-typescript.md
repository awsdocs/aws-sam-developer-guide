# Building Node\.js Lambda functions with esbuild \(Preview\)<a name="serverless-sam-cli-using-build-typescript"></a>


****  

|  | 
| --- |
| esbuild support is currently in public preview\. During public preview, esbuild support may be subject to backwards incompatible changes\. | 

You can use the AWS SAM CLI with esbuild to build and package Node\.js Lambda functions\. esbuild supports Lambda functions that you write in TypeScript\.

To build a Node\.js Lambda function with esbuild, add a `Metadata` object to your `AWS:Serverless::Function` resource and specify `esbuild` for the `BuildMethod`\. When you run `sam build`, AWS SAM uses esbuild to bundle your Lambda function code\.

## Metadata properties<a name="serverless-sam-cli-using-build-typescript-metadata"></a>

The `Metadata` object supports the following properties for esbuild:

**BuildMethod**  
Specifies the bundler for your application\. The only supported value is `esbuild`\.

**BuildProperties**  
An object that specifies the build properties for your Lambda function code\.

The `BuildProperties` object supports the following properties for esbuild\. All of the properties are optional\. By default, AWS SAM uses your Lambda function handler for the entrypoint\.

**EntryPoints**  
Specifies entry points for your application\.

**Minify**  
Specifies whether to minify the bundled output code\. The default value is `true`\.

**Sourcemap**  
Specifies whether the bundler produces a sourcemap file\. The default value is `true`\.

**Target**  
Specifies the target ECMAScript version\. The default value is `es2020`\.

## TypeScript Lambda function example<a name="serverless-sam-cli-using-build-typescript-example"></a>

The following example AWS SAM template snippet uses esbuild to create a Node\.js Lambda function from TypeScript code in `hello-world/app.ts`\.

```
Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: hello-world/
      Handler: app.handler
      Runtime: nodejs14.x
      Architectures:
        - x86_64
      Events:
        HelloWorld:
          Type: Api 
          Properties:
            Path: /hello
            Method: get
    Metadata:
      BuildMethod: esbuild
      BuildProperties:
        Minify: false
        Target: "es2020"
        Sourcemap: true
        EntryPoints: 
          - app.ts
```

## Using the esbuild preview feature<a name="serverless-sam-cli-using-build-esbuild-preview"></a>

To use esbuild, you must opt in to the preview feature\. You can use a [configuration file](serverless-sam-cli-config.md), an environment variable, or a command line argument to use esbuild\. If you don't specify any of these, the AWS SAM CLI interactively prompts you to confirm whether or not to use the preview feature\. The following examples opt in to use esbuild and [sam sync](accelerate-sync.md)\.

------
#### [ Configuration file ]

Specify the following in your application's [configuration file](serverless-sam-cli-config.md)\.

```
[default.build.parameters]
beta_features = true
          
[default.sync.parameters]
beta_features = true
```

------
#### [ Environment variable ]

Set the environment variable `SAM_CLI_BETA_ESBUILD=1`\.

------
#### [ Command line argument ]

Add the `--beta-features` argument to your build command\. The argument enables all preview features of the AWS SAM CLI\.

```
sam build --beta-features
```

------