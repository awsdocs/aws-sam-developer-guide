# AWS SAM template Metadata section properties<a name="serverless-sam-template-publishing-applications-metadata-properties"></a>

`AWS::ServerlessRepo::Application` is a metadata key that you can use to specify application information that you want published to the AWS Serverless Application Repository\.

**Note**  
AWS CloudFormation [intrinsic functions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html) aren't supported by the `AWS::ServerlessRepo::Application` metadata key\.

## Properties<a name="serverless-sam-template-publishing-applications-metadata-properties-table"></a>

This table provides information about the properties of the `Metadata` section of the AWS SAM template\. This section is required to publish applications to the AWS Serverless Application Repository using the AWS SAM CLI\.


****  

| Property | Type | Required | Description | 
| --- | --- | --- | --- | 
| Name | String | TRUE |  The name of the application\. Minimum length=1\. Maximum length=140\. Pattern: `"[a-zA-Z0-9\\-]+";`  | 
| Description | String | TRUE |  The description of the application\. Minimum length=1\. Maximum length=256\.  | 
| Author | String | TRUE |  The name of the author publishing the application\. Minimum length=1\. Maximum length=127\. Pattern: `"^[a-z0-9](([a-z0-9]\|-(?!-))*[a-z0-9])?$";`  | 
| SpdxLicenseId | String | FALSE | A valid license identifier\. To view the list of valid license identifiers, see [SPDX License List](https://spdx.org/licenses/) on the Software Package Data Exchange \(SPDX\) website\. | 
| LicenseUrl | String | FALSE |  The reference to a local license file, or an Amazon S3 link to a license file, that matches the spdxLicenseID value of your application\. An AWS SAM template file that hasn't been packaged using the `sam package` command can have a reference to a local file for this property\. However, for an application to be published using the `sam publish` command, this property must be a reference to an Amazon S3 bucket\. Maximum size: 5 MB\. You must provide a value for this property in order to make your application public\. Note that you cannot update this property after your application has been published\. So, to add a license to an application, you must either delete it first, or publish a new application with a different name\.  | 
| ReadmeUrl | String | FALSE |  The reference to a local readme file or an Amazon S3 link to the readme file that contains a more detailed description of the application and how it works\. An AWS SAM template file that hasn't been packaged using the `sam package` command can have a reference to a local file for this property\. However, to be published using the `sam publish` command, this property must be a reference to an Amazon S3 bucket\. Maximum size: 5 MB\.  | 
| Labels | String | FALSE |  The labels that improve discovery of applications in search results\. Minimum length=1\. Maximum length=127\. Maximum number of labels: 10\. Pattern: `"^[a-zA-Z0-9+\\-_:\\/@]+$";`  | 
| HomePageUrl | String | FALSE | A URL with more information about the application—for example, the location of your GitHub repository for the application\.  | 
| SemanticVersion | String | FALSE |  The semantic version of the application\. For the Semantic Versioning specification, see the [Semantic Versioning](https://semver.org/) website\. You must provide a value for this property in order to make your application public\.  | 
| SourceCodeUrl | String | FALSE | A link to a public repository for the source code of your application\. | 

## Use cases<a name="serverless-sam-template-publishing-applications-metadata-properties-cases"></a>

This section lists the use cases for publishing applications, along with the `Metadata` properties that are processed for that use case\. Properties that are *not* listed for a given use case are ignored\.
+ **Creating a new application** – A new application is created if there is no application in the AWS Serverless Application Repository with a matching name for an account\.
  + `Name`
  + `SpdxLicenseId`
  + `LicenseUrl`
  + `Description`
  + `Author`
  + `ReadmeUrl`
  + `Labels`
  + `HomePageUrl`
  + `SourceCodeUrl`
  + `SemanticVersion`
  + The content of the AWS SAM template \(for example, any event sources, resources, and Lambda function code\)

   
+ **Creating an application version** – An application version is created if there is already an application in the AWS Serverless Application Repository with a matching name for an account *and* the SemanticVersion *is* changing\.
  + `Description`
  + `Author`
  + `ReadmeUrl`
  + `Labels`
  + `HomePageUrl`
  + `SourceCodeUrl`
  + `SemanticVersion`
  + The content of the AWS SAM template \(for example, any event sources, resources, and Lambda function code\)

   
+ **Updating an application** – An application is updated if there is already an application in the AWS Serverless Application Repository with a matching name for an account *and* the SemanticVersion *is not* changing\.
  + `Description`
  + `Author`
  + `ReadmeUrl`
  + `Labels`
  + `HomePageUrl`

## Example<a name="serverless-sam-template-publishing-applications-metadata-properties-example"></a>

The following is an example `Metadata` section:

```
Metadata:
  AWS::ServerlessRepo::Application:
    Name: my-app
    Description: hello world
    Author: user1
    SpdxLicenseId: Apache-2.0
    LicenseUrl: LICENSE.txt
    ReadmeUrl: README.md
    Labels: ['tests']
    HomePageUrl: https://github.com/user1/my-app-project
    SemanticVersion: 0.0.1
    SourceCodeUrl: https://github.com/user1/my-app-project
```