# LTSI-Support-Bot

##### Created by Aamir Djearam (djearam2@gmail.com)

## Introduction

After working with the LTSI (Learning and Support Technology and Innovation) team at UVIC, I came to realize the sheer amount of people power required to organize and respond to tickets accordingly. I had suggested during a meeting that we create a sort of fillable form instead of the e-mail system that we use but recently came up with the idea of making a support bot for the UVic Support website instead.

This bot will be powered using Amazon Lex and be roughly based on the [Amazon Lex Support Bot Tutorial](https://github.com/aws-samples/amazon-lex-support-bot/edit/master/README.md) although this specific bot will also incorporate a lambda function that ties into SNS and possibly even Amazon Connect (depending on time constraints)

Before I start, I'd like to acknowledge the creators of the original AWS Support Bot Guide: Rumi Olsen (rumi@amazon.com) and Ryan Vanderwerf (ryvan@amazon.com)

Lets go over the components used in this bot:

#### Amazon Lex

"Amazon Lex is a service for building conversational interfaces into any application using voice and text. Amazon Lex provides the advanced deep learning functionalities of automatic speech recognition (ASR) for converting speech to text, and natural language understanding (NLU) to recognize the intent of the text, to enable you to build applications with highly engaging user experiences and lifelike conversational interactions. With Amazon Lex, the same deep learning technologies that power Amazon Alexa are now available to any developer, enabling you to quickly and easily build sophisticated, natural language, conversational bots (“chatbots”)." (aws.amazon.com/lex)

#### Amazon Polly

"Amazon Polly is a service that turns text into lifelike speech, allowing you to create applications that talk, and build entirely new categories of speech-enabled products. Polly's Text-to-Speech (TTS) service uses advanced deep learning technologies to synthesize natural sounding human speech. With dozens of lifelike voices across a broad set of languages, you can build speech-enabled applications that work in many different countries." (aws.amazon.com/polly)

#### Lambda

"AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers, creating workload-aware cluster scaling logic, maintaining event integrations, or managing runtimes. With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code as a ZIP file or container image, and Lambda automatically and precisely allocates compute execution power and runs your code based on the incoming request or event, for any scale of traffic. You can set up your code to automatically trigger from 140 AWS services or call it directly from any web or mobile app. You can write Lambda functions in your favorite language (Node.js, Python, Go, Java, and more) and use both serverless and container tools, such as AWS SAM or Docker CLI, to build, test, and deploy your functions." (aws.amazon.com/lambda)


#### S3

"Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. This means customers of all sizes and industries can use it to store and protect any amount of data for a range of use cases, such as data lakes, websites, mobile applications, backup and restore, archive, enterprise applications, IoT devices, and big data analytics. Amazon S3 provides easy-to-use management features so you can organize your data and configure finely-tuned access controls to meet your specific business, organizational, and compliance requirements. Amazon S3 is designed for 99.999999999% (11 9's) of durability, and stores data for millions of applications for companies all around the world." (aws.amazon.com/s3)


#### SNS

"Amazon Simple Notification Service (Amazon SNS) is a fully managed messaging service for both application-to-application (A2A) and application-to-person (A2P) communication.

The A2A pub/sub functionality provides topics for high-throughput, push-based, many-to-many messaging between distributed systems, microservices, and event-driven serverless applications. Using Amazon SNS topics, your publisher systems can fanout messages to a large number of subscriber systems including Amazon SQS queues, AWS Lambda functions and HTTPS endpoints, for parallel processing, and Amazon Kinesis Data Firehose. The A2P functionality enables you to send messages to users at scale via SMS, mobile push, and email." (aws.amazon.com/sns)
