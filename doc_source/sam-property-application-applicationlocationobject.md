# ApplicationLocationObject<a name="sam-property-application-applicationlocationobject"></a>

An application that has been published to the [AWS Serverless Application Repository](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/what-is-serverlessrepo.html)\.

## Syntax<a name="sam-property-application-applicationlocationobject-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-application-applicationlocationobject-syntax.yaml"></a>

```
  [ApplicationId](#sam-application-applicationlocationobject-applicationid): String
  [SemanticVersion](#sam-application-applicationlocationobject-semanticversion): String
```

## Properties<a name="sam-property-application-applicationlocationobject-properties"></a>

 `ApplicationId`   <a name="sam-application-applicationlocationobject-applicationid"></a>
The Amazon Resource Name \(ARN\) of the application\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

 `SemanticVersion`   <a name="sam-application-applicationlocationobject-semanticversion"></a>
The semantic version of the application\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.

## Examples<a name="sam-property-application-applicationlocationobject--examples"></a>

### my\-application<a name="sam-property-application-applicationlocationobject--examples--my-application"></a>

Example application location object

#### YAML<a name="sam-property-application-applicationlocationobject--examples--my-application--yaml"></a>

```
Location:
  ApplicationId: 'arn:aws:serverlessrepo:us-east-1:012345678901:applications/my-application'
  SemanticVersion: 1.0.0
```