# Serverless concepts<a name="what-is-concepts"></a>

Learn about basic serverless concepts before using the AWS Serverless Application Model \(AWS SAM\)\.

## Serverless concepts<a name="what-is-concepts-terms"></a>

**Event\-driven architecture**  <a name="what-is-concepts-terms-eda"></a>
A serverless application consists of individual AWS services, such as AWS Lambda for compute and Amazon DynamoDB for database management, that each perform a specialized role\. These services are then loosely integrated with each other through an event\-driven architecture\. To learn more about event\-driven architecture, see [What is an Event\-Driven Architecture?](https://aws.amazon.com/event-driven-architecture/)\. 

**Infrastructure as Code \(IaC\)**  <a name="what-is-concepts-terms-iac"></a>
Infrastructure as Code \(IaC\) is a way of treating infrastructure in the same way that developers treat code, applying the same rigor of application code development to infrastructure provisioning\. You define your infrastructure in a template file, deploy it to AWS, and AWS creates the resources for you\. With IAC, you define in code what you want AWS to provision\. For more information, see [Infrastructure as Code](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/infrastructure-as-code.html) in the *Introduction to DevOps on AWS* AWS Whitepaper\.

**Serverless technologies**  <a name="what-is-concepts-terms-serverless"></a>
With AWS serverless technologies, you can build and run applications without having to manage your own servers\. All server management is done by AWS, providing many benefits such as automatic scaling and built\-in high availability, letting you take your idea to production quickly\. Using serverless technologies, you can focus on the core of your product without having to worry about managing and operating servers\. To learn more about serverless, see the following:  
+ [Serverless on AWS](https://aws.amazon.com/serverless/)
+ [ Serverless Developer Guide](https://docs.aws.amazon.com/serverless/latest/devguide/serverless-preface.html) – Provides a conceptual overview of serverless development in the AWS Cloud\.
For a basic introduction to the core AWS serverless services, see [Serverless 101: Understanding the serverless services](https://serverlessland.com/learn/serverless-101) at *Serverless Land*\.

## Next steps<a name="what-is-concepts-next"></a>

For an introduction to AWS SAM, see [What is the AWS Serverless Application Model \(AWS SAM\)?](what-is-sam.md)