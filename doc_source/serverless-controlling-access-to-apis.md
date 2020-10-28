# Controlling access to API Gateway APIs<a name="serverless-controlling-access-to-apis"></a>

To control who can access your Amazon API Gateway APIs, you can enable authorization within your AWS SAM template\.

AWS SAM supports several mechanisms for controlling access to your API Gateway APIs\. The set of supported mechanisms differs between `AWS::Serverless::HttpApi` and `AWS::Serverless::Api` resource types\.

The following table summarizes the mechanisms that each resource type supports\.


| Mechanisms for controlling access | AWS::Serverless::HttpApi | AWS::Serverless::Api | 
| --- | --- | --- | 
| Lambda authorizers | ✓ | ✓ | 
| IAM permissions |  | ✓ | 
| Amazon Cognito user pools | ✓ \* | ✓ | 
| API keys |  | ✓ | 
| Resource policies |  | ✓ | 
| OAuth 2\.0/JWT authorizers | ✓ |  | 

\* You can use Amazon Cognito as a JSON Web Token \(JWT\) issuer with the `AWS::Serverless::HttpApi` resource type\.
+ **Lambda authorizers** – A Lambda authorizer \(formerly known as a *custom authorizer*\) is a Lambda function that you provide to control access to your API\. When your API is called, this Lambda function is invoked with a request context or an authorization token that the client application provides\. The Lambda function responds whether the caller is authorized to perform the requested operation\.

  Both the `AWS::Serverless::HttpApi` and `AWS::Serverless::Api` resource types support Lambda authorizers\.

  For more information about Lambda authorizers with `AWS::Serverless::HttpApi`, see [Working with AWS Lambda authorizers for HTTP APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-lambda-authorizer.html) in the *API Gateway Developer Guide*\. For more information about Lambda authorizers with `AWS::Serverless::Api`, see [Use API Gateway Lambda authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html) in the *API Gateway Developer Guide*\.

  For examples of Lambda authorizers for either resource type, see [Lambda authorizer examples](serverless-controlling-access-to-apis-lambda-authorizer.md)\.
+ **IAM permissions** – You can control who can invoke your API using [AWS Identity and Access Management \(IAM\) permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_controlling.html)\. Users calling your API must be authenticated with IAM credentials\. Calls to your API succeed only if there is an IAM policy attached to the IAM user that represents the API caller, an IAM group that contains the user, or an IAM role that the user assumes\.

  Only the `AWS::Serverless::Api` resource type supports IAM permissions\.

  For more information, see [Control access to an API with IAM permissions](https://docs.aws.amazon.com/apigateway/latest/developerguide/permissions.html) in the *API Gateway Developer Guide*\. For an example, see [IAM permission example](serverless-controlling-access-to-apis-permissions.md)\.
+ **Amazon Cognito user pools** – Amazon Cognito user pools are user directories in Amazon Cognito\. A client of your API must first sign in a user to the user pool and obtain an identity or access token for the user\. Then the client calls your API with one of the returned tokens\. The API call succeeds only if the required token is valid\.

  The `AWS::Serverless::Api` resource type supports Amazon Cognito user pools\. The `AWS::Serverless::HttpApi` resource type supports the use of Amazon Cognito as a JWT issuer\.

  For more information, see [Control access to a REST API using Amazon Cognito User Pools as authorizer](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-integrate-with-cognito.html) in the *API Gateway Developer Guide*\. For an example, see [Amazon Cognito user pool example](serverless-controlling-access-to-apis-cognito-user-pool.md)\.
+ **API keys** – API keys are alphanumeric string values that you distribute to application developer customers to grant access to your API\.

  Only the `AWS::Serverless::Api` resource type supports API keys\.

  For more information about API keys, see [Creating and using usage plans with API keys](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html) in the *API Gateway Developer Guide*\. For an example of API keys, see [API key example](serverless-controlling-access-to-apis-keys.md)\.
+ **Resource policies** – Resource policies are JSON policy documents that you can attach to an API Gateway API\. Use resource policies to control whether a specified principal \(typically an IAM user or role\) can invoke the API\.

  Only the `AWS::Serverless::Api` resource type supports resource policies as a mechanism for controlling access to API Gateway APIs\.

  For more information about resource policies, see [Controlling access to an API with API Gateway resource policies](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-resource-policies.html) in the *API Gateway Developer Guide*\. For an example of resource policies, see [Resource policy example](serverless-controlling-access-to-apis-resource-policies.md)\.
+ **OAuth 2\.0/JWT authorizers** – You can use JWTs as a part of [OpenID Connect \(OIDC\)](https://openid.net/specs/openid-connect-core-1_0.html) and [OAuth 2\.0](https://oauth.net/2/) frameworks to control access to your APIs\. API Gateway validates the JWTs that clients submit with API requests, and allows or denies requests based on token validation and, optionally, scopes in the token\.

  Only the `AWS::Serverless::HttpApi` resource type supports OAuth 2\.0/JWT authorizers\.

  For more information, see [Controlling access to HTTP APIs with JWT authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html) in the *API Gateway Developer Guide*\. For an example, see [OAuth 2\.0/JWT authorizer example](serverless-controlling-access-to-apis-oauth2-authorizer.md)\.

## Choosing a mechanism to control access<a name="serverless-controlling-access-to-apis-choices"></a>

The mechanism that you choose to use for controlling access to your API Gateway APIs depends on a few factors\. For example, if you have a greenfield project without either authorization or access control set up, then Amazon Cognito user pools might be your best option\. This is because when you set up user pools, you also automatically set up both authentication and access control\.

However, if your application already has authentication set up, then using Lambda authorizers might be your best option\. This is because you can call your existing authentication service and return a policy document based on the response\. Also, if your application requires custom authentication or access control logic that user pools don't support, then Lambda authorizers might be your best option\.

When you've chosen which mechanism to use, see the corresponding section in [Examples](#serverless-controlling-access-to-apis-examples) for how to use AWS SAM to configure your application to use that mechanism\.

## Customizing error responses<a name="serverless-controlling-access-to-apis-responses"></a>

You can use AWS SAM to customize the content of some API Gateway error responses\. Only the `AWS::Serverless::Api` resource type supports customized API Gateway responses\.

For more information about API Gateway responses, see [Gateway responses in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-gatewayResponse-definition.html) in the *API Gateway Developer Guide*\. For an example of customized responses, see [Customized response example](serverless-controlling-access-to-apis-customize-response.md)\.

## Examples<a name="serverless-controlling-access-to-apis-examples"></a>
+ [Lambda authorizer examples](serverless-controlling-access-to-apis-lambda-authorizer.md)
+ [IAM permission example](serverless-controlling-access-to-apis-permissions.md)
+ [Amazon Cognito user pool example](serverless-controlling-access-to-apis-cognito-user-pool.md)
+ [API key example](serverless-controlling-access-to-apis-keys.md)
+ [Resource policy example](serverless-controlling-access-to-apis-resource-policies.md)
+ [OAuth 2\.0/JWT authorizer example](serverless-controlling-access-to-apis-oauth2-authorizer.md)
+ [Customized response example](serverless-controlling-access-to-apis-customize-response.md)