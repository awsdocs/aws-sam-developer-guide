# Lambda authorizer examples<a name="serverless-controlling-access-to-apis-lambda-authorizer"></a>

The `AWS::Serverless::Api` resource type supports two types of Lambda authorizers: `TOKEN` authorizers and `REQUEST` authorizers\. The `AWS::Serverless::HttpApi` resource type supports only `REQUEST` authorizers\. The following are examples of each type\.

## Lambda `TOKEN` authorizer example \(AWS::Serverless::Api\)<a name="serverless-controlling-access-to-apis-lambda-token-authorizer"></a>

You can control access to your APIs by defining a Lambda `TOKEN` authorizer within your AWS SAM template\. To do this, you use the [ApiAuth](sam-property-api-apiauth.md) data type\.

The following is an example AWS SAM template section for a Lambda `TOKEN` authorizer:

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
      Runtime: nodejs12.x
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
      Runtime: nodejs12.x
```

For more information about Lambda authorizers, see [Use API Gateway Lambda authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html) in the *API Gateway Developer Guide*\.

## Lambda `REQUEST` authorizer example \(AWS::Serverless::Api\)<a name="serverless-controlling-access-to-apis-lambda-request-authorizer"></a>

You can control access to your APIs by defining a Lambda `REQUEST` authorizer within your AWS SAM template\. To do this, you use the [ApiAuth](sam-property-api-apiauth.md) data type\.

The following is an example AWS SAM template section for a Lambda `REQUEST` authorizer:

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
      Runtime: nodejs12.x
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
      Runtime: nodejs12.x
```

For more information about Lambda authorizers, see [Use API Gateway Lambda authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html) in the *API Gateway Developer Guide*\.

## Lambda authorizer example \(AWS::Serverless::HttpApi\)<a name="serverless-controlling-access-to-apis-lambda-authorizer-httpapi"></a>

You can control access to your HTTP APIs by defining a Lambda authorizer within your AWS SAM template\. To do this, you use the [HttpApiAuth](sam-property-httpapi-httpapiauth.md) data type\.

The following is an example AWS SAM template section for a Lambda authorizer:

```
Resources:
  MyApi:
    Type: AWS::Serverless::HttpApi
    Properties:
      StageName: Prod
      Auth:
        DefaultAuthorizer: MyLambdaRequestAuthorizer
        Authorizers:
          MyLambdaRequestAuthorizer:
            FunctionArn: !GetAtt MyAuthFunction.Arn
            FunctionInvokeRole: !GetAtt MyAuthFunctionRole.Arn
            Identity:
              Headers:
                - Authorization
            AuthorizerPayloadFormatVersion: 2.0
            EnableSimpleResponses: true

  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: ./src
      Handler: index.handler
      Runtime: nodejs12.x
      Events:
        GetRoot:
          Type: HttpApi
          Properties:
            ApiId: !Ref MyApi
            Path: /
            Method: get
            PayloadFormatVersion: "2.0"

  MyAuthFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: ./src
      Handler: authorizer.handler
      Runtime: nodejs12.x
```