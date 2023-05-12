# Using the AWS SAM CLI to upload local files at deployment<a name="deploy-upload-local-files"></a>

When developing, you will often find it beneficial to break up your application code into separate files to better organize and manage your application\. A basic example of this is separating your AWS Lambda function code from your infrastructure code\. You do this by organizing your Lambda function code in a subdirectory of your project and referencing its local path within your AWS Serverless Application Model \(AWS SAM\) template\.

When you deploy your application to the AWS Cloud, AWS CloudFormation requires that your local files are first uploaded to an accessible AWS service, such as Amazon Simple Storage Service \(Amazon S3\)\. You can use the AWS SAM CLI to automatically facilitate this process\. Use the `sam deploy` or `sam package` command to do the following:

1. Automatically upload your local files to an accessible AWS service\.

1. Automatically update your application template to reference the new file path\.

**Topics**
+ [Demo: Use the AWS SAM CLI to upload Lambda function code](#deploy-upload-local-files-demo)
+ [Supported use cases](#deploy-upload-local-files-use)
+ [Learn more](#deploy-upload-local-files-learn)

## Demo: Use the AWS SAM CLI to upload Lambda function code<a name="deploy-upload-local-files-demo"></a>

In this demo, we initialize the sample Hello World application using a \.zip package type for our Lambda function\. We use the AWS SAM CLI to automatically upload our Lambda function code to Amazon S3 and reference its new path in our application template\.

First, we run `sam init` to initialize our Hello World application\.

```
$ sam init
...
Which template source would you like to use?
        1 - AWS Quick Start Templates
        2 - Custom Template Location
Choice: 1

Choose an AWS Quick Start application template
        1 - Hello World Example
        2 - Multi-step workflow
        ...
Template: 1

Use the most popular runtime and package type? (Python and zip) [y/N]: y

Would you like to enable X-Ray tracing on the function(s) in your application?  [y/N]: ENTER

Would you like to enable monitoring using CloudWatch Application Insights?
For more info, please view https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-application-insights.html [y/N]: ENTER

Project name [sam-app]: demo

    -----------------------
    Generating application:
    -----------------------
    Name: demo
    Runtime: python3.9
    Architectures: x86_64
    Dependency Manager: pip
    Application Template: hello-world
    Output Directory: .
    Configuration file: demo/samconfig.toml
    
...
```

Our Lambda function code is organized in the `hello_world` subdirectory of our project\.

```
demo
├── README.md
├── hello_world
│   ├── __init__.py
│   ├── app.py
│   └── requirements.txt
├── template.yaml
└── tests
```

Within our AWS SAM template, we reference the local path to our Lambda function code using the `CodeUri` property\.

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function # More info about Function Resource: https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessfunction
    Properties:
      CodeUri: hello_world/
      Handler: app.lambda_handler
      Runtime: python3.9
      ...
```

Next, we run `sam build` to build our application and prepare for deployment\.

```
$ sam build
Starting Build use cache
Manifest file is changed (new hash: 3298f13049d19cffaa37ca931dd4d421) or dependency folder (.aws-sam/deps/7896875f-9bcc-4350-8adb-2c1d543627a1) is missing for (HelloWorldFunction), downloading dependencies and copying/building source
Building codeuri: /Users/.../demo/hello_world runtime: python3.9 metadata: {} architecture: x86_64 functions: HelloWorldFunction
Running PythonPipBuilder:CleanUp
Running PythonPipBuilder:ResolveDependencies
Running PythonPipBuilder:CopySource
Running PythonPipBuilder:CopySource

Build Succeeded

Built Artifacts  : .aws-sam/build
Built Template   : .aws-sam/build/template.yaml
...
```

Next, we run `sam deploy --guided` to deploy our application\.

```
$ sam deploy --guided

Configuring SAM deploy
======================

        Looking for config file [samconfig.toml] :  Found
        Reading default arguments  :  Success

        Setting default arguments for 'sam deploy'
        =========================================
        Stack Name [demo]: ENTER
        AWS Region [us-west-2]: ENTER
        #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
        Confirm changes before deploy [Y/n]: n
        #SAM needs permission to be able to create roles to connect to the resources in your template
        Allow SAM CLI IAM role creation [Y/n]: ENTER
        #Preserves the state of previously provisioned resources when an operation fails
        Disable rollback [y/N]: ENTER
        HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
        Save arguments to configuration file [Y/n]: ENTER
        SAM configuration file [samconfig.toml]: ENTER
        SAM configuration environment [default]: ENTER

        Looking for resources needed for deployment:
        ...
        Saved arguments to config file
        Running 'sam deploy' for future deployments will use the parameters saved above.
        The above parameters can be changed by modifying samconfig.toml
        Learn more about samconfig.toml syntax at 
        https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-config.html

File with same data already exists at demo/da3c598813f1c2151579b73ad788cac8, skipping upload

        Deploying with following values
        ===============================
        Stack name                   : demo
        Region                       : us-west-2
        Confirm changeset            : False
        Disable rollback             : False
        Deployment s3 bucket         : aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr
        Capabilities                 : ["CAPABILITY_IAM"]
        Parameter overrides          : {}
        Signing Profiles             : {}

Initiating deployment
=====================
...
Waiting for changeset to be created..
CloudFormation stack changeset
-------------------------------------------------------------------------------------------------
Operation                LogicalResourceId        ResourceType             Replacement            
-------------------------------------------------------------------------------------------------
+ Add                    HelloWorldFunctionHell   AWS::Lambda::Permissio   N/A                    
                         oWorldPermissionProd     n                                               
+ Add                    HelloWorldFunctionRole   AWS::IAM::Role           N/A                    
...                     
-------------------------------------------------------------------------------------------------

Changeset created successfully. arn:aws:cloudformation:us-west-2:513423067560:changeSet/samcli-deploy1680906292/1164338d-72e7-4593-a372-f2b3e67f542f

2023-04-07 12:24:58 - Waiting for stack create/update to complete

CloudFormation events from stack operations (refresh every 5.0 seconds)
-------------------------------------------------------------------------------------------------
ResourceStatus           ResourceType             LogicalResourceId        ResourceStatusReason   
-------------------------------------------------------------------------------------------------
CREATE_IN_PROGRESS       AWS::IAM::Role           HelloWorldFunctionRole   -                      
CREATE_IN_PROGRESS       AWS::IAM::Role           HelloWorldFunctionRole   Resource creation      
                                                                           Initiated              
...                    
-------------------------------------------------------------------------------------------------
CloudFormation outputs from deployed stack
-------------------------------------------------------------------------------------------------
Outputs                                                                                         
-------------------------------------------------------------------------------------------------
Key                 HelloWorldFunctionIamRole                                                   
Description         Implicit IAM Role created for Hello World function                          
Value               arn:aws:iam::513423067560:role/demo-HelloWorldFunctionRole-VQ4CU7UY7S2K     

Key                 HelloWorldApi                                                               
Description         API Gateway endpoint URL for Prod stage for Hello World function            
Value               https://satnon55e9.execute-api.us-west-2.amazonaws.com/Prod/hello/          

Key                 HelloWorldFunction                                                          
Description         Hello World Lambda Function ARN                                             
Value               arn:aws:lambda:us-west-2:513423067560:function:demo-                        
HelloWorldFunction-G14inKTmSQvK                                                                 
-------------------------------------------------------------------------------------------------
Successfully created/updated stack - demo in us-west-2
```

During deployment, the AWS SAM CLI automatically uploads our Lambda function code to Amazon S3 and updates our template\. Our modified template in the AWS CloudFormation console reflects the Amazon S3 bucket path\.

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: s3://aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr/demo/da3c598813f1c2151579b73ad788cac8
      Handler: app.lambda_handler
      ...
```

## Supported use cases<a name="deploy-upload-local-files-use"></a>

The AWS SAM CLI can automatically facilitate this process for a number of file types, AWS CloudFormation resource types, and AWS CloudFormation macros\.

### File types<a name="deploy-upload-local-files-use-types"></a>

Application files and Docker images are supported\.

### AWS CloudFormation resource types<a name="deploy-upload-local-files-use-resources"></a>

The following is a list of the supported resource types and their properties:


| Resource | Properties | 
| --- | --- | 
| AWS::ApiGateway::RestApi | BodyS3Location | 
| AWS::ApiGatewayV2::Api | BodyS3Location | 
| AWS::AppSync:FunctionConfiguration |  `CodeS3Location` `RequestMappingTemplateS3Location` `ResponseMappingTemplateS3Location`  | 
| AWS::AppSync::GraphQLSchema | DefinitionS3Location | 
| AWS::AppSync::Resolver |  `CodeS3Location` `RequestMappingTemplateS3Location` `ResponseMappingTemplateS3Location`  | 
| AWS::CloudFormation::ModuleVersion | ModulePackage | 
| AWS::CloudFormation::ResourceVersion | SchemaHandlerPackage | 
| AWS::ECR::Repository | RepositoryName | 
| AWS::ElasticBeanstalk::ApplicationVersion | SourceBundle | 
| AWS::Glue::Job | Command\.ScriptLocation | 
| AWS::Lambda::Function |  `Code` `Code.ImageUri`  | 
| AWS::Lambda::LayerVersion | Content | 
| AWS::Serverless::Api | DefinitionUri | 
| AWS::Serverless::Function |  `CodeUri` `ImageUri`  | 
| AWS::Serverless::HttpApi | DefinitionUri | 
| AWS::Serverless::LayerVersion | ContentUri | 
| AWS::Serverless::StateMachine | DefinitionUri | 
| AWS::StepFunctions::StateMachine | DefinitionS3Location | 

### AWS CloudFormation macros<a name="deploy-upload-local-files-use-macros"></a>

Files referenced using the `AWS::Include` transform macro are supported\.

## Learn more<a name="deploy-upload-local-files-learn"></a>

To learn more about the `AWS::Include` transform, see [ AWS::Include transform](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/create-reusable-transform-function-snippets-and-add-to-your-template-with-aws-include-transform.html) in the *AWS CloudFormation User Guide*\.

To see an example of using the `AWS::Include` transform in an AWS SAM template, see the [API Gateway HTTP API to SQS](https://serverlessland.com/patterns/apigw-sqs) pattern at * Serverless Land*\.