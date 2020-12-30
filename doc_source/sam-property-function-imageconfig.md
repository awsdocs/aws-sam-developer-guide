# ImageConfig \(Lambda property type\)<a name="sam-property-function-imageconfig"></a>

The object used to configure AWS Lambda container image settings\. The settings that you declare in your AWS SAM template override the settings of your container image\. For more information, see [Using container images with Lambda](https://docs.aws.amazon.com/lambda/latest/dg/lambda-images.html) in the *AWS Lambda Developer Guide*\.

**Note**  
This is a temporary location for this Lambda property type\. This topic will be moved to the *AWS CloudFormation User Guide* soon\.

## Syntax<a name="sam-property-function-imageconfig-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

**Note**  
If you declare an `ImageConfig` override in your template, you must also provide the values for the remaining `ImageConfig` properties as defined in your container image\. For example, if you are overriding `Command` as `arg1`, you must also provide the `EntryPoint` and `WorkingDirectory` defined for your container image\. This is a temporary limitation that will be resolved soon\.

### YAML<a name="sam-property-function-imageconfig-syntax.yaml"></a>

```
  [Command](#sam-function-imageconfig-command): List
  [EntryPoint](#sam-function-imageconfig-entrypoint): List
  [WorkingDirectory](#sam-function-imageconfig-workingdirectory): String
```

## Properties<a name="sam-property-function-imageconfig-properties"></a>

 `Command`   <a name="sam-function-imageconfig-command"></a>
Specifies the parameters that you want to pass in with `EntryPoint`\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `EntryPoint`   <a name="sam-function-imageconfig-entrypoint"></a>
Specifies the entry point to the application, which is typically the location of the runtime executable\.  
*Type*: List  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `WorkingDirectory`   <a name="sam-function-imageconfig-workingdirectory"></a>
Specifies the working directory\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-function-imageconfig--examples"></a>

### ImageConfig example<a name="sam-property-function-imageconfig--examples--imageconfig-example"></a>

The following is an example of an `ImageConfig` for a Lambda function of package type `Image`\.

#### YAML<a name="sam-property-function-imageconfig--examples--imageconfig-example--yaml"></a>

```
HelloWorldFunction:
  Type: AWS::Serverless::Function
  Properties:
    PackageType: Image
    ImageConfig:
      Command:
        - "app.lambda_handler" 
      EntryPoint:
        - "entrypoint1"
      WorkingDirectory: "workDir"
```