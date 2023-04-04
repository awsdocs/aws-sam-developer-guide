# Using sam deploy<a name="using-sam-cli-deploy"></a>

Use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam deploy` command to deploy your serverless application to the AWS Cloud\.
+ For an introduction to the AWS SAM CLI, see [What is the AWS SAM CLI?](what-is-sam.md#what-is-sam-cli)\.
+ For a list of `sam deploy` command options, see [sam deploy](sam-cli-command-reference-sam-deploy.md)\.
+ For an example of using `sam deploy` during a typical development workflow, see [Step 3: Deploy your application to the AWS Cloud](serverless-getting-started-hello-world.md#serverless-getting-started-hello-world-deploy)\.

**Topics**
+ [Prerequisites](#using-sam-cli-deploy-prerequisites)
+ [Deploying applications using sam deploy](#using-sam-cli-deploy-deploying)
+ [Best practices](#using-sam-cli-deploy-best)
+ [Options for sam deploy](#using-sam-cli-deploy-options)
+ [Troubleshooting](#using-sam-cli-deploy-troubleshooting)
+ [Examples](#using-sam-cli-deploy-examples)
+ [Learn more](#using-sam-cli-deploy-learn)

## Prerequisites<a name="using-sam-cli-deploy-prerequisites"></a>

To use `sam deploy`, install the AWS SAM CLI by completing the following:
+ [AWS SAM prerequisites](prerequisites.md)\.
+ [Installing the AWS SAM CLI](install-sam-cli.md)\.

Before using `sam deploy`, we recommend a basic understanding of the following:
+ [Configuring the AWS SAM CLI](using-sam-cli-configure.md)\.
+ [Using sam init](using-sam-cli-init.md)\.
+ [Using sam build](using-sam-cli-build.md)\.

## Deploying applications using sam deploy<a name="using-sam-cli-deploy-deploying"></a>

When you deploy a serverless application for the first time, use the `--guided` option\. The AWS SAM CLI will guide you through an interactive flow to configure your application’s deployment settings\.

**To deploy an application using the interactive flow**

1. Go to the root directory of your project\. This is the same location as your AWS SAM template\.

   ```
   $ cd sam-app
   ```

1. Run the following command:

   ```
   $ sam deploy --guided
   ```

1. During the interactive flow, the AWS SAM CLI prompts you with options to configure your application’s deployment settings\.

   Brackets \(`[ ]`\) indicate default values\. Leave your answer blank to select the default value\. Default values are obtained from the following configuration files:
   + `~/.aws/config` – Your general AWS account settings\.
   + `~/.aws/credentials` – Your AWS account credentials\.
   + `<project>/samconfig.toml` – Your project’s configuration file\.

   Provide values by answering the AWS SAM CLI prompts\. For example, you can enter `y` for **yes**, `n` for **no**, or string values\.

   The AWS SAM CLI writes your responses to your project’s `samconfig.toml` file\. For subsequent deployments, you can use `sam deploy` to deploy using these configured values\. To reconfigure these values, use `sam deploy --guided` again or directly modify your configuration files\.

   The following is an example output:

   ```
   sam-app $ sam deploy --guided
   
   Configuring SAM deploy
   ======================
   
           Looking for config file [samconfig.toml] :  Found
           Reading default arguments  :  Success
   
           Setting default arguments for 'sam deploy'
           =========================================
           Stack Name [sam-app]: ENTER
           AWS Region [us-west-2]: ENTER
           #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
           Confirm changes before deploy [Y/n]: ENTER
           #SAM needs permission to be able to create roles to connect to the resources in your template
           Allow SAM CLI IAM role creation [Y/n]: ENTER
           #Preserves the state of previously provisioned resources when an operation fails
           Disable rollback [y/N]: ENTER
           HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
           Save arguments to configuration file [Y/n]: ENTER
           SAM configuration file [samconfig.toml]: ENTER
           SAM configuration environment [default]: ENTER
   ```

1. Next, the AWS SAM CLI deploys your application to the AWS Cloud\. During deployment, progress is displayed in your command prompt\. The following are the major stages in deployment:
   + For applications with AWS Lambda functions packaged as a \.zip file archive, the AWS SAM CLI zips and uploads the package to an Amazon Simple Storage Service \(Amazon S3\) bucket\. If necessary, the AWS SAM CLI will create a new bucket\.
   + For applications with Lambda functions package as a container image, the AWS SAM CLI uploads the image to Amazon Elastic Container Registry \(Amazon ECR\)\. If necessary, the AWS SAM CLI will create a new repository\.
   + The AWS SAM CLI creates an AWS CloudFormation change set and deploys your application to AWS CloudFormation as a stack\.
   + The AWS SAM CLI modifies your deployed AWS SAM template with the new `CodeUri` value for your Lambda functions\.

   The following is an example of the AWS SAM CLI deployment output:

   ```
           Looking for resources needed for deployment:
   
           Managed S3 bucket: aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr
           A different default S3 bucket can be set in samconfig.toml and auto resolution of buckets turned off by setting resolve_s3=False
   
           Parameter "stack_name=sam-app" in [default.deploy.parameters] is defined as a global parameter [default.global.parameters].
           This parameter will be only saved under [default.global.parameters] in /Users/.../sam-app/samconfig.toml.
   
           Saved arguments to config file
           Running 'sam deploy' for future deployments will use the parameters saved above.
           The above parameters can be changed by modifying samconfig.toml
           Learn more about samconfig.toml syntax at 
           https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-config.html
   
           Uploading to sam-app-zip/da3c598813f1c2151579b73ad788cac8  262144 / 619839  (42.29%)Uploading to sam-app-zip/da3c598813f1c2151579b73ad788cac8  524288 / 619839  (84.58%)Uploading to sam-app-zip/da3c598813f1c2151579b73ad788cac8  619839 / 619839  (100.00%)
   
           Deploying with following values
           ===============================
           Stack name                   : sam-app
           Region                       : us-west-2
           Confirm changeset            : True
           Disable rollback             : False
           Deployment s3 bucket         : aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr
           Capabilities                 : ["CAPABILITY_IAM"]
           Parameter overrides          : {}
           Signing Profiles             : {}
   
   Initiating deployment
   =====================
   
           Uploading to sam-app-zip/be84c20f868068e4dc4a2c11966edf2d.template  1212 / 1212  (100.00%)
   
   
   Waiting for changeset to be created..
   
   CloudFormation stack changeset
   -------------------------------------------------------------------------------------------------
   Operation                LogicalResourceId        ResourceType             Replacement            
   -------------------------------------------------------------------------------------------------
   + Add                    HelloWorldFunctionHell   AWS::Lambda::Permissio   N/A                    
                            oWorldPermissionProd     n                                               
   + Add                    HelloWorldFunctionRole   AWS::IAM::Role           N/A                    
   + Add                    HelloWorldFunction       AWS::Lambda::Function    N/A                    
   + Add                    ServerlessRestApiDeplo   AWS::ApiGateway::Deplo   N/A                    
                            yment47fc2d5f9d          yment                                           
   + Add                    ServerlessRestApiProdS   AWS::ApiGateway::Stage   N/A                    
                            tage                                                                     
   + Add                    ServerlessRestApi        AWS::ApiGateway::RestA   N/A                    
                                                     pi                                              
   -------------------------------------------------------------------------------------------------
   
   
   Changeset created successfully. arn:aws:cloudformation:us-west-2:513423067560:changeSet/samcli-deploy1680559234/d9f58a77-98bc-41cd-b9f4-433a5a450d7a
   
   
   Previewing CloudFormation changeset before deployment
   ======================================================
   Deploy this changeset? [y/N]: y
   
   2023-04-03 12:00:50 - Waiting for stack create/update to complete
   
   CloudFormation events from stack operations (refresh every 5.0 seconds)
   -------------------------------------------------------------------------------------------------
   ResourceStatus           ResourceType             LogicalResourceId        ResourceStatusReason   
   -------------------------------------------------------------------------------------------------
   CREATE_IN_PROGRESS       AWS::IAM::Role           HelloWorldFunctionRole   -                      
   CREATE_IN_PROGRESS       AWS::IAM::Role           HelloWorldFunctionRole   Resource creation      
                                                                              Initiated              
   CREATE_COMPLETE          AWS::IAM::Role           HelloWorldFunctionRole   -                      
   CREATE_IN_PROGRESS       AWS::Lambda::Function    HelloWorldFunction       -                      
   CREATE_IN_PROGRESS       AWS::Lambda::Function    HelloWorldFunction       Resource creation      
                                                                              Initiated              
   CREATE_COMPLETE          AWS::Lambda::Function    HelloWorldFunction       -                      
   CREATE_IN_PROGRESS       AWS::ApiGateway::RestA   ServerlessRestApi        -                      
                            pi                                                                       
   CREATE_IN_PROGRESS       AWS::ApiGateway::RestA   ServerlessRestApi        Resource creation      
                            pi                                                Initiated              
   CREATE_COMPLETE          AWS::ApiGateway::RestA   ServerlessRestApi        -                      
                            pi                                                                       
   CREATE_IN_PROGRESS       AWS::Lambda::Permissio   HelloWorldFunctionHell   -                      
                            n                        oWorldPermissionProd                            
   CREATE_IN_PROGRESS       AWS::ApiGateway::Deplo   ServerlessRestApiDeplo   -                      
                            yment                    yment47fc2d5f9d                                 
   CREATE_IN_PROGRESS       AWS::Lambda::Permissio   HelloWorldFunctionHell   Resource creation      
                            n                        oWorldPermissionProd     Initiated              
   CREATE_IN_PROGRESS       AWS::ApiGateway::Deplo   ServerlessRestApiDeplo   Resource creation      
                            yment                    yment47fc2d5f9d          Initiated              
   CREATE_COMPLETE          AWS::ApiGateway::Deplo   ServerlessRestApiDeplo   -                      
                            yment                    yment47fc2d5f9d                                 
   CREATE_IN_PROGRESS       AWS::ApiGateway::Stage   ServerlessRestApiProdS   -                      
                                                     tage                                            
   CREATE_IN_PROGRESS       AWS::ApiGateway::Stage   ServerlessRestApiProdS   Resource creation      
                                                     tage                     Initiated              
   CREATE_COMPLETE          AWS::ApiGateway::Stage   ServerlessRestApiProdS   -                      
                                                     tage                                            
   CREATE_COMPLETE          AWS::Lambda::Permissio   HelloWorldFunctionHell   -                      
                            n                        oWorldPermissionProd                            
   CREATE_COMPLETE          AWS::CloudFormation::S   sam-app-zip              -                      
                            tack                                                                     
   -------------------------------------------------------------------------------------------------
   
   CloudFormation outputs from deployed stack
   -------------------------------------------------------------------------------------------------
   Outputs                                                                                         
   -------------------------------------------------------------------------------------------------
   Key                 HelloWorldFunctionIamRole                                                   
   Description         Implicit IAM Role created for Hello World function                          
   Value               arn:aws:iam::513423067560:role/sam-app-zip-                                 
   HelloWorldFunctionRole-11ZOGSCG28H0M                                                            
   
   Key                 HelloWorldApi                                                               
   Description         API Gateway endpoint URL for Prod stage for Hello World function            
   Value               https://njzfhdmls0.execute-api.us-west-2.amazonaws.com/Prod/hello/          
   
   Key                 HelloWorldFunction                                                          
   Description         Hello World Lambda Function ARN                                             
   Value               arn:aws:lambda:us-west-2:513423067560:function:sam-app-                 
   HelloWorldFunction-XPqNX4TBu7qn                                                                 
   -------------------------------------------------------------------------------------------------
   
   
   Successfully created/updated stack - sam-app-zip in us-west-2
   ```

1. To view your deployed application, do the following:

   1. Open the AWS CloudFormation console directly with the URL [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/)\.

   1. Select **Stacks**\.

   1. Identify your stack by application name and select it\.

### Verify changes before deployment<a name="using-sam-cli-deploy-deploying-changes"></a>

You can configure the AWS SAM CLI to display your AWS CloudFormation change set and ask for confirmation before deploying\.

**To confirm changes before deployment**

1. During `sam deploy --guided`, enter **Y** to confirm changes before deployment\.

   ```
   #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
   Confirm changes before deploy [Y/n]: Y
   ```

   Alternatively, you can modify your `samconfig.toml` file with the following:

   ```
   [default.deploy]
   [default.deploy.parameters]
   confirm_changeset = true
   ```

1. During deployment, the AWS SAM CLI will ask you to confirm changes before deployment\. The following is an example:

   ```
   Waiting for changeset to be created..
   
   CloudFormation stack changeset
   -------------------------------------------------------------------------------------------------
   Operation                LogicalResourceId        ResourceType             Replacement            
   -------------------------------------------------------------------------------------------------
   + Add                    HelloWorldFunctionHell   AWS::Lambda::Permissio   N/A                    
                            oWorldPermissionProd     n                                               
   + Add                    HelloWorldFunctionRole   AWS::IAM::Role           N/A                    
   + Add                    HelloWorldFunction       AWS::Lambda::Function    N/A                    
   + Add                    ServerlessRestApiDeplo   AWS::ApiGateway::Deplo   N/A                    
                            yment47fc2d5f9d          yment                                           
   + Add                    ServerlessRestApiProdS   AWS::ApiGateway::Stage   N/A                    
                            tage                                                                     
   + Add                    ServerlessRestApi        AWS::ApiGateway::RestA   N/A                    
                                                     pi                                              
   -------------------------------------------------------------------------------------------------
   
   Changeset created successfully. arn:aws:cloudformation:us-west-2:513423067560:changeSet/samcli-deploy1680559234/d9f58a77-98bc-41cd-b9f4-433a5a450d7a
   Previewing CloudFormation changeset before deployment
   ======================================================
   Deploy this changeset? [y/N]: y
   ```

### Specify additional parameters during deployment<a name="using-sam-cli-deploy-deploying-params"></a>

You can specify additional parameter values to configure when deploying\. You do this by modifying your AWS SAM template and configuring your parameter value during deployment\.

**To specify additional parameters**

1. Modify the `Parameters` section of your AWS SAM template\. The following is an example:

   ```
   AWSTemplateFormatVersion: '2010-09-09'
   Transform: AWS::Serverless-2016-10-31
   ...
   Globals:
   ...
   Parameters:
     DomainName:
       Type: String
       Default: example
       Description: Domain name
   ```

1. Run `sam deploy --guided`\. The following is an example output:

   ```
   sam-app $ sam deploy --guided
   
   Configuring SAM deploy
   ======================
   
           Looking for config file [samconfig.toml] :  Found
           Reading default arguments  :  Success
   
           Setting default arguments for 'sam deploy'
           =========================================
           Stack Name [sam-app-zip]: ENTER
           AWS Region [us-west-2]: ENTER
           Parameter DomainName [example]: ENTER
   ```

### Configure code signing for your Lambda functions<a name="using-sam-cli-deploy-deploying-signing"></a>

You can configure code signing for your Lambda functions at deployment\. You do this by modifying your AWS SAM template and configuring code signing during deployment\.

**To configure code signing**

1. Specify `CodeSigningConfigArn` in your AWS SAM template\. The following is an example:

   ```
   AWSTemplateFormatVersion: '2010-09-09'
   Transform: AWS::Serverless-2016-10-31
   ...
   Resources:
     HelloWorldFunction:
       Type: AWS::Serverless::Function
       Properties:
         CodeUri: hello_world/
         Handler: app.lambda_handler
         Runtime: python3.7
         CodeSigningConfigArn: arn:aws:lambda:us-east-1:111122223333:code-signing-config:csc-12e12345db1234567
   ```

1. Run `sam deploy --guided`\. The AWS SAM CLI will prompt you to configure code signing\. The following is an example output:

   ```
   #Found code signing configurations in your function definitions
   Do you want to sign your code? [Y/n]: ENTER
   #Please provide signing profile details for the following functions & layers
   #Signing profile details for function 'HelloWorld'
   Signing Profile Name: 
   Signing Profile Owner Account ID (optional):
   #Signing profile details for layer 'MyLayer', which is used by functions {'HelloWorld'}
   Signing Profile Name: 
   Signing Profile Owner Account ID (optional):
   ```

## Best practices<a name="using-sam-cli-deploy-best"></a>
+ When using `sam deploy`, the AWS SAM CLI deploys your application’s build artifacts located in the `.aws-sam` directory\. When you make changes to your application's original files, run `sam build` to update the `.aws-sam` directory before deploying\.
+ When deploying an application for the first time, use `sam deploy --guided` to configure deployment settings\. For subsequent deployments, you can use `sam deploy` to deploy with your configured settings\.

## Options for sam deploy<a name="using-sam-cli-deploy-options"></a>

The following are commonly used options for `sam deploy`\. For a list of all options, see [sam deploy](sam-cli-command-reference-sam-deploy.md)\.

### Use the guided interactive flow to deploy your application<a name="using-sam-cli-deploy-options-guided"></a>

Use the `--guided` option to configure your application’s deployment settings through an interactive flow\. The following is an example:

```
$ sam deploy --guided
```

Your application’s deployment settings are saved in your project’s `samconfig.toml` file\. For a description of the values set by the AWS SAM CLI, see [Using the AWS SAM CLI with configuration files](using-sam-cli-configure.md#using-sam-cli-configure-cli)\.

## Troubleshooting<a name="using-sam-cli-deploy-troubleshooting"></a>

To troubleshoot the AWS SAM CLI, see [AWS SAM CLI troubleshooting](sam-cli-troubleshooting.md)\.

## Examples<a name="using-sam-cli-deploy-examples"></a>

### Deploy a Hello World application that contains a Lambda function packaged as a \.zip file archive<a name="using-sam-cli-deploy-examples-example1"></a>

For an example, see [Step 3: Deploy your application to the AWS Cloud](serverless-getting-started-hello-world.md#serverless-getting-started-hello-world-deploy) in the Hello World application tutorial\.

### Deploy a Hello World application that contains a Lambda function packaged as a container image<a name="using-sam-cli-deploy-examples-example2"></a>

First, we use `sam init` to create our Hello World application\. During the interactive flow, we choose the `Python3.9` runtime and `Image` package type\.

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

Use the most popular runtime and package type? (Python and zip) [y/N]:  ENTER

Which runtime would you like to use?
        1 - aot.dotnet7 (provided.al2)
        ...
        15 - nodejs12.x
        16 - python3.9
        17 - python3.8
        ...
Runtime: 16

What package type would you like to use?
        1 - Zip
        2 - Image
Package type: 2

Based on your selections, the only dependency manager available is pip.
We will proceed copying the template using pip.
...
Project name [sam-app]: ENTER

    -----------------------
    Generating application:
    -----------------------
    Name: sam-app
    Base Image: amazon/python3.9-base
    Architectures: x86_64
    Dependency Manager: pip
    Output Directory: .
    Configuration file: sam-app/samconfig.toml

    Next steps can be found in the README file at sam-app/README.md
...
```

