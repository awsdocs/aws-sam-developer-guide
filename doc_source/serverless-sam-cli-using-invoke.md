# Invoking Functions Locally<a name="serverless-sam-cli-using-invoke"></a>

You can invoke your function locally by using the `` command and providing its function logical ID and an event file\. Alternatively, `sam local invoke` also accepts `stdin` as an event\.

**Note**  
The `sam local invoke` command described in this section corresponds to the AWS CLI command [ `aws lambda invoke`](https://docs.aws.amazon.com/lambda/latest/dg/API_Invoke.html)\. You can use either version of this command to invoke a Lambda function that you've uploaded to the AWS Cloud\.

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

This animation shows invoking a Lambda function locally using Microsoft Visual Studio Code:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/serverless-application-model/latest/developerguide/images/sam-invoke.gif)

## Environment Variable File<a name="serverless-sam-cli-using-invoke-environment-file"></a>

You can use the `--env-vars` argument with the `invoke` or `start-api` commands\. You do this to provide a JSON file that contains values to override the environment variables that are already defined in your function template\. Structure the file as follows:

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

For example, if you save this content in a file named `env.json`, then the following command uses this file to override the included environment variables:

```
sam local invoke --env-vars env.json
```

## Layers<a name="serverless-sam-cli-using-invoke-layers"></a>

If your application includes layers, see [Working with layers](serverless-sam-cli-layers.md) for more information about how to debug layers issues on your local host\.