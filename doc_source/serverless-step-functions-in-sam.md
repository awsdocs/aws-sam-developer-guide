# Orchestrating AWS resources with AWS Step Functions<a name="serverless-step-functions-in-sam"></a>

You can use [AWS Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/) to orchestrate AWS Lambda functions and other AWS resources to form complex and robust workflows\.

**Note**  
To manage AWS SAM templates that contain Step Functions state machines, you must use version 0\.52\.0 or later of the AWS SAM CLI\. To check which version you have, execute the command `sam --version`\.

Step Functions is based on the concepts of [tasks](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-task-state.html) and [state machines](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-states.html)\. You define state machines using the JSON\-based [Amazon States Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html)\. The [Step Functions console](https://console.aws.amazon.com/states/home?region=us-east-1#/) displays a graphical view of your state machine's structure so you can visually check your state machine's logic and monitor executions\.

With Step Functions support in AWS Serverless Application Model \(AWS SAM\), you can do the following:
+ Define state machines, either directly within an AWS SAM template or in a separate file 
+ Create state machine execution roles through AWS SAM policy templates, inline policies, or managed policies 
+ Trigger state machine executions with API Gateway or Amazon EventBridge events, on a schedule within an AWS SAM template, or by calling APIs directly
+ Use available [AWS SAM Policy Templates](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-policy-templates.html) for common Step Functions development patterns\.

## Example<a name="serverless-step-functions-in-sam-example"></a>

The following example snippet from a AWS SAM template file defines a Step Functions state machine in a definition file\. Note that the `my_state_machine.asl.json` file must be written in [Amazon States Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html)\.

```
AWSTemplateFormatVersion: "2010-09-09"
Transform: AWS::Serverless-2016-10-31
Description: Sample SAM template with Step Functions State Machine

Resources:
  MyStateMachine:
    Type: AWS::Serverless::StateMachine
    Properties:
      DefinitionUri: statemachine/my_state_machine.asl.json
      ...
```

To download a sample AWS SAM application that includes a Step Functions state machine, see [Create a Step Functions State Machine Using AWS SAM](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-state-machine-using-sam.html) in the *AWS Step Functions Developer Guide*\.

## More information<a name="serverless-step-functions-in-sam-more-information"></a>

To learn more about Step Functions and using it with AWS SAM, see the following:
+ [How AWS Step Functions works](https://docs.aws.amazon.com/step-functions/latest/dg/how-step-functions-works.html)
+ [AWS Step Functions and AWS Serverless Application Model](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-sam-sfn.html)
+ [Tutorial: Create a Step Functions State Machine Using AWS SAM](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-state-machine-using-sam.html)
+ [AWS SAM Specification: AWS::Serverless::StateMachine](sam-resource-statemachine.md)