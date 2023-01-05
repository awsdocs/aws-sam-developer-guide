# SnapStart<a name="sam-property-function-snapstart"></a>

Create a snapshot of any new AWS Lambda function version\. A snapshot is a cached state of your initialized function, including all of its dependencies\. The function is initialized just once and the cached state is reused for all future invocations, improving application performance by reducing the number of times your function must be initialized\. To learn more, see [SnapStart](https://docs.aws.amazon.com/lambda/latest/dg/API_SnapStart.html) in the *AWS Lambda API Reference*\.

## Syntax<a name="sam-property-function-snapstart-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-function-snapstart-syntax.yaml"></a>

```
  [ApplyOn](#sam-function-snapstart-applyon): String
```

## Properties<a name="sam-property-function-snapstart-applyon"></a>

 `ApplyOn`   <a name="sam-function-snapstart-applyon"></a>
Specify when to create a snapshot of your new Lambda function version\.  
`None` – SnapStart is turned off\.  
`PublishedVersions` – SnapStart is turned on for all newly published versions of the function\.  
If `PublishedVersions` is specified with `AutoPublishAlias`, all code changes will publish a new Lambda function version and a snapshot will be created\. Wait a few minutes while the snapshot is being created before invoking your function alias\.
*Type*: String  
*Allowed Values*: `None` \(default\) \| `PublishedVersions`  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `ApplyOn` property of the `[SnapStart](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-snapstart)` field of an `AWS::Lambda::Function` resource\.

## Examples<a name="sam-property-function-snapstart--examples"></a>

### Basic example<a name="sam-property-function-snapstart--examples--example1"></a>

Example of a Lambda function with SnapStart turned on for future versions\.

#### YAML<a name="sam-property-function-snapstart--examples--example1--yaml"></a>

```
TestFunc
  Type: AWS::Serverless::Function
  Properties:
    ...
    SnapStart:
      ApplyOn: PublishedVersions
```