Next, we `cd` to the root directory of our project and run `sam build`\. The AWS SAM CLI builds our Lambda function locally using Docker\.

```
sam-app $ sam build
Building codeuri: /Users/.../sam-app runtime: None metadata: {'Dockerfile': 'Dockerfile', 'DockerContext': '/Users/.../sam-app/hello_world', 'DockerTag': 'python3.9-v1'} architecture: x86_64 functions: HelloWorldFunction
Building image for HelloWorldFunction function
Setting DockerBuildArgs: {} for HelloWorldFunction function
Step 1/5 : FROM public.ecr.aws/lambda/python:3.9
 ---> 0a5e3da309aa
Step 2/5 : COPY requirements.txt ./
 ---> abc4e82e85f9
Step 3/5 : RUN python3.9 -m pip install -r requirements.txt -t .
 ---> [Warning] The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
 ---> Running in 43845e7aa22d
Collecting requests
  Downloading requests-2.28.2-py3-none-any.whl (62 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.8/62.8 KB 829.5 kB/s eta 0:00:00
Collecting idna<4,>=2.5
  Downloading idna-3.4-py3-none-any.whl (61 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.5/61.5 KB 2.4 MB/s eta 0:00:00
Collecting charset-normalizer<4,>=2
  Downloading charset_normalizer-3.1.0-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (199 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 199.2/199.2 KB 2.1 MB/s eta 0:00:00
Collecting certifi>=2017.4.17
  Downloading certifi-2022.12.7-py3-none-any.whl (155 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 155.3/155.3 KB 10.2 MB/s eta 0:00:00
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.15-py2.py3-none-any.whl (140 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 140.9/140.9 KB 9.1 MB/s eta 0:00:00
Installing collected packages: urllib3, idna, charset-normalizer, certifi, requests
Successfully installed certifi-2022.12.7 charset-normalizer-3.1.0 idna-3.4 requests-2.28.2 urllib3-1.26.15
Removing intermediate container 43845e7aa22d
 ---> cab8ace899ce
Step 4/5 : COPY app.py ./
 ---> 4146f3cd69f2
Step 5/5 : CMD ["app.lambda_handler"]
 ---> [Warning] The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
 ---> Running in f4131ddffb31
Removing intermediate container f4131ddffb31
 ---> d2f5180b2154
Successfully built d2f5180b2154
Successfully tagged helloworldfunction:python3.9-v1


Build Succeeded

Built Artifacts  : .aws-sam/build
Built Template   : .aws-sam/build/template.yaml

Commands you can use next
=========================
[*] Validate SAM template: sam validate
[*] Invoke Function: sam local invoke
[*] Test Function in the Cloud: sam sync --stack-name {{stack-name}} --watch
[*] Deploy: sam deploy --guided
```

