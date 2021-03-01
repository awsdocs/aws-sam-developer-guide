# Customized response example<a name="serverless-controlling-access-to-apis-customize-response"></a>

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
      Runtime: nodejs12.x
      InlineCode: module.exports = async () => throw new Error('Check out the response headers!')
      Events:
        GetResource:
          Type: Api
          Properties:
            Path: /error
            Method: get
            RestApiId: !Ref MyApi
```

For more information about API Gateway responses, see [Gateway responses in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-gatewayResponse-definition.html) in the *API Gateway Developer Guide*\.