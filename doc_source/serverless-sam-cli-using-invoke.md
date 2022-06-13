# Invoking functions locally<a name="serverless-sam-cli-using-invoke"></a>

You can invoke your function locally by using the `sam local invoke` command and providing its function logical ID and an event file\. Alternatively, `sam local invoke` also accepts `stdin` as an event\. For more information about events, see [Event](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-concepts.html#gettingstarted-concepts-event) in the *AWS Lambda Developer Guide*\. For details about event message formats from different AWS services, see [Working with other services](https://docs.aws.amazon.com/lambda/latest/dg/lambda-services.html) in the *AWS Lambda Developer Guide*\.

**Note**  
The `sam local invoke` command described in this section corresponds to the AWS CLI command [https://docs.aws.amazon.com/lambda/latest/dg/API_Invoke.html](https://docs.aws.amazon.com/lambda/latest/dg/API_Invoke.html)\. You can use either version of this command to invoke a Lambda function that you've uploaded to the AWS Cloud\.

You must execute `sam local invoke` in the project directory containing the function you want to invoke\.

Examples:

```
# Invoking function with event file
$ sam local invoke "Ratings" -e event.json

# Invoking function with event via stdin
$ echo '{"message": "Hey, are you there?" }' | sam local invoke --event - "Ratings"

# For more options
$ sam local invoke --help
```

## Environment variable file<a name="serverless-sam-cli-using-invoke-environment-file"></a>

You can use the `--env-vars` argument with the `invoke` or `start-api` commands\. You do this to provide a JSON file that contains values to override the environment variables that are already defined in your function template\. You can structure the file as follows:

```
{
  "MyFunction1": {
    "TABLE_NAME": "localtable",
    "BUCKET_NAME": "testBucket"
  },
  "MyFunction2": {
    "TABLE_NAME": "localtable",
    "STAGE": "dev"
  }
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
sam local invoke --env-vars env.json
```

## Layers<a name="serverless-sam-cli-using-invoke-layers"></a>

If your application includes layers, see [Working with layers](serverless-sam-cli-layers.md) for more information about how to debug layers issues on your local host\.