Next, we run `sam deploy --guided` to deploy our application\. The AWS SAM CLI guides us through configuring our deployment settings\. Then, the AWS SAM CLI deploys our application to the AWS Cloud\.

```
sam-app $ sam deploy --guided

Configuring SAM deploy
======================

        Looking for config file [samconfig.toml] :  Found
        Reading default arguments  :  Success

        Setting default arguments for 'sam deploy'
        =========================================
        Stack Name [sam-app]: ENTER
        AWS Region [us-west-2]: ENTER
        #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
        Confirm changes before deploy [Y/n]: ENTER
        #SAM needs permission to be able to create roles to connect to the resources in your template
        Allow SAM CLI IAM role creation [Y/n]: ENTER
        #Preserves the state of previously provisioned resources when an operation fails
        Disable rollback [y/N]: ENTER
        HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
        Save arguments to configuration file [Y/n]: ENTER
        SAM configuration file [samconfig.toml]: ENTER
        SAM configuration environment [default]: ENTER

        Looking for resources needed for deployment:

        Managed S3 bucket: aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr
        A different default S3 bucket can be set in samconfig.toml and auto resolution of buckets turned off by setting resolve_s3=False

        Parameter "stack_name=sam-app" in [default.deploy.parameters] is defined as a global parameter [default.global.parameters].
        This parameter will be only saved under [default.global.parameters] in /Users/.../sam-app/samconfig.toml.

        Saved arguments to config file
        Running 'sam deploy' for future deployments will use the parameters saved above.
        The above parameters can be changed by modifying samconfig.toml
        Learn more about samconfig.toml syntax at 
        https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-config.html

e95fc5e75742: Pushed 
d8df51e7bdd7: Pushed 
b1d0d7e0b34a: Pushed 
0071317b94d8: Pushed 
d98f98baf147: Pushed 
2d244e0816c6: Pushed 
eb2eeb1ebe42: Pushed 
a5ca065a3279: Pushed 
fe9e144829c9: Pushed 
helloworldfunction-d2f5180b2154-python3.9-v1: digest: sha256:cceb71401b47dc3007a7a1e1f2e0baf162999e0e6841d15954745ecc0c447533 size: 2206

        Deploying with following values
        ===============================
        Stack name                   : sam-app
        Region                       : us-west-2
        Confirm changeset            : True
        Disable rollback             : False
        Deployment image repository  : 
                                       {
                                           "HelloWorldFunction": "513423067560.dkr.ecr.us-west-2.amazonaws.com/samapp7427b055/helloworldfunction19d43fc4repo"
                                       }
        Deployment s3 bucket         : aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr
        Capabilities                 : ["CAPABILITY_IAM"]
        Parameter overrides          : {}
        Signing Profiles             : {}

Initiating deployment
=====================

HelloWorldFunction may not have authorization defined.
        Uploading to sam-app/682ad27c7cf7a17c7f77a1688b0844f2.template  1328 / 1328  (100.00%)


Waiting for changeset to be created..

CloudFormation stack changeset
-------------------------------------------------------------------------------------------------
Operation                LogicalResourceId        ResourceType             Replacement            
-------------------------------------------------------------------------------------------------
+ Add                    HelloWorldFunctionHell   AWS::Lambda::Permissio   N/A                    
                         oWorldPermissionProd     n                                               
+ Add                    HelloWorldFunctionRole   AWS::IAM::Role           N/A                    
+ Add                    HelloWorldFunction       AWS::Lambda::Function    N/A                    
+ Add                    ServerlessRestApiDeplo   AWS::ApiGateway::Deplo   N/A                    
                         yment47fc2d5f9d          yment                                           
+ Add                    ServerlessRestApiProdS   AWS::ApiGateway::Stage   N/A                    
                         tage                                                                     
+ Add                    ServerlessRestApi        AWS::ApiGateway::RestA   N/A                    
                                                  pi                                              
-------------------------------------------------------------------------------------------------


Changeset created successfully. arn:aws:cloudformation:us-west-2:513423067560:changeSet/samcli-deploy1680634124/0ffd4faf-2e2b-487e-b9e0-9116e8299ac4


Previewing CloudFormation changeset before deployment
======================================================
Deploy this changeset? [y/N]: y

2023-04-04 08:49:15 - Waiting for stack create/update to complete

CloudFormation events from stack operations (refresh every 5.0 seconds)
-------------------------------------------------------------------------------------------------
ResourceStatus           ResourceType             LogicalResourceId        ResourceStatusReason   
-------------------------------------------------------------------------------------------------
CREATE_IN_PROGRESS       AWS::CloudFormation::S   sam-app                  User Initiated         
                         tack                                                                     
CREATE_IN_PROGRESS       AWS::IAM::Role           HelloWorldFunctionRole   -                      
CREATE_IN_PROGRESS       AWS::IAM::Role           HelloWorldFunctionRole   Resource creation      
                                                                           Initiated              
CREATE_COMPLETE          AWS::IAM::Role           HelloWorldFunctionRole   -                      
CREATE_IN_PROGRESS       AWS::Lambda::Function    HelloWorldFunction       -                      
CREATE_IN_PROGRESS       AWS::Lambda::Function    HelloWorldFunction       Resource creation      
                                                                           Initiated              
CREATE_COMPLETE          AWS::Lambda::Function    HelloWorldFunction       -                      
CREATE_IN_PROGRESS       AWS::ApiGateway::RestA   ServerlessRestApi        -                      
                         pi                                                                       
CREATE_IN_PROGRESS       AWS::ApiGateway::RestA   ServerlessRestApi        Resource creation      
                         pi                                                Initiated              
CREATE_COMPLETE          AWS::ApiGateway::RestA   ServerlessRestApi        -                      
                         pi                                                                       
CREATE_IN_PROGRESS       AWS::Lambda::Permissio   HelloWorldFunctionHell   -                      
                         n                        oWorldPermissionProd                            
CREATE_IN_PROGRESS       AWS::ApiGateway::Deplo   ServerlessRestApiDeplo   -                      
                         yment                    yment47fc2d5f9d                                 
CREATE_IN_PROGRESS       AWS::Lambda::Permissio   HelloWorldFunctionHell   Resource creation      
                         n                        oWorldPermissionProd     Initiated              
CREATE_IN_PROGRESS       AWS::ApiGateway::Deplo   ServerlessRestApiDeplo   Resource creation      
                         yment                    yment47fc2d5f9d          Initiated              
CREATE_COMPLETE          AWS::ApiGateway::Deplo   ServerlessRestApiDeplo   -                      
                         yment                    yment47fc2d5f9d                                 
CREATE_IN_PROGRESS       AWS::ApiGateway::Stage   ServerlessRestApiProdS   -                      
                                                  tage                                            
CREATE_IN_PROGRESS       AWS::ApiGateway::Stage   ServerlessRestApiProdS   Resource creation      
                                                  tage                     Initiated              
CREATE_COMPLETE          AWS::ApiGateway::Stage   ServerlessRestApiProdS   -                      
                                                  tage                                            
CREATE_COMPLETE          AWS::Lambda::Permissio   HelloWorldFunctionHell   -                      
                         n                        oWorldPermissionProd                            
CREATE_COMPLETE          AWS::CloudFormation::S   sam-app                  -                      
                         tack                                                                     
-------------------------------------------------------------------------------------------------

CloudFormation outputs from deployed stack
-------------------------------------------------------------------------------------------------
Outputs                                                                                         
-------------------------------------------------------------------------------------------------
Key                 HelloWorldFunctionIamRole                                                   
Description         Implicit IAM Role created for Hello World function                          
Value               arn:aws:iam::513423067560:role/sam-app-HelloWorldFunctionRole-JFML1JOKHJ71  

Key                 HelloWorldApi                                                               
Description         API Gateway endpoint URL for Prod stage for Hello World function            
Value               https://endlwiqqod.execute-api.us-west-2.amazonaws.com/Prod/hello/          

Key                 HelloWorldFunction                                                          
Description         Hello World Lambda Function ARN                                             
Value               arn:aws:lambda:us-west-2:513423067560:function:sam-app-HelloWorldFunction-  
kyg6Y2iNRUPg                                                                                    
-------------------------------------------------------------------------------------------------


Successfully created/updated stack - sam-app in us-west-2
```

## Learn more<a name="using-sam-cli-deploy-learn"></a>

To learn more about using the AWS SAM CLI `sam deploy` command, see the following:
+ **[The Complete AWS SAM Workshop: Module 3 \- Deploy manually](https://s12d.com/sam-ws-en-manual-deploy)** – Learn how to build, package, and deploy a serverless application using the AWS SAM CLI\.