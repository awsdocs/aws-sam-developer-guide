# Monitor your serverless applications with CloudWatch Application Insights<a name="monitor-app-insights"></a>

 Amazon CloudWatch Application Insights helps you monitor the AWS resources in your applications to help identify potential issues\. It can analyze AWS resource data for signs of problems and build automated dashboards to visualize them\. You can configure CloudWatch Application Insights to use with your AWS Serverless Application Model \(AWS SAM\) applications\. To learn more about CloudWatch Application Insights, see [Amazon CloudWatch Application Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-application-insights.html) in the *Amazon CloudWatch User Guide*\. 

**Topics**
+ [Configuring CloudWatch Application Insights with AWS SAM](#monitor-app-insights-configure)
+ [Next steps](#monitor-app-insights-next)

## Configuring CloudWatch Application Insights with AWS SAM<a name="monitor-app-insights-configure"></a>

 Configure CloudWatch Application Insights for your AWS SAM applications through the AWS SAM Command Line Interface \(AWS SAM CLI\) or through your AWS SAM templates\. 

### Configure through the AWS SAM CLI<a name="monitor-app-insights-configure-cli"></a>

 When initializing your application with sam init, activate CloudWatch Application Insights through the interactive flow or by using the \-\-application\-insights option\. 

 To activate CloudWatch Application Insights through the AWS SAM CLI interactive flow, enter **y** when prompted\. 

```
Would you like to enable monitoring using CloudWatch Application Insights?
For more info, please view https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-application-insights.html [y/N]:
```

 To activate CloudWatch Application Insights with the \-\-application\-insights option, do the following\. 

```
sam init --application-insights
```

 To learn more about using the sam init command, see [sam init](sam-cli-command-reference-sam-init.md)\. 

### Configure through AWS SAM templates<a name="monitor-app-insights-configure-template"></a>

 Activate CloudWatch Application Insights by defining the `AWS::ResourceGroups::Group` and `AWS::ApplicationInsights::Application` resources in your AWS SAM templates\. 

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31 
...
Resources:
  ApplicationResourceGroup:
    Type: AWS::ResourceGroups::Group
    Properties:
      Name:
        Fn::Join:
        - ''
        - - ApplicationInsights-SAM-
        - Ref: AWS::StackName
      ResourceQuery:
        Type: CLOUDFORMATION_STACK_1_0
  ApplicationInsightsMonitoring:
    Type: AWS::ApplicationInsights::Application
    Properties:
      ResourceGroupName:
        Fn::Join:
          - ''
          - - ApplicationInsights-SAM-
          - Ref: AWS::StackName
        AutoConfigurationEnabled: 'true'
    DependsOn: ApplicationResourceGroup
```
+  `AWS::ResourceGroups::Group` – Creates a group to organize your AWS resources in order to manage and automate tasks on a large number of resources at one time\. Here, you create a resource group to use with CloudWatch Application Insights\. For more information on this resource type, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-resourcegroups-group.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-resourcegroups-group.html) in the *AWS CloudFormation User Guide*\. 
+  `AWS::ApplicationInsights::Application` – Configures CloudWatch Application Insights for the resource group\. For more information on this resource type, see [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-applicationinsights-application.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-applicationinsights-application.html) in the *AWS CloudFormation User Guide*\. 

 Both resources are automatically passed through to AWS CloudFormation at application deployment\. You can use the AWS CloudFormation syntax in your AWS SAM template to configure CloudWatch Application Insights further\. For more information, see [Use AWS CloudFormation templates](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/appinsights-cloudformation.html) in the *Amazon CloudWatch User Guide*\. 

 When using the sam init \-\-application\-insights command, both of these resources are automatically generated in your AWS SAM template\. Here is an example of a generated template\. 

```
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Description: >
  sam-app-test
  
  Sample SAM Template for sam-app-test

# More info about Globals: https://github.com/awslabs/serverless-application-model/blob/master/docs/globals.rst
Globals:
  Function:
    Timeout: 3
    MemorySize: 128

Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function # More info about Function Resource: https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessfunction
    Properties:
      CodeUri: hello_world/
      Handler: app.lambda_handler
      Runtime: python3.9
      Architectures:
      - x86_64
      Events:
        HelloWorld:
          Type: Api # More info about API Event Source: https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#api
          Properties:
            Path: /hello
            Method: get

  ApplicationResourceGroup:
    Type: AWS::ResourceGroups::Group
    Properties:
      Name:
        Fn::Join:
        - ''
        - - ApplicationInsights-SAM-
        - Ref: AWS::StackName
      ResourceQuery:
      	Type: CLOUDFORMATION_STACK_1_0
  ApplicationInsightsMonitoring:
    Type: AWS::ApplicationInsights::Application
    Properties:
      ResourceGroupName:
        Fn::Join:
        - ''
        - - ApplicationInsights-SAM-
        - Ref: AWS::StackName
      AutoConfigurationEnabled: 'true'
    DependsOn: ApplicationResourceGroup
    
Outputs:
  # ServerlessRestApi is an implicit API created out of Events key under Serverless::Function
  # Find out more about other implicit resources you can reference within SAM
  # https://github.com/awslabs/serverless-application-model/blob/master/docs/internals/generated_resources.rst#api
  HelloWorldApi:
    Description: API Gateway endpoint URL for Prod stage for Hello World function
    Value: !Sub "https://${ServerlessRestApi}.execute-api.${AWS::Region}.amazonaws.com/Prod/hello/"
  HelloWorldFunction:
    Description: Hello World Lambda Function ARN
    Value: !GetAtt HelloWorldFunction.Arn
  HelloWorldFunctionIamRole:
    Description: Implicit IAM Role created for Hello World function
    Value: !GetAtt HelloWorldFunctionRole.Arn
```

## Next steps<a name="monitor-app-insights-next"></a>

 After configuring CloudWatch Application Insights, use sam build to build your application and sam deploy to deploy your application\. All CloudWatch Application Insights supported resources will be configured for monitoring\. 
+  For a list of supported resources, see [Supported logs and metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/appinsights-logs-and-metrics.html) in the *Amazon CloudWatch User Guide*\. 
+  To learn how to access CloudWatch Application Insights, see [Access CloudWatch Application Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/appinsights-accessing.html) in the *Amazon CloudWatch User Guide*\. 