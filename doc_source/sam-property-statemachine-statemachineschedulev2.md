# ScheduleV2<a name="sam-property-statemachine-statemachineschedulev2"></a>

The object describing a `ScheduleV2` event source type, which sets your state machine as the target of an Amazon EventBridge Scheduler event that triggers on a schedule\. For more information, see [What is Amazon EventBridge Scheduler?](https://docs.aws.amazon.com/scheduler/latest/UserGuide/what-is-scheduler.html) in the *EventBridge Scheduler User Guide*\.

AWS Serverless Application Model \(AWS SAM\) generates an [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html) resource when this event type is set\.

## Syntax<a name="sam-property-statemachine-statemachineschedulev2-syntax"></a>

To declare this entity in your AWS Serverless Application Model \(AWS SAM\) template, use the following syntax\.

### YAML<a name="sam-property-statemachine-statemachineschedulev2-syntax.yaml"></a>

```
DeadLetterConfig: DeadLetterConfig
[Description](#sam-statemachine-statemachineschedulev2-description): String
[EndDate](#sam-statemachine-statemachineschedulev2-enddate): String
[FlexibleTimeWindow](#sam-statemachine-statemachineschedulev2-flexibletimewindow): FlexibleTimeWindow
[GroupName](#sam-statemachine-statemachineschedulev2-groupname): String
[Input](#sam-statemachine-statemachineschedulev2-input): String
[KmsKeyArn](#sam-statemachine-statemachineschedulev2-kmskeyarn): String
[Name](#sam-statemachine-statemachineschedulev2-name): String
[OmitName](#sam-statemachine-statemachineschedulev2-omitname): Boolean
[PermissionsBoundary](#sam-statemachine-statemachineschedulev2-permissionsboundary): String
[RetryPolicy](#sam-statemachine-statemachineschedulev2-retrypolicy): RetryPolicy
[RoleArn](#sam-statemachine-statemachineschedulev2-rolearn): String
[ScheduleExpression](#sam-statemachine-statemachineschedulev2-scheduleexpression): String
[ScheduleExpressionTimezone](#sam-statemachine-statemachineschedulev2-scheduleexpressiontimezone): String
[StartDate](#sam-statemachine-statemachineschedulev2-startdate): String
[State](#sam-statemachine-statemachineschedulev2-state): String
```

## Properties<a name="sam-property-statemachine-statemachineschedulev2-properties"></a>

 `DeadLetterConfig`   <a name="sam-statemachine-statemachineschedulev2-deadletterconfig"></a>
Configure the Amazon Simple Queue Service \(Amazon SQS\) queue where EventBridge sends events after a failed target invocation\. Invocation can fail, for example, when sending an event to a Lambda function that doesn't exist, or when EventBridge has insufficient permissions to invoke the Lambda function\. For more information, see [Configuring a dead\-letter queue for EventBridge Scheduler](https://docs.aws.amazon.com/scheduler/latest/UserGuide/configuring-schedule-dlq.html) in the *EventBridge Scheduler User Guide*\.  
*Type*: [DeadLetterConfig](sam-property-statemachine-statemachinescheduledeadletterconfig.md)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is similar to the `[DeadLetterConfig](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-scheduler-schedule-target.html#cfn-scheduler-schedule-target-deadletterconfig)` property of the `AWS::Scheduler::Schedule` `Target` data type\. The AWS SAM version of this property includes additional subproperties, in case you want AWS SAM to create the dead\-letter queue for you\.

 `Description`   <a name="sam-statemachine-statemachineschedulev2-description"></a>
A description of the schedule\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Description](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html#cfn-scheduler-schedule-description)` property of an `AWS::Scheduler::Schedule` resource\.

 `EndDate`   <a name="sam-statemachine-statemachineschedulev2-enddate"></a>
The date, in UTC, before which the schedule can invoke its target\. Depending on the schedule's recurrence expression, invocations might stop on, or before, the EndDate you specify\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[EndDate](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html#cfn-scheduler-schedule-enddate)` property of an `AWS::Scheduler::Schedule` resource\.

 `FlexibleTimeWindow`   <a name="sam-statemachine-statemachineschedulev2-flexibletimewindow"></a>
Allows configuration of a window within which a schedule can be invoked\.  
*Type*: [FlexibleTimeWindow](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html#cfn-scheduler-schedule-flexibletimewindow)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[FlexibleTimeWindow](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler.html#cfn-scheduler-schedule-flexibletimewindow)` property of an `AWS::Scheduler::Schedule` resource\.

 `GroupName`   <a name="sam-statemachine-statemachineschedulev2-groupname"></a>
The name of the schedule group to associate with this schedule\. If not defined, the default group is used\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[GroupName](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html#cfn-scheduler-schedule-groupname)` property of an `AWS::Scheduler::Schedule` resource\.

 `Input`   <a name="sam-statemachine-statemachineschedulev2-input"></a>
Valid JSON text passed to the target\. If you use this property, nothing from the event text itself is passed to the target\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Input](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-scheduler-schedule-target.html#cfn-scheduler-schedule-target-input)` property of an `AWS::Scheduler::Schedule Target` resource\.

 `KmsKeyArn`   <a name="sam-statemachine-statemachineschedulev2-kmskeyarn"></a>
The ARN for a KMS Key that will be used to encrypt customer data\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[KmsKeyArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html#cfn-scheduler-schedule-kmskeyarn)` property of an `AWS::Scheduler::Schedule` resource\.

 `Name`   <a name="sam-statemachine-statemachineschedulev2-name"></a>
The name of the schedule\. If you don't specify a name, AWS SAM generates a name in the format `StateMachine-Logical-IDEvent-Source-Name` and uses that ID for the schedule name\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[Name](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html#cfn-scheduler-schedule-name)` property of an `AWS::Scheduler::Schedule` resource\.

 `OmitName`   <a name="sam-statemachine-statemachineschedulev2-omitname"></a>
By default, AWS SAM generates a name in the format `StateMachine-Logical-IDEvent-Source-Name` and uses that ID for the schedule name\. If this property is set to `true`, AWS CloudFormation generates a unique physical ID and uses that ID for the schedule name\.  
*Type*: Boolean  
*Required*: No  
*AWS CloudFormation compatibility*: This property is unique to AWS SAM and doesn't have an AWS CloudFormation equivalent\.



 `PermissionsBoundary`   <a name="sam-statemachine-statemachineschedulev2-permissionsboundary"></a>
The ARN of the policy used to set the permissions boundary for the role\.  
If `PermissionsBoundary` is defined, AWS SAM will apply the same boundaries to the scheduler schedule's target IAM role\.
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[PermissionsBoundary](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html#cfn-iam-role-permissionsboundary)` property of an `AWS::IAM::Role` resource\.

 `RetryPolicy`   <a name="sam-statemachine-statemachineschedulev2-retrypolicy"></a>
A `RetryPolicy` object that includes information about the retry policy settings\.  
*Type*: [RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-scheduler-schedule-target.html#cfn-scheduler-schedule-target-retrypolicy)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RetryPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-scheduler-schedule-target.html#cfn-scheduler-schedule-target-retrypolicy)` property of the `AWS::Scheduler::Schedule` `Target` data type\.

 `RoleArn`   <a name="sam-statemachine-statemachineschedulev2-rolearn"></a>
The ARN of the IAM role that EventBridge Scheduler will use for the target when the schedule is invoked\.  
*Type*: [RoleArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-scheduler-schedule-target.html#cfn-scheduler-schedule-target-rolearn)  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[RoleArn](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-scheduler-schedule-target.html#cfn-scheduler-schedule-target-rolearn)` property of the `AWS::Scheduler::Schedule` `Target` data type\.

 `ScheduleExpression`   <a name="sam-statemachine-statemachineschedulev2-scheduleexpression"></a>
The scheduling expression that determines when and how often the schedule runs\.  
*Type*: String  
*Required*: Yes  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ScheduleExpression](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html#cfn-scheduler-schedule-scheduleexpression)` property of an `AWS::Scheduler::Schedule` resource\.

 `ScheduleExpressionTimezone`   <a name="sam-statemachine-statemachineschedulev2-scheduleexpressiontimezone"></a>
The timezone in which the scheduling expression is evaluated\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[ScheduleExpressionTimezone](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html#cfn-scheduler-schedule-scheduleexpressiontimezone)` property of an `AWS::Scheduler::Schedule` resource\.

 `StartDate`   <a name="sam-statemachine-statemachineschedulev2-startdate"></a>
The date, in UTC, after which the schedule can begin invoking a target\. Depending on the schedule's recurrence expression, invocations might occur on, or after, the StartDate you specify\.  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[StartDate](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html#cfn-scheduler-schedule-startdate)` property of an `AWS::Scheduler::Schedule` resource\.

 `State`   <a name="sam-statemachine-statemachineschedulev2-state"></a>
The state of the schedule\.  
*Accepted values:* `DISABLED | ENABLED`  
*Type*: String  
*Required*: No  
*AWS CloudFormation compatibility*: This property is passed directly to the `[State](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html#cfn-scheduler-schedule-state)` property of an `AWS::Scheduler::Schedule` resource\.

## Examples<a name="sam-property-statemachine-statemachineschedulev2--examples"></a>

### Basic example of defining a ScheduleV2 resource<a name="sam-property-statemachine-statemachineschedulev2--examples--example1"></a>

```
StateMachine:
  Type: AWS::Serverless::StateMachine
  Properties:
    Name: MyStateMachine
    Events:
      ScheduleEvent:
        Type: ScheduleV2
        Properties:
          ScheduleExpression: "rate(1 minute)"
      ComplexScheduleEvent:
        Type: ScheduleV2
        Properties:
          ScheduleExpression: rate(1 minute)
          FlexibleTimeWindow:
            Mode: FLEXIBLE
            MaximumWindowInMinutes: 5
          StartDate: '2022-12-28T12:00:00.000Z'
          EndDate: '2023-01-28T12:00:00.000Z'
          ScheduleExpressionTimezone: UTC
          RetryPolicy:
            MaximumRetryAttempts: 5
            MaximumEventAgeInSeconds: 300
          DeadLetterConfig:
            Type: SQS
    DefinitionUri:
      Bucket: sam-demo-bucket
      Key: my-state-machine.asl.json
      Version: 3
    Policies:
      - LambdaInvokePolicy:
          FunctionName: !Ref MyFunction
```
