# Telemetry in the AWS SAM CLI<a name="serverless-sam-telemetry"></a>

At AWS, we develop and launch services based on what we learn from interactions with customers\. We use customer feedback to iterate on our product\. Telemetry is additional information that helps us to better understand our customers' needs, diagnose issues, and deliver features that improve the customer experience\.

The AWS SAM command line interface \(CLI\) collects telemetry, such as generic usage metrics, system and environment information, and errors\. For details about the types of telemetry collected, see [Types of information collected](#serverless-sam-telemtry-data-collected)\.

The AWS SAM CLI does **not** collect personal information, such as user names or email addresses\. It also does not extract sensitive project\-level information\.

Customers control whether telemetry is turned on, and they can change their settings at any point of time\. If telemetry remains on, the AWS SAM CLI sends telemetry data in the background without requiring any additional customer interaction\.

## Turn off telemetry for a session<a name="serverless-sam-telemtry-opt-out"></a>

In macOS and Linux operating systems, you can turn off telemetry for a single session\. To turn off telemetry for your current session, run the following command to set the environment variable `SAM_CLI_TELEMETRY` to `false`\. Repeat the command for each new terminal or session\.

```
export SAM_CLI_TELEMETRY=0
```

## Turn off telemetry for your profile in all sessions<a name="serverless-sam-telemtry-opt-out"></a>

Run the following commands to turn off telemetry for all sessions when you're running the AWS SAM CLI on your operating system\.

**To turn off telemetry in Linux**

1. Run:

   ```
   echo "export SAM_CLI_TELEMETRY=0" >>~/.profile
   ```

1. Run:

   ```
   source ~/.profile
   ```

**To turn off telemetry in macOS**

1. Run:

   ```
   echo "export SAM_CLI_TELEMETRY=0" >>~/.profile
   ```

1. Run:

   ```
   source ~/.profile
   ```

**To turn off telemetry in Windows**

1. Run:

   ```
   setx SAM_CLI_TELEMETRY 0
   ```

1. Run:

   ```
   refreshenv
   ```

## Types of information collected<a name="serverless-sam-telemtry-data-collected"></a>
+ **Usage information** – The generic commands and subcommands that customers run\.
+ **Errors and diagnostic information** – The status and duration of commands that customers run, including exit codes, internal exception names, and failures when connecting to Docker\.
+ **System and environment information** – The Python version, operating system \(Windows, Linux, or macOS\), environment in which the AWS SAM CLI runs \(for example, AWS CodeBuild, an AWS IDE toolkit, or a terminal\), and hash values of usage attributes\.

## Learn more<a name="serverless-sam-telemtry-learn-more"></a>

The telemetry data that the AWS SAM CLI collects adheres to the AWS data privacy policies\. For more information, see the following:
+ [AWS Service Terms](http://aws.amazon.com/service-terms/)
+ [Data Privacy FAQ](http://aws.amazon.com/compliance/data-privacy-faq/)