# Controlling Access to API Gateway APIs<a name="serverless-controlling-access-to-apis"></a>

You can use AWS SAM to control who can access your API Gateway APIs by enabling authorization within your AWS SAM template\.

AWS SAM supports several mechanisms for controlling access to your API Gateway APIs:
+ **Lambda authorizers**\. A Lambda authorizer \(formerly known as a *custom authorizer*\) is a Lambda function that you provide to control access to your API\. When your API is called, this Lambda function is invoked with a request context or an authorization token that is provided by the client application\. The Lambda function returns a policy document that specifies the operations that the caller is authorized to perform, if any\. For more information about Lambda authorizers, see [Use API Gateway Lambda Authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html) in the *API Gateway Developer Guide*\. For examples of Lambda authorizers, see [Example: Defining Lambda Token Authorizers](#serverless-controlling-access-to-apis-lambda-token-authorizer) and [Example: Defining Lambda Request Authorizers](#serverless-controlling-access-to-apis-lambda-request-authorizer) later in this topic\.

   
+ **Amazon Cognito user pools**\. Amazon Cognito user pools are user directories in Amazon Cognito\. A client of your API must first sign a user in to the user pool, and obtain an identity or access token for the user\. Then your API is called with one of the returned tokens\. The API call succeeds only if the required token is valid\. For more information about Amazon Cognito user pools, see [Control Access to REST API Using Amazon Cognito User Pools as Authorizer](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-integrate-with-cognito.html) in the *API Gateway Developer Guide*\. For an example of Amazon Cognito user pools, see [Example: Defining Amazon Cognito User Pools](#serverless-controlling-access-to-apis-cognito-user-pool) later in this topic\.

   
+ **IAM permissions**\. You can control who can invoke your API using [IAM permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_permissions.html)\. Users calling your API must be authenticated with IAM credentials\. Calls to your API only succeed if there is an IAM policy attached to the IAM user that represents the API caller, an IAM group that contains the user, or an IAM role that is assumed by the user\. For more information about IAM permissions, see [Control Access to an API with IAM Permissions](https://docs.aws.amazon.com/apigateway/latest/developerguide/permissions.html) in the *API Gateway Developer Guide*\. For an example of IAM permissions, see [Example: Defining IAM Permissions](#serverless-controlling-access-to-apis-permissions) later in this topic\.

   
+ **API keys**\. API keys are alphanumeric string values that you distribute to application developer customers to grant access to your API\. For more information about API keys, see [Create and Use Usage Plans with API Keys](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html) in the *API Gateway Developer Guide*\. For an example of API keys, see [Example: Defining API Keys](#serverless-controlling-access-to-apis-keys) later in this topic\.

   
+ **Resource policies**\. Resource policies are JSON policy documents that you can attach to an API Gateway API to control whether a specified principal \(typically an IAM user or role\) can invoke the API\. For more information about resource policies, see [Control Access to an API with Amazon API Gateway Resource Policies](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies.html) in the *API Gateway Developer Guide*\. For an example of resource policies, see [Example: Defining Resource Policies](#serverless-controlling-access-to-apis-resource-policies) later in this topic\.

In addition, you can use AWS SAM to customize the content of some API Gateway error responses\. For more information about customizing API Gateway error responses, see [Set Up Gateway Responses to Customize Error Responses](https://docs.aws.amazon.com/apigateway/latest/developerguide/customize-gateway-responses.html)\. For an example of customized responses, see [Example: Defining Customized Responses](#serverless-controlling-access-to-apis-customize-response) later in this topic\.

## Choosing a Mechanism to Control Access<a name="serverless-controlling-access-to-apis-choices"></a>

The mechanism that you choose to control access to your API Gateway APIs depends on a few factors\. For example, if you have a greenfield project that doesn't have either authorization or access control set up yet, then Amazon Cognito user pools might be your best option\. This is because when you set up user pools, you also set up both authentication and access control automatically\. 

However, if your application already has authentication set up, then using Lambda authorizers might be the best option\. This is because you can call your existing authentication service and return a policy document based on the response\. Also, if your application requires custom authentication or access control logic that user pools don't support, then Lambda authorizers might be your best option\.

After you've decided which mechanism to use, see the corresponding section in this topic to see how to use AWS SAM to configure your application to use that mechanism\.

## Example: Defining Lambda Token Authorizers<a name="serverless-controlling-access-to-apis-lambda-token-authorizer"></a>

You can control access to your APIs by defining a Lambda Token authorizer within your AWS SAM template\. To do this, you use the [API Auth Object](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#api-auth-object) data type\.

The following is an example AWS SAM template section for a Lambda Token authorizer:

```
Resources:
  MyApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: Prod
      Auth:
        DefaultAuthorizer: MyLambdaTokenAuthorizer
        Authorizers:
          MyLambdaTokenAuthorizer:
            FunctionArn: !GetAtt MyAuthFunction.Arn

  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: ./src
      Handler: index.handler
      Runtime: nodejs8.10
      Events:
        GetRoot:
          Type: Api
          Properties:
            RestApiId: !Ref MyApi
            Path: /
            Method: get

  MyAuthFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: ./src
      Handler: authorizer.handler
      Runtime: nodejs8.10
```

For more information about API Gateway Lambda authorizers, see [Use API Gateway Lambda Authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html) in the *API Gateway Developer Guide*\.

For a full sample application that includes a Lambda Token authorizer, see [API Gateway \+ Lambda TOKEN Authorizer Example](https://github.com/awslabs/serverless-application-model/tree/master/examples/2016-10-31/api_lambda_token_auth)\.

## Example: Defining Lambda Request Authorizers<a name="serverless-controlling-access-to-apis-lambda-request-authorizer"></a>

You can control access to your APIs by defining a Lambda Request authorizer within your AWS SAM template\. To do this, you use the [API Auth Object](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#api-auth-object) data type\.

The following is an example AWS SAM template section for a Lambda Request authorizer:

```
Resources:
  MyApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: Prod
      Auth:
        DefaultAuthorizer: MyLambdaRequestAuthorizer
        Authorizers:
          MyLambdaRequestAuthorizer:
            FunctionPayloadType: REQUEST
            FunctionArn: !GetAtt MyAuthFunction.Arn
            Identity:
              QueryStrings:
                - auth

  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: ./src
      Handler: index.handler
      Runtime: nodejs8.10
      Events:
        GetRoot:
          Type: Api
          Properties:
            RestApiId: !Ref MyApi
            Path: /
            Method: get

  MyAuthFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: ./src
      Handler: authorizer.handler
      Runtime: nodejs8.10
```

For more information about API Gateway Lambda authorizers, see [Use API Gateway Lambda Authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html) in the *API Gateway Developer Guide*\.

For a full sample application that includes a Lambda Request authorizer, see [API Gateway \+ Lambda REQUEST Authorizer Example](https://github.com/awslabs/serverless-application-model/tree/master/examples/2016-10-31/api_lambda_request_auth)\.

## Example: Defining Amazon Cognito User Pools<a name="serverless-controlling-access-to-apis-cognito-user-pool"></a>

You can control access to your APIs by defining Amazon Cognito user pools within your AWS SAM template\. To do this, you use the [API Auth Object](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#api-auth-object) data type\.

The following is an example AWS SAM template section for a user pool:

```
Resources:
  MyApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: Prod
      Cors: "'*'"
      Auth:
        DefaultAuthorizer: MyCognitoAuthorizer
        Authorizers:
          MyCognitoAuthorizer:
            UserPoolArn: !GetAtt MyCognitoUserPool.Arn

  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: ./src
      Handler: lambda.handler
      Runtime: nodejs8.10
      Events:
        Root:
          Type: Api
          Properties:
            RestApiId: !Ref MyApi
            Path: /
            Method: GET

  MyCognitoUserPool:
    Type: AWS::Cognito::UserPool
    Properties:
      UserPoolName: !Ref CognitoUserPoolName
      Policies:
        PasswordPolicy:
          MinimumLength: 8
      UsernameAttributes:
        - email
      Schema:
        - AttributeDataType: String
          Name: email
          Required: false
  
  MyCognitoUserPoolClient:
    Type: AWS::Cognito::UserPoolClient
    Properties:
      UserPoolId: !Ref MyCognitoUserPool
      ClientName: !Ref CognitoUserPoolClientName
      GenerateSecret: false
```

For more information about Amazon Cognito user pools, see [Control Access to a REST API Using Amazon Cognito User Pools as Authorizer ](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-integrate-with-cognito.html) in the *API Gateway Developer Guide*\.

For a full sample application that includes a user pool as an authorizer, see [API Gateway \+ Cognito Auth \+ Cognito Hosted Auth Example](https://github.com/awslabs/serverless-application-model/tree/master/examples/2016-10-31/api_cognito_auth)\.

## Example: Defining IAM Permissions<a name="serverless-controlling-access-to-apis-permissions"></a>

You can control access to your APIs by defining IAM permissions within your AWS SAM template\. To do this, you use the [API Auth Object](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#api-auth-object) data type\.

The following is an example AWS SAM template section for IAM permissions:

```
Resources:
  MyApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: Prod
      Auth:
        DefaultAuthorizer: AWS_IAM

  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: .
      Handler: index.handler
      Runtime: nodejs8.10
      Events:
        GetRoot:
          Type: Api
          Properties:
            RestApiId: !Ref MyApi
            Path: /
            Method: get
```

For more information about IAM permissions, see [Control Access to an API Using IAM Permissions](https://docs.aws.amazon.com/apigateway/latest/developerguide/permissions.html) in the *API Gateway Developer Guide*\.

For a full sample application that includes a user pool as an authorizer, see [API Gateway \+ IAM Permissions Example](https://github.com/awslabs/serverless-application-model/tree/master/examples/2016-10-31/api_aws_iam_auth)\.

## Example: Defining API Keys<a name="serverless-controlling-access-to-apis-keys"></a>

You can control access to your APIs by requiring API keys within your AWS SAM template\. To do this, you use the [API Auth Object](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#api-auth-object) data type\.

The following is an example AWS SAM template section for API keys:

```
Resources:
  MyApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: Prod
      Auth:
        ApiKeyRequired: true # sets for all methods

  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: .
      Handler: index.handler
      Runtime: nodejs8.10
      Events:
        ApiKey:
          Type: Api
          Properties:
            RestApiId: !Ref MyApi
            Path: /
            Method: get
            Auth:
              ApiKeyRequired: true
```

For more information about API keys, see [Create and Use Usage Plans with API Keys](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html) in the *API Gateway Developer Guide*\.

## Example: Defining Resource Policies<a name="serverless-controlling-access-to-apis-resource-policies"></a>

You can control access to your APIs by attaching a resource policy within your AWS SAM template\. To do this, you use the [API Auth Object](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#api-auth-object) data type\.

The following is an example AWS SAM template section for resource policies:

```
Resources:
  ExplicitApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: Prod
      EndpointConfiguration: PRIVATE
      Auth:
        ResourcePolicy:
          CustomStatements: {
              Effect: 'Allow',
              Action: 'execute-api:Invoke', 
              Resource: ['execute-api:/*/*/*'],
              Principal: '*'
            }
  MinimalFunction:
    Type: 'AWS::Serverless::Function'
    Properties:
      CodeUri: s3://sam-demo-bucket/hello.zip
      Handler: hello.handler
      Runtime: python2.7
      Events:
        AddItem:
          Type: Api
          Properties:
            RestApiId: 
              Ref: ExplicitApi
            Path: /add
            Method: post
```

For more information about resource policies, see [Control Access to an API with Amazon API Gateway Resource Policies](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies.html) in the *API Gateway Developer Guide*\.

## Example: Defining Customized Responses<a name="serverless-controlling-access-to-apis-customize-response"></a>

You can customize some API Gateway error responses by defining response headers within your AWS SAM template\. To do this, you use the [Gateway Response Object](https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#gateway-response-object) data type\.

The following is an example AWS SAM template section for API Gateway responses:

```
Resources:
  MyApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: Prod
      GatewayResponses:
        DEFAULT_4xx:
          ResponseParameters:
            Headers:
              Access-Control-Expose-Headers: "'WWW-Authenticate'"
              Access-Control-Allow-Origin: "'*'"

  GetFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: index.get
      Runtime: nodejs6.10
      InlineCode: module.exports = async () => throw new Error('Check out the response headers!')
      Events:
        GetResource:
          Type: Api
          Properties:
            Path: /error
            Method: get
            RestApiId: !Ref MyApi
```

For more information about customizing API Gateway messages, see [Set Up Gateway Responses to Customize Error Responses](https://docs.aws.amazon.com/apigateway/latest/developerguide/customize-gateway-responses.html) in the *API Gateway Developer Guide*\.

For a full sample application that includes a customized error response, see [API Gateway \+ GatewayResponse Example](https://github.com/awslabs/serverless-application-model/tree/master/examples/2016-10-31/api_gateway_responses)\.