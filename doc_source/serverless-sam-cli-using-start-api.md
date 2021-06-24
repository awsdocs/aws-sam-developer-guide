# Running API Gateway locally<a name="serverless-sam-cli-using-start-api"></a>

Use the `sam local start\-api` command to start a local instance of API Gateway that you will use to test HTTP request/response functionality\. This functionality features hot reloading to enable you to quickly develop and iterate over your functions\.

**Note**  
"Hot reloading" is when only the files that changed are refreshed without losing the state of the application\. In contrast, "live reloading" is when the entire application is refreshed, such that the state of the application is lost\.

You must execute `sam local start-api` in the project directory containing the function you want to invoke\.

By default, AWS SAM uses Lambda proxy integrations, and supports both `HttpApi` and `Api` resource types\. For more information about proxy integrations for `HttpApi` resource types, see [Working with Lambda proxy integrations for HTTP APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-develop-integrations-lambda.html)\. For more information about proxy integrations with `Api` resource types, see [Understand API Gateway Lambda proxy integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-lambda-proxy-integrations.html#api-gateway-create-api-as-simple-proxy)\.

**Example**:

```
sam local start-api
```

AWS SAM automatically finds any functions within your AWS SAM template that have `HttpApi` or `Api` event sources defined\. Then, it mounts them at the defined HTTP paths\.

In the following `Api` example, the `Ratings` function mounts `ratings.py:handler()` at `/ratings` for `GET` requests:

```
Ratings:
  Type: AWS::Serverless::Function
  Properties:
    Handler: ratings.handler
    Runtime: python3.6
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

**Environment Variable File**

You can use the `--env-vars` argument with the `invoke` or `start-api` commands to provide a JSON file that contains values to override the environment variables already defined in your function template\. You can structure the file as follows:

```
{
  "MyFunction1": {
    "TABLE_NAME": "localtable",
    "BUCKET_NAME": "testBucket"
  },
  "MyFunction2": {
    "TABLE_NAME": "localtable",
    "STAGE": "dev"
  },
}
```

Alternatively, your environment file can contain a single `Parameters` entry with the environment variables for all functions\. Note that you can't mix this format with the example above\.

```
{
  "Parameters": {
    "TABLE_NAME": "localtable",
    "BUCKET_NAME": "testBucket",
    "STAGE": "dev"
  }
}
```

Save your environment variables in a file named `env.json`\. The following command uses this file to override the included environment variables:

```
sam local start-api --env-vars env.json
```

## Layers<a name="serverless-sam-cli-using-start-api-layers"></a>

If your application includes layers, see [Working with layers](serverless-sam-cli-layers.md) for more information about how to debug layers issues on your local host\.