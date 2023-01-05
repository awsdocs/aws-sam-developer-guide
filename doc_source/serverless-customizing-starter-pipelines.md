# Customizing starter pipelines<a name="serverless-customizing-starter-pipelines"></a>

As a CI/CD administrator, you may want to customize a starter pipeline template, and associated guided prompts, that developers in your organization can use to create pipeline configurations\.

The AWS SAM CLI uses Cookiecutter templates when creating starter templates\. For details about cookie cutter templates, [Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/README.html)\.

You can also customize the prompts that the AWS SAM CLI displays to users when creating pipeline configurations using the `sam pipeline init` command\. To customize user prompts, do the following:

1. **Create a `questions.json` file** – The `questions.json` file must be in the root of the project respository\. This is the same directory as the `cookiecutter.json` file\. To view the schema for the `questions.json` file, see [questions\.json\.schema](https://github.com/aws/aws-sam-cli/blob/2b831b29f76ac9c4e0cbcbd68b37f8f664e136d8/samcli/lib/pipeline/init/questions.json.schema)\. To view an example `questions.json` file, see [questions\.json](https://github.com/aws/aws-sam-cli-pipeline-init-templates/blob/main/Jenkins/two-stage-pipeline-template/questions.json)\.

1. **Map question keys with cookiecutter names** – Each object in the `questions.json` file needs a key that matches a name in the cookiecutter template\. This key matching is how the AWS SAM CLI maps user prompt responses to the cookie cutter template\. To see examples of this key matching, see the [Example files](#serverless-customizing-starter-pipelines-example-files) section later in this topic\. 

1. **Create a `metadata.json` file** – Declare the number of stages the pipeline will have in the `metadata.json` file\. The number of stages instructs the `sam pipeline init` command how many stages to prompt information about, or in the case of the `--bootstrap` option, how many stages to create infrastructure resources for\. To view an example `metadata.json` file that declares a pipeline with two stages, see [metadata\.json](https://github.com/aws/aws-sam-cli-pipeline-init-templates/blob/main/Jenkins/two-stage-pipeline-template/metadata.json)\.

## Example projects<a name="serverless-customizing-starter-pipelines-example-projects"></a>

Here are example projects, which each include a Cookiecutter template, a `questions.json` file, and a `metadata.json` file:
+ Jenkins example: [Two\-stage Jenkins pipeline template](https://github.com/aws/aws-sam-cli-pipeline-init-templates/tree/main/Jenkins/two-stage-pipeline-template)
+ CodePipeline example: [Two stage CodePipeline pipeline template](https://github.com/aws/aws-sam-cli-pipeline-init-templates/tree/main/AWS-CodePipeline/two-stage-pipeline-template)

## Example files<a name="serverless-customizing-starter-pipelines-example-files"></a>

The following set of files show how questions in the `questions.json` file are associated with entries in the Cookiecutter template file\. Note that these examples are file snippets, not full files\. To see examples of full files, see the [Example projects](#serverless-customizing-starter-pipelines-example-projects) section earlier in this topic\.

Example **`questions.json`**:

```
{
  "questions": [{
    "key": "intro",
    "question": "\nThis template configures a pipeline that deploys a serverless application to a testing and a production stage.\n",
    "kind": "info"
  }, {
    "key": "pipeline_user_jenkins_credential_id",
    "question": "What is the Jenkins credential ID (via Jenkins plugin \"aws-credentials\") for pipeline user access key?",
    "isRequired": true
  }, {
    "key": "sam_template",
    "question": "What is the template file path?",
    "default": "template.yaml"
  }, {
    ...
```

Example **`cookiecutter.json`**:

```
{
  "outputDir": "aws-sam-pipeline",
  "pipeline_user_jenkins_credential_id": "",
  "sam_template": "",
    ...
```

Example **`Jenkinsfile`**:

```
pipeline {
  agent any
  environment {
    PIPELINE_USER_CREDENTIAL_ID = '{{cookiecutter.pipeline_user_jenkins_credential_id}}'
    SAM_TEMPLATE = '{{cookiecutter.sam_template}}'
    ...
```