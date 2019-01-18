# AWS SAM Template Metadata Section Properties<a name="serverless-sam-template-publishing-applications-metadata-properties"></a>

This table provides information about the properties of the `Metadata` section of the AWS SAM template, which is needed to publish applications to the AWS Serverless Application Repository using AWS SAM CLI\.


****  

| Property | Type | Required | Description | 
| --- | --- | --- | --- | 
| Name | String | TRUE |  The name of the application\. Minimum length=1\. Maximum length=140\. Pattern: "\[a\-zA\-Z0\-9\\\\\-\]\+";  | 
| Description | String | TRUE |  The description of the application\. Minimum length=1\. Maximum length=256\.  | 
| Author | String | TRUE |  The name of the author publishing the applicatoin\. Minimum length=1\. Maximum length=127\. Pattern "^\[a\-z0\-9\]\(\(\[a\-z0\-9\]\|\-\(?\!\-\)\)\*\[a\-z0\-9\]\)?$";  | 
| SpdxLicenseId | String | TRUE | A valid license identifier: [https://spdx\.org/licenses/](https://spdx.org/licenses/) | 
| LicenseUrl | String | TRUE |  Reference to a local license file, or an Amazon S3 link to a license file, of the app that matches the spdxLicenseID value of your application\. An AWS SAM template file prior to being packaged using the `sam package` command could have a reference to a local file for this property\. However, to be published using the `sam publish` command, this property must be a reference to an Amazon S3 bucket\. Maximum size 5 MB  | 
| ReadmeUrl | String | FALSE |  Reference to a local readme file, or an Amazon S3 link to the readme file, that contains a more detailed description of the application and how it works\. An AWS SAM template file prior to being packaged using the `sam package` command could have a reference to a local file for this property\. However, to be published using the `sam publish` command, this property must be a reference to an Amazon S3 bucket\. Maximum size 5 MB  | 
| Labels | String | FALSE |  Labels to improve discovery of apps in search results\. Minimum length=1\. Maximum length=127\. Maximum number of labels: 10 Pattern: "^\[a\-zA\-Z0\-9\+\\\\\-\_:\\\\/@\]\+$";  | 
| HomePageUrl | String | FALSE | A URL with more information about the application, for example the location of your GitHub repository for the application\.  | 
| SemanticVersion | String | FALSE |  The semantic version of the application: [https://semver\.org/](https://semver.org/) You must provide a value for this property in order to make your application public\.  | 
| SourceCodeUrl | String | FALSE | A link to a public repository for the source code of your application\. | 

## Use Cases<a name="serverless-sam-template-publishing-applications-metadata-properties-cases"></a>

The use cases for publishing applications are listed below, along with the `Metadata` properties that are processed for that use case\. Properties that are *not* listed for a given use casese are ignored\.
+ **Create New Application** – A new application is created if there is no application in AWS Serverless Application Repository with a matching name for an account\.
  + Name
  + SpdxLicenseId
  + LicenseUrl
  + Description
  + Author
  + ReadmeUrl
  + Labels
  + HomePageUrl
  + SourceCodeUrl
  + SemanticVersion
  + The content of the SAM template \(for example, any Event Sources, Resources, Lambda function code, etc\.\)

   
+ **Create Application Version** – An application version is created if there is already an application in AWS Serverless Application Repository with a matching name for an account *and* the SemanticVersion *is* changing\.
  + Description
  + Author
  + ReadmeUrl
  + Labels
  + HomePageUrl
  + SourceCodeUrl
  + SemanticVersion
  + The content of the SAM template \(for example, any Event Sources, Resources, Lambda function code, etc\.\)

   
+ **Update Application** – An application is updated if there is already an application in AWS Serverless Application Repository with a matching name for an account *and* the SemanticVersion *is not* changing\.
  + Description
  + Author
  + ReadmeUrl
  + Labels
  + HomePageUrl