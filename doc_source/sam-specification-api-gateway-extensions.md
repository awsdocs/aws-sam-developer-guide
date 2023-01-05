# API Gateway extensions<a name="sam-specification-api-gateway-extensions"></a>

API Gateway extensions are extensions to the OpenAPI specification that support the AWS\-specific authorization and API Gateway\-specific API integrations\. For more information about API Gateway extensions, see [API Gateway Extensions to OpenAPI](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions.html)\.

AWS SAM supports a subset of API Gateway extensions\. To see which API Gateway extensions are supported by AWS SAM, see the following table\.


|  |  | 
| --- |--- |
|  API Gateway Extension  |  Supported by AWS SAM  | 
| [x\-amazon\-apigateway\-any\-method Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-any-method.html) | Yes | 
| [x\-amazon\-apigateway\-api\-key\-source Property](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-api-key-source.html) | No | 
| [x\-amazon\-apigateway\-auth Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-auth.html) | Yes | 
| [x\-amazon\-apigateway\-authorizer Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-authorizer.html) | Yes | 
| [x\-amazon\-apigateway\-authtype Property](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-authtype.html) | Yes | 
| [x\-amazon\-apigateway\-binary\-media\-types Property](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-binary-media-types.html) | Yes | 
| [x\-amazon\-apigateway\-documentation Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-documentation.html) | No | 
| [x\-amazon\-apigateway\-endpoint\-configuration Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-endpoint-configuration.html) | No | 
| [x\-amazon\-apigateway\-gateway\-responses Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-gateway-responses.html) | Yes | 
| [x\-amazon\-apigateway\-gateway\-responses\.gatewayResponse Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-gateway-responses.gatewayResponse.html) | Yes | 
| [x\-amazon\-apigateway\-gateway\-responses\.responseParameters Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-gateway-responses.responseParameters.html) | Yes | 
| [x\-amazon\-apigateway\-gateway\-responses\.responseTemplates Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-gateway-responses.responseTemplates.html) | Yes | 
| [x\-amazon\-apigateway\-integration Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-integration.html) | Yes | 
| [x\-amazon\-apigateway\-integration\.requestTemplates Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-integration-requestTemplates.html) | Yes | 
| [x\-amazon\-apigateway\-integration\.requestParameters Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-integration-requestParameters.html) | No | 
| [x\-amazon\-apigateway\-integration\.responses Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-integration-responses.html) | Yes | 
| [x\-amazon\-apigateway\-integration\.response Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-integration-response.html) | Yes | 
| [x\-amazon\-apigateway\-integration\.responseTemplates Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-integration-responseTemplates.html) | Yes | 
| [x\-amazon\-apigateway\-integration\.responseParameters Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-integration-responseParameters.html) | Yes | 
| [x\-amazon\-apigateway\-request\-validator Property](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-request-validator.html) | No | 
| [x\-amazon\-apigateway\-request\-validators Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-request-validators.html) | No | 
| [x\-amazon\-apigateway\-request\-validators\.requestValidator Object](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-request-validators.requestValidator.html) | No | 