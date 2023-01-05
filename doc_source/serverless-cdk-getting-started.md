# Getting started with AWS SAM and the AWS CDK<a name="serverless-cdk-getting-started"></a>

This topic describes what you need to use the AWS SAM CLI with AWS CDK applications, and provides instructions for building and locally testing a simple AWS CDK application\.

## Prerequisites<a name="serverless-cdk-getting-started-prerequisites"></a>

To use the AWS SAM CLI with AWS CDK, you must install the AWS CDK, and the AWS SAM CLI\.
+ For information about installing the AWS CDK, see [Getting started with the AWS CDK](https://docs.aws.amazon.com/cdk/latest/guide/getting_started.html) in the *AWS Cloud Development Kit \(AWS CDK\) Developer Guide*\.
+ For information about installing the AWS SAM CLI, see [Installing the AWS SAM CLI](install-sam-cli.md)\.

## Creating and locally testing an AWS CDK application<a name="serverless-cdk-tutorial-hello-world"></a>

To locally test an AWS CDK application using the AWS SAM CLI, you must have a AWS CDK application that contains a Lambda function\. Use the following steps to create a basic AWS CDK application with a Lambda function\. For more information, see [Creating a serverless application using the AWS CDK](https://docs.aws.amazon.com/cdk/latest/guide/serverless_example.html) in the *AWS Cloud Development Kit \(AWS CDK\) Developer Guide*\.

**Note**  
The AWS SAM CLI supports AWS CDK v1 starting from version 1\.135\.0 and AWS CDK v2 starting from version 2\.0\.0\.

### Step 1: Create an AWS CDK application<a name="serverless-cdk-tutorial-hello-world-init.title"></a>

For this tutorial, initialize an AWS CDK application that uses TypeScript\.

**Command to run:**

------
#### [ AWS CDK v2 ]

```
mkdir cdk-sam-example
cd cdk-sam-example
cdk init app --language typescript
```

------
#### [ AWS CDK v1 ]

```
mkdir cdk-sam-example
cd cdk-sam-example
cdk init app --language typescript
npm install @aws-cdk/aws-lambda
```

------

### Step 2: Add a Lambda function to your application<a name="serverless-cdk-tutorial-hello-world-lambda.title"></a>

Replace the code in `lib/cdk-sam-example-stack.ts` with the following:

------
#### [ AWS CDK v2 ]

```
import { Stack, StackProps } from 'aws-cdk-lib';
import { Construct } from 'constructs';
import * as lambda from 'aws-cdk-lib/aws-lambda';

export class CdkSamExampleStack extends Stack {
  constructor(scope: Construct, id: string, props?: StackProps) {
    super(scope, id, props);

    new lambda.Function(this, 'MyFunction', {
      runtime: lambda.Runtime.PYTHON_3_7,
      handler: 'app.lambda_handler',
      code: lambda.Code.fromAsset('./my_function'),
    });
  }
}
```

------
#### [ AWS CDK v1 ]

```
import * as cdk from '@aws-cdk/core';
import * as lambda from '@aws-cdk/aws-lambda';

export class CdkSamExampleStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: StackProps) {
    super(scope, id, props);

    new lambda.Function(this, 'MyFunction', {
      runtime: lambda.Runtime.PYTHON_3_7,
      handler: 'app.lambda_handler',
      code: lambda.Code.fromAsset('./my_function'),
    });
  }
}
```

------

### Step 3: Add your Lambda function code<a name="serverless-cdk-tutorial-hello-world-lambda-code.title"></a>

Create a directory named `my_function`\. In that directory, create a file named `app.py`\.

**Command to run:**

```
mkdir my_function
cd my_function
touch app.py
```

Add the following code to `app.py`:

```
def lambda_handler(event, context):
    return "Hello from SAM and the CDK!"
```

### Step 4: Test your Lambda function<a name="serverless-cdk-tutorial-hello-init.title"></a>

You can use the AWS SAM CLI to locally invoke a Lambda function that you define in an AWS CDK application\. To do this, you need the function construct identifier and the path to your synthesized AWS CloudFormation template\.

**Command to run:**

```
cdk synth --no-staging
```

```
sam local invoke MyFunction --no-event -t ./cdk.out/CdkSamExampleStack.template.json
```

**Example output:**

```
Invoking app.lambda_handler (python3.7)
     
START RequestId: 5434c093-7182-4012-9b06-635011cac4f2 Version: $LATEST
"Hello from SAM and the CDK!"
END RequestId: 5434c093-7182-4012-9b06-635011cac4f2
REPORT RequestId: 5434c093-7182-4012-9b06-635011cac4f2	Init Duration: 0.32 ms	Duration: 177.47 ms	Billed Duration: 178 ms	Memory Size: 128 MB	Max Memory Used: 128 MB
```

For more information about options available to test AWS CDK applications using the AWS SAM CLI, see [Locally testing AWS CDK applications](serverless-cdk-testing.md)\.