# Tutorial: Deploying a Hello World application<a name="serverless-getting-started-hello-world"></a>

In this tutorial, you use the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) to complete the following:
+ Initialize, build, and deploy a sample **Hello World** application\.
+ Make local changes and sync to AWS CloudFormation\.
+ Test your application in the AWS Cloud\.
+ Optionally, perform local testing on your development host\.
+ Delete the sample application from the AWS Cloud\.

The sample **Hello World** application implements a basic API backend\. It consists of the following resources:
+ **Amazon API Gateway** – API endpoint that you will use to invoke your function\.
+ **AWS Lambda** – Function that processes the HTTP API GET request and returns a `hello world` message\.
+ **AWS Identity and Access Management \(IAM\) role** – Provisions permissions for the services to securely interact\.

The following diagram shows the components of this application:

![\[A diagram of a Lambda function that's invoked when you send a GET request to the API Gateway endpoint.\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/images/gs-01.png)

**Topics**
+ [Prerequisites](#serverless-getting-started-hello-world-prerequisites)
+ [Step 1: Initialize the sample Hello World application](#serverless-getting-started-hello-world-init)
+ [Step 2: Build your application](#serverless-getting-started-hello-world-build)
+ [Step 3: Deploy your application to the AWS Cloud](#serverless-getting-started-hello-world-deploy)
+ [Step 4: Run your application](#serverless-getting-started-hello-world-run)
+ [Step 5: Modify and sync your application to the AWS Cloud](#serverless-getting-started-hello-world-sync)
+ [Step 6: \(Optional\) Test your application locally](#serverless-getting-started-hello-world-test)
+ [Step 7: Delete your application from the AWS Cloud](#serverless-getting-started-hello-world-delete)
+ [Troubleshooting](#serverless-getting-started-hello-world-troubleshoot)
+ [Learn more](#serverless-getting-started-hello-world-learn)

## Prerequisites<a name="serverless-getting-started-hello-world-prerequisites"></a>

Verify that you have completed the following:
+ [AWS SAM prerequisites](prerequisites.md)
+ [Installing the AWS SAM CLI](install-sam-cli.md)

## Step 1: Initialize the sample Hello World application<a name="serverless-getting-started-hello-world-init"></a>

In this step, you will use the AWS SAM CLI to create a sample **Hello World** application project on your local machine\.

**To initialize the sample Hello World application**

1. In your command line, run the following from a starting directory of your choice:

   ```
   $ sam init
   ```

1. The AWS SAM CLI will guide you through initializing a new application\. Configure the following:

   1. Select **AWS Quick Start Templates** to choose a starting template\.

   1. Choose the **Hello World Example** template and download it\.

   1. Use the Python runtime and `zip` package type\.

   1. For this tutorial, opt out of AWS X\-Ray tracing\. To learn more, see [What is AWS X\-Ray?](https://docs.aws.amazon.com/xray/latest/devguide/aws-xray.html) in the *AWS X\-Ray Developer Guide*\.

   1. For this tutorial, opt out of monitoring with Amazon CloudWatch Application Insights\. To learn more, see [ Amazon CloudWatch Application Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-application-insights.html) in the *Amazon CloudWatch User Guide*\.

   1. Name your application as **sam\-app**\.

   To use the AWS SAM CLI interactive flow:
   + Brackets \(`[ ]`\) indicate default values\. Leave your answer blank to select the default value\.
   + Enter **`y`** for **yes**, and **`n`** for **no**\.

   The following is an example of the `sam init` interactive flow:

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
       3 - Serverless API
       4 - Scheduled task
       5 - Standalone function
       6 - Data processing
       7 - Hello World Example With Powertools
       8 - Infrastructure event management
       9 - Serverless Connector Hello World Example
       10 - Multi-step workflow with Connectors
       11 - Lambda EFS example
       12 - DynamoDB Example
       13 - Machine Learning
   Template: 1
   
   Use the most popular runtime and package type? (Python and zip) [y/N]: y
   
   Would you like to enable X-Ray tracing on the function(s) in your application?  [y/N]: 
   
   Would you like to enable monitoring using CloudWatch Application Insights?
   For more info, please view https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-application-insights.html [y/N]: 
   
   Project name [sam-app]:
   ```

1. The AWS SAM CLI downloads your starting template and creates the application project directory structure on your local machine\. The following is an example of the AWS SAM CLI output:

   ```
   Cloning from https://github.com/aws/aws-sam-cli-app-templates (process may take a moment)
   
       -----------------------
       Generating application:
       -----------------------
       Name: sam-app
       Runtime: python3.9
       Architectures: x86_64
       Dependency Manager: pip
       Application Template: hello-world
       Output Directory: .
       Configuration file: sam-app/samconfig.toml
   
       Next steps can be found in the README file at sam-app/README.md
   
   
   Commands you can use next
   =========================
   [*] Create pipeline: cd sam-app && sam pipeline init --bootstrap
   [*] Validate SAM template: cd sam-app && sam validate
   [*] Test Function in the Cloud: cd sam-app && sam sync --stack-name {stack-name} --watch
   ```

1. From your command line, move to the newly created `sam-app` directory\. The following is an example of what the AWS SAM CLI has created:

   ```
   $ cd sam-app
   
   $ tree
   
   ├── README.md
   ├── __init__.py
   ├── events
   │   └── event.json
   ├── hello_world
   │   ├── __init__.py
   │   ├── app.py
   │   └── requirements.txt
   ├── samconfig.toml
   ├── template.yaml
   └── tests
       ├── __init__.py
       ├── integration
       │   ├── __init__.py
       │   └── test_api_gateway.py
       ├── requirements.txt
       └── unit
           ├── __init__.py
           └── test_handler.py
           
   6 directories, 14 files
   ```

   Some important files to highlight:
   + `hello_world/app.py` – Contains your Lambda function code\.
   + `hello_world/requirements.txt` – Contains any Python dependencies that your Lambda function requires\.
   + `samconfig.toml` – Configuration file for your application that stores default parameters used by the AWS SAM CLI\.
   + `template.yaml` – The AWS SAM template that contains your application infrastructure code\.

You now have a completely authored serverless application on your local machine\!

## Step 2: Build your application<a name="serverless-getting-started-hello-world-build"></a>

In this step, you use the AWS SAM CLI to build your application and prepare for deployment\. When you build, the AWS SAM CLI creates a `.aws-sam` directory and organizes your function dependencies, project code, and project files there\.

**To build your application**
+ In your command line, from the `sam-app` project directory, run the following:

  ```
  $ sam build
  ```
**Note**  
 If you don't have Python on your local machine, use the sam build \-\-use\-container  command instead\. The AWS SAM CLI will create a Docker container that includes your function's runtime and dependencies\. This command requires Docker on your local machine\. To install Docker, see [Installing Docker](install-docker.md)\.

  The following is an example of the AWS SAM CLI output:

  ```
  $ sam build
  Starting Build use cache
  Manifest file is changed (new hash: 3298f1304...d4d421) or dependency folder (.aws-sam/deps/4d3dfad6-a267-47a6-a6cd-e07d6fae318c) is missing for (HelloWorldFunction), downloading dependencies and copying/building source
  Building codeuri: /Users/.../Demo/sam-tutorial1/sam-app/hello_world runtime: python3.9 metadata: {} architecture: x86_64 functions: HelloWorldFunction
  Running PythonPipBuilder:CleanUp
  Running PythonPipBuilder:ResolveDependencies
  Running PythonPipBuilder:CopySource
  Running PythonPipBuilder:CopySource
  
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

  The following is a shortened example of the `.aws-sam` directory created by the AWS SAM CLI:

  ```
  .aws-sam
  ├── build
  │   ├── HelloWorldFunction
  │   │   ├── __init__.py
  │   │   ├── app.py
  │   │   └── requirements.txt
  │   └── template.yaml
  └── build.toml
  ```

Some important files to highlight:
+ `build/HelloWorldFunction` – Contains your Lambda function code and dependencies\. The AWS SAM CLI creates a directory for each function in your application\.
+ `build/template.yaml` – Contains a copy of your AWS SAM template that is referenced by AWS CloudFormation at deployment\.
+ `build.toml` – Configuration file that stores default parameter values referenced by the AWS SAM CLI when building and deploying your application\.

You are now ready to deploy your application to the AWS Cloud\.

## Step 3: Deploy your application to the AWS Cloud<a name="serverless-getting-started-hello-world-deploy"></a>

**Note**  
This step requires AWS credentials configuration\. For more information, see [Step 5: Use the AWS CLI to configure AWS credentials](prerequisites.md#prerequisites-configure-credentials) in [AWS SAM prerequisites](prerequisites.md)\.

In this step, you use the AWS SAM CLI to deploy your application to the AWS Cloud\. The AWS SAM CLI will do the following:
+ Guide you through configuring your application settings for deployment\.
+ Upload your application files to Amazon Simple Storage Service \(Amazon S3\)\.
+ Transform your AWS SAM template into an AWS CloudFormation template\. It then uploads your template to the AWS CloudFormation service to provision your AWS resources\.

**To deploy your application**

1. In your command line, from the `sam-app` project directory, run the following:

   ```
   $ sam deploy --guided
   ```

1. Follow the AWS SAM CLI interactive flow to configure your application settings\. Configure the following:

   1. The **AWS CloudFormation stack name** – A stack is a collection of AWS resources that you can manage as a single unit\. To learn more, see [Working with stacks](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacks.html) in the *AWS CloudFormation User Guide*\.

   1. The **AWS Region** to deploy your AWS CloudFormation stack to\. For more information, see [AWS CloudFormation endpoints](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-endpoints.html) in the *AWS CloudFormation User Guide*\.

   1. For this tutorial, opt out of **confirming changes before deploy**\.

   1. Allow **IAM role creation** – This lets AWS SAM create the IAM role necessary for your API Gateway resource and Lambda function resource to interact\.

   1. For this tutorial, opt out of **disabling rollback**\.

   1. Allow **HelloWorldFunction without authorization defined** – This message displays because your API Gateway endpoint is configured to be publicly accessible, without authorization\. Since this is the intended configuration for your Hello World application, allow the AWS SAM CLI to continue\. For more information about configuring authorization, see [Controlling access to API Gateway APIs](serverless-controlling-access-to-apis.md)\.

   1. **Save arguments to configuration file** – This will update your application’s `samconfig.toml` file with your deployment preferences\.

   1. Select the default **configuration file name**\.

   1. Select the default **configuration environment**\.

   The following is an example output of the `sam deploy --guided` interactive flow:

   ```
   $ sam-app sam deploy --guided
   
   Configuring SAM deploy
   ======================
   
       Looking for config file [samconfig.toml] :  Found
       Reading default arguments  :  Success
   
       Setting default arguments for 'sam deploy'
       =========================================
       Stack Name [sam-app]:
       AWS Region [us-west-2]:
       #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
       Confirm changes before deploy [Y/n]: n
       #SAM needs permission to be able to create roles to connect to the resources in your template
       Allow SAM CLI IAM role creation [Y/n]: 
       #Preserves the state of previously provisioned resources when an operation fails
       Disable rollback [y/N]: 
       HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
       Save arguments to configuration file [Y/n]: 
       SAM configuration file [samconfig.toml]:
       SAM configuration environment [default]:
   ```

1. The AWS SAM CLI deploys your application by doing the following:
   + The AWS SAM CLI creates an Amazon S3 bucket and uploads your `.aws-sam` directory\.
   + The AWS SAM CLI transforms your AWS SAM template into AWS CloudFormation and uploads it to the AWS CloudFormation service\.
   + AWS CloudFormation provisions your resources\.

   During deployment, the AWS SAM CLI displays your progress\. The following is an example output:

   ```
   Looking for resources needed for deployment:
   
       Managed S3 bucket: aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr
       A different default S3 bucket can be set in samconfig.toml
   
       Parameter "stack_name=sam-app" in [default.deploy.parameters] is defined as a global parameter [default.global.parameters].
       This parameter will be only saved under [default.global.parameters] in /Users/.../Demo/sam-tutorial1/sam-app/samconfig.toml.
   
       Saved arguments to config file
       Running 'sam deploy' for future deployments will use the parameters saved above.
       The above parameters can be changed by modifying samconfig.toml
       Learn more about samconfig.toml syntax at
       https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-config.html
   
   File with same data already exists at sam-app/da3c598813f1c2151579b73ad788cac8, skipping upload
   
       Deploying with following values
       ===============================
       Stack name                   : sam-app
       Region                       : us-west-2
       Confirm changeset            : False
       Disable rollback             : False
       Deployment s3 bucket         : aws-sam-cli-managed-default-samclisourcebucket-1a4x26zbcdkqr
       Capabilities                 : ["CAPABILITY_IAM"]
       Parameter overrides          : {}
       Signing Profiles             : {}
   
   Initiating deployment
   =====================
   
   File with same data already exists at sam-app/2bebf67c79f6a743cc5312f6dfc1efee.template, skipping upload
   
   
   Waiting for changeset to be created..
   
   CloudFormation stack changeset
   ---------------------------------------------------------------------------------------------------------------------------------------------
   Operation                           LogicalResourceId                   ResourceType                        Replacement
   ---------------------------------------------------------------------------------------------------------------------------------------------
   * Modify                            HelloWorldFunction                  AWS::Lambda::Function               False
   * Modify                            ServerlessRestApi                   AWS::ApiGateway::RestApi            False
   - Delete                            AwsSamAutoDependencyLayerNestedSt   AWS::CloudFormation::Stack          N/A
                                       ack
   ---------------------------------------------------------------------------------------------------------------------------------------------
   
   
   Changeset created successfully. arn:aws:cloudformation:us-west-2:513423067560:changeSet/samcli-deploy1678917603/22e05525-08f9-4c52-a2c4-f7f1fd055072
   
   
   2023-03-15 12:00:16 - Waiting for stack create/update to complete
   
   CloudFormation events from stack operations (refresh every 0.5 seconds)
   ---------------------------------------------------------------------------------------------------------------------------------------------
   ResourceStatus                      ResourceType                        LogicalResourceId                   ResourceStatusReason
   ---------------------------------------------------------------------------------------------------------------------------------------------
   UPDATE_IN_PROGRESS                  AWS::Lambda::Function               HelloWorldFunction                  -
   UPDATE_COMPLETE                     AWS::Lambda::Function               HelloWorldFunction                  -
   UPDATE_COMPLETE_CLEANUP_IN_PROGRE   AWS::CloudFormation::Stack          sam-app                             -
   SS
   DELETE_IN_PROGRESS                  AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   -
                                                                           ack
   DELETE_COMPLETE                     AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   -
                                                                           ack
   UPDATE_COMPLETE                     AWS::CloudFormation::Stack          sam-app                             -
   ---------------------------------------------------------------------------------------------------------------------------------------------
   
   CloudFormation outputs from deployed stack
   ----------------------------------------------------------------------------------------------------------------------------------------------
   Outputs
   ----------------------------------------------------------------------------------------------------------------------------------------------
   Key                 HelloWorldFunctionIamRole
   Description         Implicit IAM Role created for Hello World function
   Value               arn:aws:iam::513423067560:role/sam-app-HelloWorldFunctionRole-15GLOUR9LMT1W
   
   Key                 HelloWorldApi
   Description         API Gateway endpoint URL for Prod stage for Hello World function
   Value               https://<restapiid>.execute-api.us-west-2.amazonaws.com/Prod/hello/
   
   Key                 HelloWorldFunction
   Description         Hello World Lambda Function ARN
   Value               arn:aws:lambda:us-west-2:513423067560:function:sam-app-HelloWorldFunction-yQDNe17r9maD
   ----------------------------------------------------------------------------------------------------------------------------------------------
   
   
   Successfully created/updated stack - sam-app in us-west-2
   ```

Your application is now deployed and running in the AWS Cloud\!

## Step 4: Run your application<a name="serverless-getting-started-hello-world-run"></a>

In this step, you will send a GET request to your API endpoint and see your Lambda function output\.

**To get your API endpoint value**

1. From the information displayed by the AWS SAM CLI in the previous step, locate the `Outputs` section\. In this section, locate your `HelloWorldApi` resource to find your HTTP endpoint value\. The following is an example output:

   ```
   ----------------------------------------------------------------------------------------------------------------------------------------------
   Outputs
   ----------------------------------------------------------------------------------------------------------------------------------------------
   ...
   Key                 HelloWorldApi
   Description         API Gateway endpoint URL for Prod stage for Hello World function
   Value               https://ets1gv8lxi.execute-api.us-west-2.amazonaws.com/Prod/hello/
   ...
   ----------------------------------------------------------------------------------------------------------------------------------------------
   ```

1. Alternatively, you can use the sam list endpoints \-\-output json command to get this information\. The following is an example output:

   ```
   $ sam list endpoints --output json
   2023-03-15 12:39:19 Loading policies from IAM...
   2023-03-15 12:39:25 Finished loading policies from IAM.
   [
     {
       "LogicalResourceId": "HelloWorldFunction",
       "PhysicalResourceId": "sam-app-HelloWorldFunction-yQDNe17r9maD",
       "CloudEndpoint": "-",
       "Methods": "-"
     },
     {
       "LogicalResourceId": "ServerlessRestApi",
       "PhysicalResourceId": "ets1gv8lxi",
       "CloudEndpoint": [
         "https://ets1gv8lxi.execute-api.us-west-2.amazonaws.com/Prod",
         "https://ets1gv8lxi.execute-api.us-west-2.amazonaws.com/Stage"
       ],
       "Methods": [
         "/hello['get']"
       ]
     }
   ]
   ```

**To invoke your function**
+ Using your browser or the command line, send a GET request to your API endpoint\. The following is an example using the curl command:

  ```
  $ curl https://ets1gv8lxi.execute-api.us-west-2.amazonaws.com/Prod/hello/
  {"message": "hello world"}
  ```

## Step 5: Modify and sync your application to the AWS Cloud<a name="serverless-getting-started-hello-world-sync"></a>

In this step, you use the AWS SAM CLI sam sync \-\-watch command to sync local changes to the AWS Cloud\.

**To use sam sync**

1. In your command line, from the `sam-app` project directory, run the following:

   ```
   $ sam sync --watch
   ```

1. The AWS SAM CLI prompts you to confirm that you are syncing a development stack\. Since the sam sync \-\-watch command automatically deploys local changes to the AWS Cloud in real time, we recommend it for development environments only\.

   The AWS SAM CLI performs an initial deployment before it begins monitoring for local changes\. The following is an example output:

   ```
   $ sam sync --watch
   The SAM CLI will use the AWS Lambda, Amazon API Gateway, and AWS StepFunctions APIs to upload your code without
   performing a CloudFormation deployment. This will cause drift in your CloudFormation stack.
   **The sync command should only be used against a development stack**.
   
   Confirm that you are synchronizing a development stack.
   
   Enter Y to proceed with the command, or enter N to cancel:
    [Y/n]: y
   Queued infra sync. Waiting for in progress code syncs to complete...
   Starting infra sync.
   Manifest is not changed for (HelloWorldFunction), running incremental build
   Building codeuri: /Users/.../Demo/sam-tutorial1/sam-app/hello_world runtime: python3.9 metadata: {} architecture: x86_64 functions: HelloWorldFunction
   Running PythonPipBuilder:CopySource
   
   Build Succeeded
   
   Successfully packaged artifacts and wrote output template to file /var/folders/45/5ct135bx3fn2551_ptl5g6_80000gr/T/tmpq3x9vh63.
   Execute the following command to deploy the packaged template
   sam deploy --template-file /var/folders/45/5ct135bx3fn2551_ptl5g6_80000gr/T/tmpq3x9vh63 --stack-name <YOUR STACK NAME>
   
   
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
   
   
   2023-03-15 13:10:05 - Waiting for stack create/update to complete
   
   CloudFormation events from stack operations (refresh every 0.5 seconds)
   ---------------------------------------------------------------------------------------------------------------------------------------------
   ResourceStatus                      ResourceType                        LogicalResourceId                   ResourceStatusReason
   ---------------------------------------------------------------------------------------------------------------------------------------------
   UPDATE_IN_PROGRESS                  AWS::CloudFormation::Stack          sam-app                             Transformation succeeded
   CREATE_IN_PROGRESS                  AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   -
                                                                           ack
   CREATE_IN_PROGRESS                  AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   Resource creation Initiated
                                                                           ack
   CREATE_COMPLETE                     AWS::CloudFormation::Stack          AwsSamAutoDependencyLayerNestedSt   -
                                                                           ack
   UPDATE_IN_PROGRESS                  AWS::Lambda::Function               HelloWorldFunction                  -
   UPDATE_COMPLETE                     AWS::Lambda::Function               HelloWorldFunction                  -
   UPDATE_COMPLETE_CLEANUP_IN_PROGRE   AWS::CloudFormation::Stack          sam-app                             -
   SS
   UPDATE_COMPLETE                     AWS::CloudFormation::Stack          sam-app                             -
   ---------------------------------------------------------------------------------------------------------------------------------------------
   
   CloudFormation outputs from deployed stack
   ----------------------------------------------------------------------------------------------------------------------------------------------
   Outputs
   ----------------------------------------------------------------------------------------------------------------------------------------------
   Key                 HelloWorldFunctionIamRole
   Description         Implicit IAM Role created for Hello World function
   Value               arn:aws:iam::513423067560:role/sam-app-HelloWorldFunctionRole-15GLOUR9LMT1W
   
   Key                 HelloWorldApi
   Description         API Gateway endpoint URL for Prod stage for Hello World function
   Value               https://ets1gv8lxi.execute-api.us-west-2.amazonaws.com/Prod/hello/
   
   Key                 HelloWorldFunction
   Description         Hello World Lambda Function ARN
   Value               arn:aws:lambda:us-west-2:513423067560:function:sam-app-HelloWorldFunction-yQDNe17r9maD
   ----------------------------------------------------------------------------------------------------------------------------------------------
   
   
   Stack update succeeded. Sync infra completed.
   
   Infra sync completed.
   CodeTrigger not created as CodeUri or DefinitionUri is missing for ServerlessRestApi.
   ```

Next, you will modify your Lambda function code\. The AWS SAM CLI will automatically detect this change and sync your application to the AWS Cloud\.

**To modify and sync your application**

1. In your IDE of choice, open the `sam-app/hello_world/app.py` file\.

1. Change the `message` and save your file\. The following is an example:

   ```
   import json
   ...
   def lambda_handler(event, context):
       ...
       return {
           "statusCode": 200,
           "body": json.dumps({
               "message": "hello everyone!",
               ...
           }),
       }
   ```

1. The AWS SAM CLI detects your change and syncs your application to the AWS Cloud\. The following is an example output:

   ```
   Syncing Lambda Function HelloWorldFunction...
   Manifest is not changed for (HelloWorldFunction), running incremental build
   Building codeuri: /Users/.../Demo/sam-tutorial1/sam-app/hello_world runtime: python3.9 metadata: {} architecture: x86_64 functions: HelloWorldFunction
   Running PythonPipBuilder:CopySource
   Finished syncing Lambda Function HelloWorldFunction.
   ```

1. To verify your change, send a GET request to your API endpoint again\.

   ```
   $ curl https://ets1gv8lxi.execute-api.us-west-2.amazonaws.com/Prod/hello/
   {"message": "hello everyone!"}
   ```

## Step 6: \(Optional\) Test your application locally<a name="serverless-getting-started-hello-world-test"></a>

**Note**  
This step is optional since it requires Docker on your local machine\.

**Important**  
To use the AWS SAM CLI for local testing, you must have Docker installed and configured\. For more information, see [Installing Docker](install-docker.md)\.

In this step, you use the AWS SAM CLI sam local command to test your application locally\. To accomplish this, the AWS SAM CLI creates a local environment using Docker\. This local environment emulates the cloud\-based execution environment of your Lambda function\.

You will do the following:

1. Create a local environment for your Lambda function and invoke it\.

1. Host your HTTP API endpoint locally and use it to invoke your Lambda function\.

**To invoke your Lambda function locally**

1. In your command line, from the `sam-app` project directory, run the following:

   ```
   $ sam local invoke
   ```

1. The AWS SAM CLI creates a local Docker container and invokes your function\. The following is an example output:

   ```
   $ sam local invoke
   Invoking app.lambda_handler (python3.9)
   Local image was not found.
   Removing rapid images for repo public.ecr.aws/sam/emulation-python3.9
   Building image.....................
   Using local image: public.ecr.aws/lambda/python:3.9-rapid-x86_64.
   
   Mounting /Users/.../Demo/sam-tutorial1/sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated inside runtime container
   START RequestId: b046db01-2a00-415d-af97-35f3a02e9eb6 Version: $LATEST
   END RequestId: b046db01-2a00-415d-af97-35f3a02e9eb6
   REPORT RequestId: b046db01-2a00-415d-af97-35f3a02e9eb6    Init Duration: 1.01 ms    Duration: 633.45 ms    Billed Duration: 634 ms    Memory Size: 128 MB    Max Memory Used: 128 MB
   {"statusCode": 200, "body": "{\"message\": \"hello world\"}"}
   ```

**To host your API locally**

1. In your command line, from the `sam-app` project directory, run the following:

   ```
   $ sam local start-api
   ```

1. The AWS SAM CLI creates a local Docker container for your Lambda function and creates a local HTTP server to simulate your API endpoint\. The following is an example output:

   ```
   $ sam local start-api
   Initializing the lambda functions containers.
   Local image is up-to-date
   Using local image: public.ecr.aws/lambda/python:3.9-rapid-x86_64.
   
   Mounting /Users/.../Demo/sam-tutorial1/sam-app/.aws-sam/build/HelloWorldFunction as /var/task:ro,delegated inside runtime container
   Containers Initialization is done.
   Mounting HelloWorldFunction at http://127.0.0.1:3000/hello [GET]
   You can now browse to the above endpoints to invoke your functions. You do not need to restart/reload SAM CLI while working on your functions, changes will be reflected instantly/automatically. If you used sam build before running local commands, you will need to re-run sam build for the changes to be picked up. You only need to restart SAM CLI if you update your AWS SAM template
   2023-03-15 14:25:21 WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
    * Running on http://127.0.0.1:3000
   2023-03-15 14:25:21 Press CTRL+C to quit
   ```

1. Using your browser or the command line, send a GET request to your local API endpoint\. The following is an example using the curl command:

   ```
   $ curl http://127.0.0.1:3000/hello
   {"message": "hello world"}
   ```

## Step 7: Delete your application from the AWS Cloud<a name="serverless-getting-started-hello-world-delete"></a>

In this step, you use the AWS SAM CLI sam delete command to delete your application from the AWS Cloud\.

**To delete your application from the AWS Cloud**

1. In your command line, from the `sam-app` project directory, run the following:

   ```
   $ sam delete
   ```

1. The AWS SAM CLI will ask you to confirm\. Then, it will delete your application’s Amazon S3 bucket and AWS CloudFormation stack\. The following is an example output:

   ```
   $ sam delete
       Are you sure you want to delete the stack sam-app in the region us-west-2 ? [y/N]: y
       Are you sure you want to delete the folder sam-app in S3 which contains the artifacts? [y/N]: y
       - Deleting S3 object with key c6ce8fa8b5a97dd022ecd006536eb5a4
       - Deleting S3 object with key 5d513a459d062d644f3b7dd0c8b56a2a.template
       - Deleting S3 object with key sam-app/2bebf67c79f6a743cc5312f6dfc1efee.template
       - Deleting S3 object with key sam-app/6b208d0e42ad15d1cee77d967834784b.template
       - Deleting S3 object with key sam-app/da3c598813f1c2151579b73ad788cac8
       - Deleting S3 object with key sam-app/f798cdd93cee188a71d120f14a035b11
       - Deleting Cloudformation stack sam-app
   
   Deleted successfully
   ```

## Troubleshooting<a name="serverless-getting-started-hello-world-troubleshoot"></a>

To troubleshoot the AWS SAM CLI, see [AWS SAM CLI troubleshooting](sam-cli-troubleshooting.md)\.

## Learn more<a name="serverless-getting-started-hello-world-learn"></a>

To continue learning about AWS SAM, see the following resources:
+ **[The Complete AWS SAM Workshop](https://s12d.com/sam-ws-en-intro)** – A workshop designed to teach you many of the major features that AWS SAM provides\.
+ **[ Sessions with SAM](https://www.youtube.com/playlist?list=PLJo-rJlep0ED198FJnTzhIB5Aut_1vDAd)** – Video series created by our AWS Serverless Developer Advocate team on using AWS SAM\.
+ **[Serverless Land](https://serverlessland.com/)** – Site that brings together the latest information, blogs, videos, code, and learning resources for AWS serverless\.