# Resource policy example<a name="serverless-controlling-access-to-apis-resource-policies"></a>

You can control access to your APIs by attaching a resource policy within your AWS SAM template\. To do this, you use the [ApiAuth](sam-property-api-apiauth.md) data type\.

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

For more information about resource policies, see [Controlling access to an API with API Gateway resource policies](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies.html) in the *API Gateway Developer Guide*\.