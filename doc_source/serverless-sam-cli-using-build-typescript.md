# Building Node\.js Lambda functions with esbuild<a name="serverless-sam-cli-using-build-typescript"></a>

To build and package Node\.js AWS Lambda functions, you can use the AWS SAM CLI with the esbuild JavaScript bundler\. The esbuild bundler supports Lambda functions that you write in TypeScript\.

To build a Node\.js Lambda function with esbuild, add a `Metadata` object to your `AWS:Serverless::Function` resource and specify `esbuild` for the `BuildMethod`\. When you run the sam build command, AWS SAM uses esbuild to bundle your Lambda function code\.

## Metadata properties<a name="serverless-sam-cli-using-build-typescript-metadata"></a>

The `Metadata` object supports the following properties for esbuild\.

### BuildMethod<a name="serverless-sam-cli-using-build-typescript-metadata-buildmethod"></a>

Specifies the bundler for your application\. The only supported value is `esbuild`\.

### BuildProperties<a name="serverless-sam-cli-using-build-typescript-metadata-buildproperties"></a>

Specifies the build properties for your Lambda function code\.

The `BuildProperties` object supports the following properties for esbuild\. All of the properties are optional\. By default, AWS SAM uses your Lambda function handler for the entry point\.

**EntryPoints**  
Specifies entry points for your application\.

**External**  
Specifies the list of packages to omit from the build\.

**Format**  
Specifies the output format of the generated JavaScript files in your application\. For more information, see [Format](https://esbuild.github.io/api/#format) in the *esbuild website*\.

**Loader**  
Specifies the list of configurations for loading data for a given file type\.

**MainFields**  
Specifies which `package.json` fields to try to import when resolving a package\. The default value is `main,module`\.

**Minify**  
Specifies whether to minify the bundled output code\. The default value is `true`\.

**OutExtension**  
Customize the file extension of the files that esbuild generates\. For more information, see [Out extension](https://esbuild.github.io/api/#out-extension) in the *esbuild website*\.

**Sourcemap**  
Specifies whether the bundler produces a source map file\. The default value is `false`\.  
When set to `true`, `NODE_OPTIONS: --enable-source-maps` is appended to the Lambda function's environment variables, and a source map is generated and included in the function\.  
Alternatively, when `NODE_OPTIONS: --enable-source-maps` is included in the function's environment variables, `Sourcemap` is automatically set to `true`\.  
When conflicting, `Sourcemap: false` takes precedence over `NODE_OPTIONS: --enable-source-maps`\.  
By default, Lambda encrypts all environment variables at rest with AWS Key Management Service \(AWS KMS\)\. When using source maps, for the deployment to succeed, your function's execution role must have permission to perform the `kms:Encrypt` action\.

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
      Environment:
        Variables:
          NODE_OPTIONS: --enable-source-maps
    Metadata:
      BuildMethod: esbuild
      BuildProperties:
        Format: esm
        Minify: false
        OutExtension:
          - .js=.mjs
        Target: "es2020"
        Sourcemap: true
        EntryPoints: 
          - app.ts
```