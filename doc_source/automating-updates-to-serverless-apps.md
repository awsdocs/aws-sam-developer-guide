# Deploying serverless applications gradually<a name="automating-updates-to-serverless-apps"></a>

AWS Serverless Application Model \(AWS SAM\) comes built\-in with [CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html) to provide gradual AWS Lambda deployments\. With just a few lines of configuration, AWS SAM does the following for you:
+ Deploys new versions of your Lambda function, and automatically creates aliases that point to the new version\.
+ Gradually shifts customer traffic to the new version until you're satisfied that it's working as expected\. If an update doesn't work correctly, you can roll back the changes\.
+ Defines pre\-traffic and post\-traffic test functions to verify that the newly deployed code is configured correctly and that your application operates as expected\.
+ Automatically rolls back the deployment if CloudWatch alarms are triggered\.

**Note**  
If you enable gradual deployments through your AWS SAM template, a CodeDeploy resource is automatically created for you\. You can view the CodeDeploy resource directly through the AWS Management Console\.

**Example**

The following example demonstrates the use of CodeDeploy to gradually shift customers to your newly deployed version of Lambda function:

```
Resources:
MyLambdaFunction:
  Type: AWS::Serverless::Function
  Properties:
    Handler: index.handler
    Runtime: nodejs12.x
    CodeUri: s3://bucket/code.zip

    AutoPublishAlias: live

    DeploymentPreference:
      Type: Canary10Percent10Minutes 
      Alarms:
        # A list of alarms that you want to monitor
        - !Ref AliasErrorMetricGreaterThanZeroAlarm
        - !Ref LatestVersionErrorMetricGreaterThanZeroAlarm
      Hooks:
        # Validation Lambda functions that are run before & after traffic shifting
        PreTraffic: !Ref PreTrafficLambdaFunction
        PostTraffic: !Ref PostTrafficLambdaFunction
```

These revisions to the AWS SAM template do the following:
+ `AutoPublishAlias`: By adding this property and specifying an alias name, AWS SAM:
  + Detects when new code is being deployed, based on changes to the Lambda function's Amazon S3 URI\.
  + Creates and publishes an updated version of that function with the latest code\.
  + Creates an alias with a name that you provide \(unless an alias already exists\), and points to the updated version of the Lambda function\. Function invocations should use the alias qualifier to take advantage of this\. If you aren't familiar with Lambda function versioning and aliases, see [AWS Lambda Function Versioning and Aliases](https://docs.aws.amazon.com/lambda/latest/dg/versioning-aliases.html)\.
+ `Deployment Preference Type`: In the previous example, 10 percent of your customer traffic is immediately shifted to your new version\. After 10 minutes, all traffic is shifted to the new version\. However, if your pre\-traffic or post\-traffic tests fail, or if a CloudWatch alarm is triggered, CodeDeploy rolls back your deployment\. You can specify how traffic should be shifted between versions in the following ways:
  + `Canary`: Traffic is shifted in two increments\. You can choose from predefined canary options\. The options specify the percentage of traffic that's shifted to your updated Lambda function version in the first increment, and the interval, in minutes, before the remaining traffic is shifted in the second increment\. 
  + `Linear`: Traffic is shifted in equal increments with an equal number of minutes between each increment\. You can choose from predefined linear options that specify the percentage of traffic that's shifted in each increment and the number of minutes between each increment\. 
  + `AllAtOnce`: All traffic is shifted from the original Lambda function to the updated Lambda function version at once\. 

  The following table outlines other traffic\-shifting options that are available beyond the one used in the example\.     
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/automating-updates-to-serverless-apps.html)
+ `Alarms`: These are CloudWatch alarms that are triggered by any errors raised by the deployment\. When encountered, they automatically roll back your deployment\. For example, if the updated code you're deploying causes errors within the application\. Another example is if any [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/monitoring-functions-metrics.html) or custom CloudWatch metrics that you specified have breached the alarm threshold\.
+ `Hooks`: These are pre\-traffic and post\-traffic test functions that run checks before traffic shifting starts to the new version, and after traffic shifting completes\.
  + `PreTraffic`: Before traffic shifting starts, CodeDeploy invokes the pre\-traffic hook Lambda function\. This Lambda function must call back to CodeDeploy and indicate success or failure\. If the function fails, it aborts and reports a failure back to AWS CloudFormation\. If the function succeeds, CodeDeploy proceeds to traffic shifting\.
  + `PostTraffic`: After traffic shifting completes, CodeDeploy invokes the post\-traffic hook Lambda function\. This is similar to the pre\-traffic hook, where the function must call back to CodeDeploy to report a success or failure\. Use post\-traffic hooks to run integration tests or other validation actions\.

  For more information, see [SAM Reference to Safe Deployments](https://github.com/aws/serverless-application-model/blob/master/docs/safe_lambda_deployments.rst)\. 

## Gradually deploying a Lambda function for the first time<a name="automating-updates-to-serverless-apps-first-time"></a>

 When deploying a Lambda function gradually, CodeDeploy requires a previously deployed function version to shift traffic from\. Therefore, your first deployment should be accomplished in two steps: 
+ **Step 1**: Deploy your Lambda function and automatically create aliases with `AutoPublishAlias`\.
+ **Step 2**: Perform your gradual deployment with `DeploymentPreference`\.

Performing your first gradual deployment in two steps gives CodeDeploy a previous Lambda function version to shift traffic from\.

### Step 1: Deploy your Lambda function<a name="automating-updates-to-serverless-apps-first-time-step1"></a>

```
Resources:
MyLambdaFunction:
  Type: AWS::Serverless::Function
  Properties:
    Handler: index.handler
    Runtime: nodejs12.x
    CodeUri: s3://bucket/code.zip

    AutoPublishAlias: live
```

### Step 2: Perform your gradual deployment<a name="automating-updates-to-serverless-apps-first-time-step2"></a>

```
Resources:
MyLambdaFunction:
  Type: AWS::Serverless::Function
  Properties:
    Handler: index.handler
    Runtime: nodejs12.x
    CodeUri: s3://bucket/code.zip

    AutoPublishAlias: live

    DeploymentPreference:
      Type: Canary10Percent10Minutes 
      Alarms:
        # A list of alarms that you want to monitor
        - !Ref AliasErrorMetricGreaterThanZeroAlarm
        - !Ref LatestVersionErrorMetricGreaterThanZeroAlarm
      Hooks:
        # Validation Lambda functions that are run before and after traffic shifting
        PreTraffic: !Ref PreTrafficLambdaFunction
        PostTraffic: !Ref PostTrafficLambdaFunction
```