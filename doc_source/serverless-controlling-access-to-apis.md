# Controlling Access to API Gateway APIs<a name="serverless-controlling-access-to-apis"></a>

You can use AWS SAM to control who can access your API Gateway APIs by enabling authorization within your AWS SAM template\.

AWS SAM supports a few mechanisms for controlling access to your API Gateway APIs:
+ **Lambda authorizers**\. A Lambda authorizer \(formerly known as a *custom authorizer*\) is a Lambda function that you provide to control access to your API\. When your API is called, this Lambda function is invoked with a request context and an authorization token that are provided by the client application\. The Lambda function returns a policy document that specifies the operations that the caller is authorized to perform, if any\. For more information about Lambda authorizers, see [Use API Gateway Lambda Authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html) in the *API Gateway Developer Guide*\. For examples of Lambda authorizers, see the [Defining Lambda Token Authorizers](#serverless-controlling-access-to-apis-lambda-token-authorizer) and [Defining Lambda Token Authorizers](#serverless-controlling-access-to-apis-lambda-request-authorizer) sections in this topic\.

   
+ **Amazon Cognito user pools**\. Amazon Cognito user pools are user directories in Amazon Cognito\. A client of your API must first sign a user in to the user pool and obtain an identity or access token for the user\. Then your API is called with one of the returned tokens\. The API call succeeds only if the required token is valid\. For more information about Amazon Cognito user pools, see [Control Access to REST API Using Amazon Cognito User Pools as Authorizer](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-integrate-with-cognito.html) in the *API Gateway Developer Guide*\. For an example of Amazon Cognito user pools, see the [Defining Cognito User Pools](#serverless-controlling-access-to-apis-cognito-user-pool) section\.

## Choosing a Mechanism to Control Access<a name="serverless-controlling-access-to-apis-choices"></a>

The mechanism that you choose to control access to your API Gateway APIs depends on a few factors\. For example, if you have a greenfield project that doesn't have either authorization or access control set up yet, then Amazon Cognito user pools might be your best option\. This is because by setting up user pools, you also set up both authentication and access control automatically\. 

However, if your application already has authentication set up, then using Lambda authorizers might be the best option\. This is because you can call your existing authentication service and return a policy document based on the response\. Also, if the nature of your application requires custom authentication and/or access control logic that user pools don't support, then Lambda authorizers might again be your best option\.

After you've decided which mechanism to use, see the corresponding section in this topic to see how to use AWS SAM to configure your application to use that mechanism\.

## Defining Lambda Token Authorizers<a name="serverless-controlling-access-to-apis-lambda-token-authorizer"></a>

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

## Defining Lambda Request Authorizers<a name="serverless-controlling-access-to-apis-lambda-request-authorizer"></a>

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

## Defining Cognito User Pools<a name="serverless-controlling-access-to-apis-cognito-user-pool"></a>

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