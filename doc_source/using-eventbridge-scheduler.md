# Scheduling events with EventBridge Scheduler<a name="using-eventbridge-scheduler"></a>

## What is Amazon EventBridge Scheduler?<a name="using-eventbridge-scheduler-intro"></a>

Amazon EventBridge Scheduler is a scheduling service that lets you create, initiate, and manage tens of millions of events and tasks across all AWS services\. To learn more about Amazon EventBridge Scheduler, see [What is Amazon EventBridge Scheduler?](https://docs.aws.amazon.com/scheduler/latest/UserGuide/what-is-scheduler.html) in the *EventBridge Scheduler User Guide*\.

**Topics**
+ [What is Amazon EventBridge Scheduler?](#using-eventbridge-scheduler-intro)
+ [EventBridge Scheduler support in AWS SAM](#using-eventbridge-scheduler-sam-support)
+ [Creating EventBridge Scheduler events in AWS SAM](#using-eventbridge-scheduler-sam-create)
+ [Examples](#using-eventbridge-scheduler-examples)
+ [Learn more](#using-eventbridge-scheduler-learn)

## EventBridge Scheduler support in AWS SAM<a name="using-eventbridge-scheduler-sam-support"></a>

The AWS Serverless Application Model \(AWS SAM\) template specification provides a simple, short\-hand syntax that you can use to schedule events with EventBridge Scheduler for AWS Lambda and AWS Step Functions\.

## Creating EventBridge Scheduler events in AWS SAM<a name="using-eventbridge-scheduler-sam-create"></a>

Set the `ScheduleV2` property as the event type in your AWS SAM template to define your EventBridge Scheduler event\. This property supports the `AWS::Serverless::Function` and `AWS::Serverless::StateMachine` resource types\.

```
MyFunction:
  Type: AWS::Serverless::Function
  Properties:
    Events:
      CWSchedule:
        Type: ScheduleV2
        Properties:
          Schedule: 'rate(1 minute)'
          Name: TestScheduleV2Function
          Description: Test schedule event
                    
MyStateMachine:
  Type: AWS::Serverless::StateMachine
  Properties:
    Events:
      CWSchedule:
        Type: ScheduleV2
        Properties:
          Schedule: 'rate(1 minute)'
          Name: TestScheduleV2StateMachine
          Description: Test schedule event
```

EventBridge Scheduler event scheduling also supports *dead\-letter queues \(DLQ\)* for unprocessed events\. For more information on dead\-letter queues, see [Configuring a dead\-letter queue for EventBridge Scheduler](https://docs.aws.amazon.com/scheduler/latest/UserGuide/configuring-schedule-dlq.html) in the *EventBridge Scheduler User Guide*\.

When a DLQ ARN is specified, AWS SAM configures permissions for the Scheduler schedule to send messages to the DLQ\. When a DLQ ARN is not specified, AWS SAM will create the DLQ resource\.

## Examples<a name="using-eventbridge-scheduler-examples"></a>

### Basic example of defining an EventBridge Scheduler event with AWS SAM<a name="using-eventbridge-scheduler-examples-example1"></a>

```
Transform: AWS::Serverless-2016-10-31
Resources:
  MyLambdaFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: index.handler
      Runtime: python3.8
      InlineCode: |
        def handler(event, context):
            print(event)
            return {'body': 'Hello World!', 'statusCode': 200}
      MemorySize: 128
      Events:
        Schedule:
          Type: ScheduleV2
          Properties:
            ScheduleExpression: rate(1 minute)
            Input: '{"hello": "simple"}'
 
  MySFNFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: index.handler
      Runtime: python3.8
      InlineCode: |
        def handler(event, context):
            print(event)
            return {'body': 'Hello World!', 'statusCode': 200}
      MemorySize: 128
 
  StateMachine:
    Type: AWS::Serverless::StateMachine
    Properties:
      Type: STANDARD
      Definition:
        StartAt: MyLambdaState
        States:
          MyLambdaState:
            Type: Task
            Resource: !GetAtt MySFNFunction.Arn
            End: true
      Policies:
        - LambdaInvokePolicy:
            FunctionName: !Ref MySFNFunction
      Events:
        Events:
        Schedule:
          Type: ScheduleV2
          Properties:
            ScheduleExpression: rate(1 minute)
            Input: '{"hello": "simple"}'
```

## Learn more<a name="using-eventbridge-scheduler-learn"></a>

To learn more about defining the `ScheduleV2` EventBridge Scheduler property, see:
+ [ScheduleV2](sam-property-function-schedulev2.md) for `AWS::Serverless::Function`\.
+ [ScheduleV2](sam-property-statemachine-statemachineschedulev2.md) for `AWS::Serverless::StateMachine`\.