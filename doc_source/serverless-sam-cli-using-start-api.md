# Running API Gateway locally<a name="serverless-sam-cli-using-start-api"></a>

Use the `` command to start a local instance of API Gateway that you will use to test HTTP request/response functionality\. This functionality features hot reloading to enable you to quickly develop and iterate over your functions\.

**Note**  
"Hot reloading" is when only the files that changed are refreshed without losing the state of the application\. In contrast, "live reloading" is when the entire application is refreshed, such that the state of the application is lost\.

You must execute `sam local start-api` in the project directory containing the function you want to invoke\.

Example:

```
sam local start-api
```

AWS SAM automatically finds any functions within your AWS SAM template that have `Api` event sources defined\. Then, it mounts them at the defined HTTP paths\.

This animation shows running API Gateway locally using Microsoft Visual Studio Code:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/images/sam-start-api.gif)

In the following example, the `Ratings` function mounts `ratings.py:handler()` at `/ratings` for `GET` requests:

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

By default, AWS SAM uses [ Proxy Integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-create-api-as-simple-proxy-for-lambda.html) and expects the response from your Lambda function to include one or more of the following: `statusCode`, `headers`, or `body`\.

For example:

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

For examples in other AWS Lambda languages, see [ Proxy Integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-create-api-as-simple-proxy-for-lambda.html)\.

*Environment Variable File*

You can use the `--env-vars` argument with the `invoke` or `start-api` commands to provide a JSON file that contains values to override the environment variables already defined in your function template\. Structure the file as follows:

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

For example, if you save this content in a file named `env.json`, then the following command uses this file to override the included environment variables:

```
sam local start-api --env-vars env.json
```

## Layers<a name="serverless-sam-cli-using-start-api-layers"></a>

If your application includes layers, see [Working with layers](serverless-sam-cli-layers.md) for more information about how to debug layers issues on your local host\.