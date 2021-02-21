# LTSI-Support-Bot

##### Created by Aamir Djearam (djearam2@gmail.com)

## Introduction

After working with the LTSI (Learning and Support Technology and Innovation) team at UVIC, I came to realize the sheer amount of people power required to organize and respond to tickets accordingly. I had suggested during a meeting that we create a sort of fillable form instead of the e-mail system that we use but recently decided that a support bot would increase efficiency even more.

This bot will be powered using Amazon Lex and be roughly based on the [Amazon Lex Support Bot Tutorial](https://github.com/aws-samples/amazon-lex-support-bot/edit/master/README.md) although this specific bot will also incorporate a function that ties into SNS and possibly even Amazon Connect (depending on time constraints)

This bot will also draw off of the document search bot built by Akash Jain and Rahul Kulkarni located [here](https://aws.amazon.com/blogs/machine-learning/build-a-document-search-bot-using-amazon-lex-and-amazon-elasticsearch-service/). While it will utilize relatively the same document search method it will also be capable of indexing videos (for video tutorials). It will not use cognito as well since users do not need to be authenticated (no privacy violations), this will also serve to be a form of cost-optomization.

Currently a ticket handler needs to manually read through every incoming ticket in our RT system and assign it accordingly which can often be a tedious process. The bot's objective is to mitigate this and to answer simple questions by redirecting clients to the correct resources. Essentially replacing a Level 1 Helpdesk position.

Before I start, I'd like to acknowledge the creators of the original AWS Support Bot Guide: Rumi Olsen (rumi@amazon.com) and Ryan Vanderwerf (ryvan@amazon.com)

Lets go over the components used in this bot:

#### Amazon Lex

"Amazon Lex is a service for building conversational interfaces into any application using voice and text. Amazon Lex provides the advanced deep learning functionalities of automatic speech recognition (ASR) for converting speech to text, and natural language understanding (NLU) to recognize the intent of the text, to enable you to build applications with highly engaging user experiences and lifelike conversational interactions. With Amazon Lex, the same deep learning technologies that power Amazon Alexa are now available to any developer, enabling you to quickly and easily build sophisticated, natural language, conversational bots (“chatbots”)." (aws.amazon.com/lex)

#### Amazon Polly

"Amazon Polly is a service that turns text into lifelike speech, allowing you to create applications that talk, and build entirely new categories of speech-enabled products. Polly's Text-to-Speech (TTS) service uses advanced deep learning technologies to synthesize natural sounding human speech. With dozens of lifelike voices across a broad set of languages, you can build speech-enabled applications that work in many different countries." (aws.amazon.com/polly)

##### Elasticsearch

"Amazon Elasticsearch Service is a fully managed service that makes it easy for you to deploy, secure, and run Elasticsearch cost effectively at scale. You can build, monitor, and troubleshoot your applications using the tools you love, at the scale you need. The service provides support for open source Elasticsearch APIs, managed Kibana, integration with Logstash and other AWS services, and built-in alerting and SQL querying. Amazon Elasticsearch Service lets you pay only for what you use – there are no upfront costs or usage requirements. With Amazon Elasticsearch Service, you get the ELK stack you need, without the operational overhead." (https://aws.amazon.com/elasticsearch-service/)

#### CloudTrail

"AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. This event history simplifies security analysis, resource change tracking, and troubleshooting. In addition, you can use CloudTrail to detect unusual activity in your AWS accounts. These capabilities help simplify operational analysis and troubleshooting." (https://aws.amazon.com/cloudtrail/)

#### Lambda

"AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers, creating workload-aware cluster scaling logic, maintaining event integrations, or managing runtimes. With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code as a ZIP file or container image, and Lambda automatically and precisely allocates compute execution power and runs your code based on the incoming request or event, for any scale of traffic. You can set up your code to automatically trigger from 140 AWS services or call it directly from any web or mobile app. You can write Lambda functions in your favorite language (Node.js, Python, Go, Java, and more) and use both serverless and container tools, such as AWS SAM or Docker CLI, to build, test, and deploy your functions." (aws.amazon.com/lambda)

#### S3

"Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. This means customers of all sizes and industries can use it to store and protect any amount of data for a range of use cases, such as data lakes, websites, mobile applications, backup and restore, archive, enterprise applications, IoT devices, and big data analytics. Amazon S3 provides easy-to-use management features so you can organize your data and configure finely-tuned access controls to meet your specific business, organizational, and compliance requirements. Amazon S3 is designed for 99.999999999% (11 9's) of durability, and stores data for millions of applications for companies all around the world." (aws.amazon.com/s3)

#### SNS

"Amazon Simple Notification Service (Amazon SNS) is a fully managed messaging service for both application-to-application (A2A) and application-to-person (A2P) communication.

The A2A pub/sub functionality provides topics for high-throughput, push-based, many-to-many messaging between distributed systems, microservices, and event-driven serverless applications. Using Amazon SNS topics, your publisher systems can fanout messages to a large number of subscriber systems including Amazon SQS queues, AWS Lambda functions and HTTPS endpoints, for parallel processing, and Amazon Kinesis Data Firehose. The A2P functionality enables you to send messages to users at scale via SMS, mobile push, and email." (aws.amazon.com/sns)

#### SES

"Amazon Simple Email Service (SES) is a cost-effective, flexible, and scalable email service that enables developers to send mail from within any application. You can configure Amazon SES quickly to support several email use cases, including transactional, marketing, or mass email communications. Amazon SES's flexible IP deployment and email authentication options help drive higher deliverability and protect sender reputation, while sending analytics measure the impact of each email. With Amazon SES, you can send email securely, globally, and at scale." (https://aws.amazon.com/ses/)

#### Connect

"Amazon Connect is an easy to use omnichannel cloud contact center that helps you provide superior customer service at a lower cost. Over 10 years ago, Amazon’s retail business needed a contact center that would give our customers personal, dynamic, and natural experiences. We couldn’t find one that met our needs, so we built it. We've now made this available for all businesses, and today thousands of companies ranging from 10 to tens of thousands of agents use Amazon Connect to serve millions of customers daily." (https://aws.amazon.com/connect/)

#### IAM

AWS Identity and Access Management (IAM) enables you to manage access to AWS services and resources securely. Using IAM, you can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources. (https://aws.amazon.com/iam/)

#### Cloudformation

"AWS CloudFormation gives you an easy way to model a collection of related AWS and third-party resources, provision them quickly and consistently, and manage them throughout their lifecycles, by treating infrastructure as code. A CloudFormation template describes your desired resources and their dependencies so you can launch and configure them together as a stack. You can use a template to create, update, and delete an entire stack as a single unit, as often as you need to, instead of managing resources individually. You can manage and provision stacks across multiple AWS accounts and AWS Regions." (https://aws.amazon.com/cloudformation/)

#### CloudTrail

"AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. This event history simplifies security analysis, resource change tracking, and troubleshooting. In addition, you can use CloudTrail to detect unusual activity in your AWS accounts. These capabilities help simplify operational analysis and troubleshooting." (https://aws.amazon.com/cloudtrail/)


### Preparation

To prepare it's important to understand how the different systems interact with each other and which permissions need to be enabled for them to access the required data. It's important to follow the AWS Best Practices which specifically state **GRANT LEAST PRIVILEGE** which is why there is two seperate IAM roles for the lambda functions.

![LTSI Support Bot](https://i.imgur.com/44oVJl0.png)

The bot will interface with the customer and if the customer is just looking to get redirected to the appropriate help page, the bot will pull a saved version of that webpage or tutorial video from a private S3 Bucket (private due to HIPAA requirements). If the request is level 2 helpdesk or higher, the bot will generate an e-mail ticket that is already pre-formatted which will be sent to the correct LTSI Support e-mail address. By having pre-formatted e-mails, the team is able to quickly respond to support requests and have the correct team member handle tickets. It also makes data analysis easier if the tickets can be pre-sorted.

### Creation

To start we will be building off of the template created by Akash and Rahul. In their template they have pre-configured an S3 Bucket, an Elasticache Cluster, two Lambda functions for indexing from the S3 Bucket into the cluster and from the pulling the correct data from the cluster into Lex. I will also include a step by step guide on how to build the model from scratch located here. 


