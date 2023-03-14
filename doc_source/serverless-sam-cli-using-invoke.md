# Invoking Lambda functions locally<a name="serverless-sam-cli-using-invoke"></a>

You can invoke your AWS Lambda function locally by using the `sam local invoke` AWS SAM CLI command and providing the function's logical ID and an event file\. Alternatively, sam local invoke also accepts `stdin` as an event\. For more information about events, see [Event](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-concepts.html#gettingstarted-concepts-event) in the *AWS Lambda Developer Guide*\. For information about event message formats from different AWS services, see [Using AWS Lambda with other services](https://docs.aws.amazon.com/lambda/latest/dg/lambda-services.html) in the *AWS Lambda Developer Guide*\.

**Note**  
The sam local invoke command corresponds to the AWS Command Line Interface \(AWS CLI\) command [https://awscli.amazonaws.com/v2/documentation/api/latest/reference/lambda/invoke.html](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/lambda/invoke.html)\. You can use either command to invoke a Lambda function\.

You must run the sam local invoke command in the project directory that contains the function that you want to invoke\.

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

### Overriding environment variable values<a name="serverless-sam-cli-using-invoke-environment-file-override"></a>

To override environment variables with those defined in your JSON file, use the `--env-vars` argument with the invoke or start\-api commands\. For example:

```
sam local invoke --env-vars env.json
```

## Layers<a name="serverless-sam-cli-using-invoke-layers"></a>

If your application includes layers, for information about how to debug issues with layers on your local host, see [Working with layers](serverless-sam-cli-layers.md)\.

## Learn more<a name="serverless-sam-cli-using-invoke-learn"></a>

For a hands\-on example of invoking functions locally, see [ Module 2 \- Run locally](https://s12d.com/sam-ws-en-local) in *The Complete AWS SAM Workshop*\.