# Deploying using GitHub Actions<a name="deploying-using-github"></a>

To configure your [GitHub](https://github.com/) pipeline to automate the build and deployment of your AWS SAM application, you must first install the AWS SAM command line interface \(CLI\) on your host\. You can use [GitHub Actions](https://github.com/features/actions) in your GitHub workflow to help with this setup\.

The following example GitHub workflow sets up an Ubuntu host using a series of GitHub Actions, then runs AWS SAM CLI commands to build and deploy an AWS SAM application:

```
on:
  push:
    branches:
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v3
      - uses: aws-actions/setup-sam@v2
      - uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-2
      - run: sam build --use-container
      - run: sam deploy --no-confirm-changeset --no-fail-on-empty-changeset
```

For a list of available Amazon Elastic Container Registry \(Amazon ECR\) build container images for different runtimes, see [Image repositories](serverless-image-repositories.md)\.