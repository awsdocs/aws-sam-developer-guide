# Running API Gateway locally<a name="serverless-sam-cli-using-start-api"></a>

To start a local instance of Amazon API Gateway that you can use to test HTTP request/response functionality, use the `sam local start\-api` AWS SAM CLI command\. This functionality features hot reloading so that you can quickly develop and iterate over your functions\.

**Note**  
*Hot reloading* is when only the files that changed are refreshed, and the state of the application remains the same\. In contrast, *live reloading* is when the entire application is refreshed, and the state of the application is lost\.

You must run the sam local start\-api command in the project directory that contains the function that you want to invoke\.

By default, AWS SAM uses AWS Lambda proxy integrations and supports both `HttpApi` and `Api` resource types\. For more information about proxy integrations for `HttpApi` resource types, see [Working with AWS Lambda proxy integrations for HTTP APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-develop-integrations-lambda.html) in the *API Gateway Developer Guide*\. For more information about proxy integrations with `Api` resource types, see [Understand API Gateway Lambda proxy integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-lambda-proxy-integrations.html#api-gateway-create-api-as-simple-proxy) in the *API Gateway Developer Guide*\.

**Example**:

```
sam local start-api
```

AWS SAM automatically finds any functions within your AWS SAM template that have `HttpApi` or `Api` event sources defined\. Then, it mounts the function at the defined HTTP paths\.

In the following `Api` example, the `Ratings` function mounts `ratings.py:handler()` at `/ratings` for `GET` requests:

```
Ratings:
  Type: AWS::Serverless::Function
  Properties:
    Handler: ratings.handler
    Runtime: python3.9
    Events:
      Api:
        Type: Api
        Properties:
          Path: /ratings
          Method: get
```

Here is an example `Api` response:

```
// Example of a Proxy Integration response
exports.handler = (event, context, callback) => {
    callback(null, {
        statusCode: 200,
        headers: { "x-custom-header" : "my custom header value" },
        body: "hello world"
    });
}
```

## Environment variable file<a name="serverless-sam-cli-using-start-api-environment-variable"></a>

To declare environment variables locally that override values defined in your templates, do the following:

1. Create a JSON file that contains the environment variables to override\.

1. Use the `--env-vars` argument to override values defined in your templates\.

### Declaring environment variables<a name="serverless-sam-cli-using-invoke-environment-file-declaring"></a>

To declare environment variables that apply globally to all resources, specify a `Parameters` object like the following:

```
{
    "Parameters": {
        "TABLE_NAME": "localtable",
        "BUCKET_NAME": "testBucket",
        "STAGE": "dev"
    }
}
```

To declare different environment variables for each resource, specify objects for each resource like the following:

```
{
    "MyFunction1": {
        "TABLE_NAME": "localtable",
        "BUCKET_NAME": "testBucket",
    },
    "MyFunction2": {
        "TABLE_NAME": "localtable",
        "STAGE": "dev"
    }
}
```

When specifying objects for each resource, you can use the following identifiers, listed in order of highest to lowest precedence:

1. `logical_id`

1. `function_id`

1. `function_name`

1. Full path identifier

You can use both of the preceding methods of declaring environment variables together in a single file\. When doing so, environment variables that you provided for specific resources take precedence over global environment variables\.

Save your environment variables in a JSON file, such as `env.json`\.

### Overriding environment variable values<a name="serverless-sam-cli-using-start-api-environment-file-override"></a>

To override environment variables with those defined in your JSON file, use the `--env-vars` argument with the invoke or start\-api commands\. For example:

```
sam local start-api --env-vars env.json
```

## Layers<a name="serverless-sam-cli-using-start-api-layers"></a>

If your application includes layers, for information about how to debug issues with layers on your local host, see [Working with layers](serverless-sam-cli-layers.md)\.