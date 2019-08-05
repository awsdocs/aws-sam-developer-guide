# Telemetry in the AWS SAM CLI<a name="serverless-sam-telemetry"></a>

SAM CLI includes telemetry\. In addition to existing feedback, telemetry allows us to better understand our customer’s needs, common CLI scenarios and existing issues\. The information collected will include generic usage metrics, system and environment information, and errors \(see below for types of information collected\)\. These generic metrics will inform our product decisions and help us continue to deliver features and enhancements that improve the customer experience\. This feature does not collect personal information, such as usernames or email addresses, or extract sensitive project\-level information and customers control whether telemetry is enabled and can change their settings at any point of time\. 

Customers new to SAM CLI, upon first use after installation, will be provided with a message prompt informing them that telemetry collection is enabled and will provide the customer with instructions on how to opt out \(see instructions for opt out below\)\. 

Customers already using SAM CLI, including as a part of automated CI/CD systems, will be provided with the message prompt upon first use after update or next install\. If telemetry remains enabled, we will send telemetry data in the background without requiring any additional customer interaction\.

**Note**  
The message prompt will only appear upon the first update or install after the launch of the telemetry feature, and not upon every update thereafter\.

## Disabling Telemetry for a Session<a name="serverless-sam-telemtry-opt-out"></a>

In macOS and Linux operating systems, you can disable telemetry for a single session\. To disable telemetry for your current session, run the following command to set the environment variable `SAM_CLI_TELEMETRY` to `false`\. You must repeat the command for each new terminal or session\. 

```
export SAM_CLI_TELEMETRY=0
```

## Disabling Telemetry for Your Profile in All Sessions<a name="serverless-sam-telemtry-opt-out"></a>

Run the following commands to disable telemetry for all sessions when you're running the AWS SAM CLI on your operating system\.

**To disable telemetry in Linux**

1. Run:

   ```
   echo "export SAM_CLI_TELEMETRY=0" >>~/.profile
   ```

1. Run:

   ```
   source ~/.profile
   ```

**To disable telemetry in macOS**

1. Run:

   ```
   echo "export SAM_CLI_TELEMETRY=0" >>~/.profile
   ```

1. Run:

   ```
   source ~/.profile
   ```

**To disable telemetry in Windows**

1. Run:

   ```
   setx SAM_CLI_TELEMETRY 0
   ```

1. Run:

   ```
   refreshenv
   ```

## Types of Information Collected<a name="serverless-sam-telemtry-data-collected"></a>
+ **Usage information** – The generic commands and subcommands that are run\.
+ **Errors and diagnostic information** – The status and duration of commands that are run, including exit codes, internal exception names, and failures when connecting to Docker\.
+ **System and environment information** – The Python version, operating system \(Windows, Linux, or macOS\), and environment in which the AWS SAM CLI is configured \(for example, AWS CodeBuild, an AWS IDE toolkit, or a terminal\)\.

## Learn More<a name="serverless-sam-telemtry-learn-more"></a>

The telemetry data that's collected adheres to the AWS data privacy policies\. For more information, see the following:
+ [AWS Service Terms](https://aws.amazon.com/service-terms/)
+ [Data Privacy](https://aws.amazon.com/compliance/data-privacy-faq/)