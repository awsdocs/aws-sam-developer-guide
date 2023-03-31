# Using sam sync<a name="using-sam-cli-sync"></a>

The AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) `sam sync` command provides options to quickly sync local application changes to the AWS Cloud\. Use `sam sync` when developing your applications to:

1. Automatically detect and sync local changes to the AWS Cloud\.

1. Customize what local changes are synced to the AWS Cloud\.

1. Prepare your application in the cloud for testing and validation\.

With `sam sync`, you can create a rapid development workflow that shortens the time it takes to sync your local changes to the cloud for testing and validation\.

**Note**  
The `sam sync` command is recommended for development environments\. For production environments, we recommend using `sam deploy` or configuring a *continuous integration and delivery \(CI/CD\)* pipeline\. To learn more, see [Deploying serverless applications](serverless-deploying.md)\.

The `sam sync` command is a part of AWS SAM Accelerate\. *AWS SAM Accelerate* provides tools that you can use to speed up the experience of developing and testing serverless applications in the AWS Cloud\.

**Topics**
+ [Automatically detect and sync local changes to the AWS Cloud](#using-sam-cli-sync-auto)
+ [Customize what local changes are synced to the AWS Cloud](#using-sam-cli-sync-customize)
+ [Prepare your application in the cloud for testing and validation](#using-sam-cli-sync-test)
+ [Options for the sam sync command](#using-sam-cli-sync-options)
+ [Examples](#using-sam-cli-sync-examples)
+ [Learn more](#using-sam-cli-sync-learn)

## Automatically detect and sync local changes to the AWS Cloud<a name="using-sam-cli-sync-auto"></a>

Run `sam sync` with the `--watch` option to begin syncing your application to the AWS Cloud\. This does the following:

1. **Build your application ** – This process is similar to using the `sam build` command\.

1. **Deploy your application** – The AWS SAM CLI deploys your application to AWS CloudFormation using your default settings\. The following default values are used:

   1. AWS credentials and general configuration settings found in your `.aws` user folder\.

   1. Application deployment settings found in your application’s `samconfig.toml` file\.

   If default values can’t be found, the AWS SAM CLI will inform you and exit the sync process\.

1. **Watch for local changes** – The AWS SAM CLI remains running and watches for local changes to your application\. This is what the `--watch` option provides\.

   This option may be turned on by default\. For default values, see your application’s `samconfig.toml` file\. The following is an example file:

   ```
   ...
   [default.sync]
   [default.sync.parameters]
   watch = true
   ...
   ```

1. **Sync local changes to the AWS Cloud** – When you make local changes, the AWS SAM CLI detects and syncs those changes to the AWS Cloud through the quickest method available\. Depending on the type of change, the following may occur:

   1. If your updated resource supports AWS service APIs, the AWS SAM CLI will use it to deploy your changes\. This results in a quick sync to update your resource in the AWS Cloud\.

   1. If your updated resource doesn’t support AWS service APIs, the AWS SAM CLI will perform an AWS CloudFormation deployment\. This updates your entire application in the AWS Cloud\. While not as quick, it does prevent you from having to manually initiate a deployment\.

Since the `sam sync` command automatically updates your application in the AWS Cloud, it is recommended for development environments only\. When you run `sam sync`, you will be asked to confirm:

```
**The sync command should only be used against a development stack**.

Confirm that you are synchronizing a development stack.

Enter Y to proceed with the command, or enter N to cancel:
 [Y/n]: ENTER
```

## Customize what local changes are synced to the AWS Cloud<a name="using-sam-cli-sync-customize"></a>

Provide options to customize what local changes are synced to the AWS Cloud\. This can speed up the time it takes to see your local changes in the cloud for testing and validation\.

For example, provide the `--code` option to sync only code changes, such as AWS Lambda function code\. During development, if you are focused specifically on Lambda code, this will get your changes into the cloud quickly for testing and validation\. The following is an example:

```
$ sam sync --code --watch
```

To sync only code changes for a specific Lambda function or layer, use the `--resource-id` option\. The following is an example:

```
$ sam sync --code --resource-id HelloWorldFunction --resource-id HelloWorldLayer
```

## Prepare your application in the cloud for testing and validation<a name="using-sam-cli-sync-test"></a>

The `sam sync` command automatically finds the quickest method available to update your application in the AWS Cloud\. This can speed up your development and cloud testing workflows\. By utilizing AWS service APIs, you can quickly develop, sync, and test supported resources\. For a hands\-on example, see [Module 6 \- AWS SAM Accelerate](https://s12d.com/sam-ws-en-accelerate) in *The Complete AWS SAM Workshop*\.

## Options for the sam sync command<a name="using-sam-cli-sync-options"></a>

The following are some of the main options you can use to modify the `sam sync` command\. For a list of all options, see [sam sync](sam-cli-command-reference-sam-sync.md)\.

### Perform a one\-time AWS CloudFormation deployment<a name="using-sam-cli-sync-options-single-deploy"></a>

Use the `--no-watch` option to turn off automatic syncing\. The following is an example:

```
$ sam sync --no-watch
```

The AWS SAM CLI will perform a one\-time AWS CloudFormation deployment\. This command groups together the actions performed by the `sam build` and `sam deploy` commands\.

### Skip the initial AWS CloudFormation deployment<a name="using-sam-cli-sync-options-skip-deploy-sync"></a>

You can customize whether an AWS CloudFormation deployment is required each time `sam sync` is run\.
+ Provide `--no-skip-deploy-sync` to require an AWS CloudFormation deployment each time `sam sync` is run\. This ensures that your local infrastructure is synced to AWS CloudFormation, preventing drift\. Using this option does add additional time to your development and testing workflow\.
+ Provide `--skip-deploy-sync` to make AWS CloudFormation deployment optional\. The AWS SAM CLI will compare your local AWS SAM template with your deployed AWS CloudFormation template and will skip the initial AWS CloudFormation deployment if a change isn't detected\. Skipping AWS CloudFormation deployment can save you time when syncing local changes to the AWS Cloud\.

  If no change is detected, the AWS SAM CLI will still perform an AWS CloudFormation deployment in the following scenarios:
  + If its been 7 days or more since your last AWS CloudFormation deployment\.
  + If a large number of Lambda function code changes are detected, making AWS CloudFormation deployment the quickest method to update your application\.

The following is an example:

```
$ sam sync --skip-deploy-sync
```

### Sync a resource from a nested stack<a name="using-sam-sync-options-nested-stack"></a>

**To sync a resource from a nested stack**

1. Provide the root stack using `--stack-name`\.

1. Identify the resource in the nested stack using the following format: `nestedStackId/resourceId`\.

1. Provide the resource in the nested stack using `--resource-id`\.

   The following is an example:

   ```
   $ sam sync --code --stack-name sam-app --resource-id myNestedStack/HelloWorldFunction
   ```

For more information about creating nested applications, see [Using nested applications](serverless-sam-template-nested-applications.md)\.

### Specify a specific AWS CloudFormation stack to update<a name="using-sam-sync-options-stack-name"></a>

To specify a specific AWS CloudFormation stack to update, provide the `--stack-name` option\. The following is an example:

```
$ sam sync --stack-name dev-sam-app
```

## Examples<a name="using-sam-cli-sync-examples"></a>

### Using sam sync to update the Hello World application<a name="using-sam-cli-sync-examples-example1"></a>

In this example, we start by initializing the sample Hello World application\. To learn more about this application, see [Tutorial: Deploying a Hello World application](serverless-getting-started-hello-world.md)\.

Running `sam sync` begins the build and deployment process\.

```
$ sam sync
				
The SAM CLI will use the AWS Lambda, Amazon API Gateway, and AWS StepFunctions APIs to upload your code without
performing a CloudFormation deployment. This will cause drift in your CloudFormation stack.
**The sync command should only be used against a development stack**.

Confirm that you are synchronizing a development stack.

Enter Y to proceed with the command, or enter N to cancel:
 [Y/n]:
Queued infra sync. Waiting for in progress code syncs to complete...
Starting infra sync.
Manifest file is changed (new hash: 3298f13049d19cffaa37ca931dd4d421) or dependency folder (.aws-sam/deps/0663e6fe-a888-4efb-b908-e2344261e9c7) is missing for (HelloWorldFunction), downloading dependencies and copying/building source
Building codeuri: /Users/.../Demo/sync/sam-app/hello_world runtime: python3.9 metadata: {} architecture: x86_64 functions: HelloWorldFunction
Running PythonPipBuilder:CleanUp
Running PythonPipBuilder:ResolveDependencies
Running PythonPipBuilder:CopySource

Build Succeeded

Successfully packaged artifacts and wrote output template to file /var/folders/45/5ct135bx3fn2551_ptl5g6_80000gr/T/tmpx_5t4u3f.
Execute the following command to deploy the packaged template
sam deploy --template-file /var/folders/45/5ct135bx3fn2551_ptl5g6_80000gr/T/tmpx_5t4u3f --stack-name <YOUR STACK NAME>


    Deploying with following values
    ===============================
    Stack name                   : sam-app
    Region                       : us-west-2
    Disable rollback             : False
    Deployment s3 bucket         : aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr
    Capabilities                 : ["CAPABILITY_NAMED_IAM", "CAPABILITY_AUTO_EXPAND"]
    Parameter overrides          : {}
    Signing Profiles             : null

Initiating deployment
=====================


2023-03-17 11:17:19 - Waiting for stack create/update to complete

CloudFormation events from stack operations (refresh every 0.5 seconds)
---------------------------------------------------------------------------------------------------------------------------------------------
ResourceStatus                      ResourceType                        LogicalResourceId                   ResourceStatusReason
---------------------------------------------------------------------------------------------------------------------------------------------
CREATE_IN_PROGRESS                  AWS::CloudFormation::Stack          sam-app                             Transformation succeeded
CREATE_IN_PROGRESS                  AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   -
                                                                        ack
CREATE_IN_PROGRESS                  AWS::IAM::Role                      HelloWorldFunctionRole              -
CREATE_IN_PROGRESS                  AWS::IAM::Role                      HelloWorldFunctionRole              Resource creation Initiated
CREATE_IN_PROGRESS                  AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   Resource creation Initiated
                                                                        ack
CREATE_COMPLETE                     AWS::IAM::Role                      HelloWorldFunctionRole              -
CREATE_COMPLETE                     AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   -
                                                                        ack
CREATE_IN_PROGRESS                  AWS::Lambda::Function               HelloWorldFunction                  -
CREATE_IN_PROGRESS                  AWS::Lambda::Function               HelloWorldFunction                  Resource creation Initiated
CREATE_COMPLETE                     AWS::Lambda::Function               HelloWorldFunction                  -
CREATE_IN_PROGRESS                  AWS::ApiGateway::RestApi            ServerlessRestApi                   -
CREATE_IN_PROGRESS                  AWS::ApiGateway::RestApi            ServerlessRestApi                   Resource creation Initiated
CREATE_COMPLETE                     AWS::ApiGateway::RestApi            ServerlessRestApi                   -
CREATE_IN_PROGRESS                  AWS::ApiGateway::Deployment         ServerlessRestApiDeployment47fc2d   -
                                                                        5f9d
CREATE_IN_PROGRESS                  AWS::Lambda::Permission             HelloWorldFunctionHelloWorldPermi   -
                                                                        ssionProd
CREATE_IN_PROGRESS                  AWS::Lambda::Permission             HelloWorldFunctionHelloWorldPermi   Resource creation Initiated
                                                                        ssionProd
CREATE_IN_PROGRESS                  AWS::ApiGateway::Deployment         ServerlessRestApiDeployment47fc2d   Resource creation Initiated
                                                                        5f9d
CREATE_COMPLETE                     AWS::ApiGateway::Deployment         ServerlessRestApiDeployment47fc2d   -
                                                                        5f9d
CREATE_IN_PROGRESS                  AWS::ApiGateway::Stage              ServerlessRestApiProdStage          -
CREATE_IN_PROGRESS                  AWS::ApiGateway::Stage              ServerlessRestApiProdStage          Resource creation Initiated
CREATE_COMPLETE                     AWS::ApiGateway::Stage              ServerlessRestApiProdStage          -
CREATE_COMPLETE                     AWS::Lambda::Permission             HelloWorldFunctionHelloWorldPermi   -
                                                                        ssionProd
CREATE_COMPLETE                     AWS::CloudFormation::Stack          sam-app                             -
---------------------------------------------------------------------------------------------------------------------------------------------

CloudFormation outputs from deployed stack
----------------------------------------------------------------------------------------------------------------------------------------------
Outputs
----------------------------------------------------------------------------------------------------------------------------------------------
Key                 HelloWorldFunctionIamRole
Description         Implicit IAM Role created for Hello World function
Value               arn:aws:iam::513423067560:role/sam-app-HelloWorldFunctionRole-BUFVMO2PJIYF

Key                 HelloWorldApi
Description         API Gateway endpoint URL for Prod stage for Hello World function
Value               https://pcrx5gdaof.execute-api.us-west-2.amazonaws.com/Prod/hello/

Key                 HelloWorldFunction
Description         Hello World Lambda Function ARN
Value               arn:aws:lambda:us-west-2:513423067560:function:sam-app-HelloWorldFunction-2PlN6TPTQoco
----------------------------------------------------------------------------------------------------------------------------------------------
Stack creation succeeded. Sync infra completed.

Infra sync completed.
CodeTrigger not created as CodeUri or DefinitionUri is missing for ServerlessRestApi.
```

Once deployment is complete, we modify the `HelloWorldFunction` code\. The AWS SAM CLI detects this change and syncs our application to the AWS Cloud\. Since AWS Lambda supports AWS service APIs, a quick sync is performed\.

```
Syncing Lambda Function HelloWorldFunction...
Manifest is not changed for (HelloWorldFunction), running incremental build
Building codeuri: /Users/.../Demo/sync/sam-app/hello_world runtime: python3.9 metadata: {} architecture: x86_64 functions: HelloWorldFunction
Running PythonPipBuilder:CopySource
Finished syncing Lambda Function HelloWorldFunction.
```

Next, we modify our API endpoint in the application’s AWS SAM template\. We change `/hello` to `/helloworld`\.

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
...
Resources:
  HelloWorldFunction:
    ...
    Properties:
      ...
      Events:
        HelloWorld:
          Type: Api
          Properties:
            Path: /helloworld
            Method: get
```

Since the Amazon API Gateway resource doesn’t support the AWS service API, the AWS SAM CLI automatically performs an AWS CloudFormation deployment\. The following is an example output:

```
Queued infra sync. Waiting for in progress code syncs to complete...
Starting infra sync.
Manifest is not changed for (HelloWorldFunction), running incremental build
Building codeuri: /Users/.../Demo/sync/sam-app/hello_world runtime: python3.9 metadata: {} architecture: x86_64 functions: HelloWorldFunction
Running PythonPipBuilder:CopySource

Build Succeeded

Successfully packaged artifacts and wrote output template to file /var/folders/45/5ct135bx3fn2551_ptl5g6_80000gr/T/tmpuabo0jb9.
Execute the following command to deploy the packaged template
sam deploy --template-file /var/folders/45/5ct135bx3fn2551_ptl5g6_80000gr/T/tmpuabo0jb9 --stack-name <YOUR STACK NAME>


    Deploying with following values
    ===============================
    Stack name                   : sam-app
    Region                       : us-west-2
    Disable rollback             : False
    Deployment s3 bucket         : aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr
    Capabilities                 : ["CAPABILITY_NAMED_IAM", "CAPABILITY_AUTO_EXPAND"]
    Parameter overrides          : {}
    Signing Profiles             : null

Initiating deployment
=====================


2023-03-17 14:41:18 - Waiting for stack create/update to complete

CloudFormation events from stack operations (refresh every 0.5 seconds)
---------------------------------------------------------------------------------------------------------------------------------------------
ResourceStatus                      ResourceType                        LogicalResourceId                   ResourceStatusReason
---------------------------------------------------------------------------------------------------------------------------------------------
UPDATE_IN_PROGRESS                  AWS::CloudFormation::Stack          sam-app                             Transformation succeeded
UPDATE_IN_PROGRESS                  AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   -
                                                                        ack
UPDATE_COMPLETE                     AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   -
                                                                        ack
UPDATE_IN_PROGRESS                  AWS::ApiGateway::RestApi            ServerlessRestApi                   -
UPDATE_COMPLETE                     AWS::ApiGateway::RestApi            ServerlessRestApi                   -
CREATE_IN_PROGRESS                  AWS::ApiGateway::Deployment         ServerlessRestApiDeployment8cf30e   -
                                                                        d3cd
UPDATE_IN_PROGRESS                  AWS::Lambda::Permission             HelloWorldFunctionHelloWorldPermi   Requested update requires the
                                                                        ssionProd                           creation of a new physical
                                                                                                            resource; hence creating one.
UPDATE_IN_PROGRESS                  AWS::Lambda::Permission             HelloWorldFunctionHelloWorldPermi   Resource creation Initiated
                                                                        ssionProd
CREATE_IN_PROGRESS                  AWS::ApiGateway::Deployment         ServerlessRestApiDeployment8cf30e   Resource creation Initiated
                                                                        d3cd
CREATE_COMPLETE                     AWS::ApiGateway::Deployment         ServerlessRestApiDeployment8cf30e   -
                                                                        d3cd
UPDATE_IN_PROGRESS                  AWS::ApiGateway::Stage              ServerlessRestApiProdStage          -
UPDATE_COMPLETE                     AWS::ApiGateway::Stage              ServerlessRestApiProdStage          -
UPDATE_COMPLETE                     AWS::Lambda::Permission             HelloWorldFunctionHelloWorldPermi   -
                                                                        ssionProd
UPDATE_COMPLETE_CLEANUP_IN_PROGRE   AWS::CloudFormation::Stack          sam-app                             -
SS
DELETE_IN_PROGRESS                  AWS::Lambda::Permission             HelloWorldFunctionHelloWorldPermi   -
                                                                        ssionProd
DELETE_IN_PROGRESS                  AWS::ApiGateway::Deployment         ServerlessRestApiDeployment47fc2d   -
                                                                        5f9d
DELETE_COMPLETE                     AWS::ApiGateway::Deployment         ServerlessRestApiDeployment47fc2d   -
                                                                        5f9d
UPDATE_COMPLETE                     AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   -
                                                                        ack
DELETE_COMPLETE                     AWS::Lambda::Permission             HelloWorldFunctionHelloWorldPermi   -
                                                                        ssionProd
UPDATE_COMPLETE                     AWS::CloudFormation::Stack          sam-app                             -
---------------------------------------------------------------------------------------------------------------------------------------------

CloudFormation outputs from deployed stack
----------------------------------------------------------------------------------------------------------------------------------------------
Outputs
----------------------------------------------------------------------------------------------------------------------------------------------
Key                 HelloWorldFunctionIamRole
Description         Implicit IAM Role created for Hello World function
Value               arn:aws:iam::513423067560:role/sam-app-HelloWorldFunctionRole-BUFVMO2PJIYF

Key                 HelloWorldApi
Description         API Gateway endpoint URL for Prod stage for Hello World function
Value               https://pcrx5gdaof.execute-api.us-west-2.amazonaws.com/Prod/hello/

Key                 HelloWorldFunction
Description         Hello World Lambda Function ARN
Value               arn:aws:lambda:us-west-2:513423067560:function:sam-app-HelloWorldFunction-2PlN6TPTQoco
----------------------------------------------------------------------------------------------------------------------------------------------


Stack update succeeded. Sync infra completed.

Infra sync completed.
```

## Learn more<a name="using-sam-cli-sync-learn"></a>

For a description of all `sam sync` options, see [sam sync](sam-cli-command-reference-sam-sync.md)\.