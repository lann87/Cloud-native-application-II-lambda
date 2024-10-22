## Brief

### Preparation

Write about any preparations needed for the lesson, such as tools, installations, prior-knowledge, etcs.

### Lesson Overview

Write about how instructors can brief the students at the start of the lesson. It is good to guide students through what is going to be covered and the outcome. Setting expectations.

---

## Part 1 - Recap Prev Session

Instructor recap the material from previous session.

```Create new serverless application```

**Create new serverless application with S3 Event**

![image](https://user-images.githubusercontent.com/106639884/209033278-ae7f9602-f7d9-4b08-9990-bcc9e4620c34.png)


Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. Customers of all sizes and industries can use Amazon S3 to store and protect any amount of data for a range of use cases, such as data lakes, websites, mobile applications, backup and restore, archive, enterprise applications, IoT devices, and big data analytics. Amazon S3 provides management features so that you can optimize, organize, and configure access to your data to meet your specific business, organizational, and compliance requirements.

**S3 Event for Serverless**

```
functions:
  resize:
    handler: resize.handler
    events:
      - s3: photos
```

---

## Part 2 - Event

### SNS

![image](https://user-images.githubusercontent.com/106639884/209033249-11b6ab17-0f25-42de-91cc-34af6a610f67.png)


Amazon Simple Notification Service (Amazon SNS) is a web service that coordinates and manages the delivery or sending of messages to subscribing endpoints or clients.

In Amazon SNS, there are two types of clients—publishers and subscribers—also referred to as producers and consumers.

Publishers communicate asynchronously with subscribers by producing and sending a message to a topic, which is a logical access point and communication channel. Subscribers (web servers, email addresses, Amazon SQS queues, Lambda functions) consume or receive the message or notification over one of the supported protocols (Amazon SQS, HTTP/S, email, SMS, AWS Lambda) when they are subscribed to the topic.

**SNS Event for Serverless**

In the following example we create a new SNS topic with the name dispatch which is bound to the dispatcher function. The function will be called every time a message is sent to the dispatch topic.

```
functions:
  dispatcher:
    handler: dispatcher.dispatch
    events:
      - sns: dispatch
```

### SQS


![image](https://user-images.githubusercontent.com/106639884/209033230-dd91bff3-e989-43c9-b2ec-467c1d2b519b.png)


Amazon Simple Queue Service (Amazon SQS) offers a secure, durable, and available hosted queue that lets you integrate and decouple distributed software systems and components. Amazon SQS offers common constructs such as dead-letter queues and cost allocation tags. It provides a generic web services API that you can access using any programming language that the AWS SDK supports.


**SQS Event for Serverless**

In the following example, we specify that the compute function should be triggered whenever there are messages in the given SQS Queue.

The ARN for the queue can be specified as a string, the reference to the ARN of a resource by logical ID, or the import of an ARN that was exported by a different service or CloudFormation stack.


```
functions:
  compute:
    handler: handler.compute
    events:
      - sqs:
          arn: arn:aws:sqs:region:XXXXXX:myQueue
          batchSize: 10
          maximumBatchingWindow: 60
          functionResponseType: ReportBatchItemFailures
```

```
service: sqs-triggers-demo
provider:
  name: aws
  runtime: nodejs12
  profile: sls
  region: ap-southeast-1
  iamRoleStatements:
    - Effect: "Allow"
      Action:
        - "sqs:SendMessage"
        - "sqs:GetQueueUrl"
      Resource: "arn:aws:sqs:${self:provider.region}:XXXXXXXXXXXXX:MyQueue"
    - Effect: "Allow"
      Action:
        - "sqs:ListQueues"
      Resource: "arn:aws:sqs:${self:provider.region}:XXXXXXXXXXXXX:*"
functions:
  sender:
    handler: sender.handler
    events:
      - http:
          path: v1/sender
          method: post
  receiver:
    handler: receiver.handler
    events:
      - sqs:
          arn:
            Fn::GetAtt:
              - MyQueue
              - Arn
resources:
  Resources:
    MyQueue:
      Type: "AWS::SQS::Queue"
      Properties:
        QueueName: "MyQueue"
```
---

## Part 3 - AWS Xray - AWS Cloudwatch

### AWS Cloudwatch

![image](https://user-images.githubusercontent.com/106639884/209033199-6ac5ee2d-79f9-4058-ad48-7779a09c9aa5.png)


Amazon CloudWatch is a component of Amazon Web Services that provides monitoring for AWS resources and the customer applications running on the Amazon infrastructure.

CloudWatch enables real-time monitoring of AWS resources such as Amazon Elastic Compute Cloud (EC2) instances, Amazon Elastic Block Store (EBS) volumes, Elastic Load Balancing and Amazon Relational Database Service (RDS) instances. The application automatically collects and provides metrics for CPU utilization, latency and request counts. Users can also stipulate additional metrics to be monitored, such as memory usage, transaction volumes or error rates.

Users can access CloudWatch functions through an application programming interface (API), command-line tools, one of the AWS software development kits or the AWS Management Console. The CloudWatch interface provides current statistics that users can view in graph format. Users can set notification alarms to be sent when something being monitored surpasses a specified threshold. The app can also detect and shut down unused or underused EC2 instances.


```Instructor demonstrate how to use and access AWS Cloudwatch```

### AWS X-Ray

Amazon X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture. With X-Ray, you can understand how your application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors. X-Ray provides an end-to-end view of requests as they travel through your application, and shows a map of your application’s underlying components. You can use X-Ray to analyze both applications in development and in production, from simple three-tier applications to complex microservices applications consisting of thousands of services.

![image](https://user-images.githubusercontent.com/106639884/209033167-36b78219-4934-41ab-b18f-3fe5a0a988c9.png)

Users can access CloudWatch functions through an application programming interface (API), command-line tools, one of the AWS software development kits or the AWS Management Console. The CloudWatch interface provides current statistics that users can view in graph format. Users can set notification alarms to be sent when something being monitored surpasses a specified threshold. The app can also detect and shut down unused or underused EC2 instances.

## Part 4 - Recap
