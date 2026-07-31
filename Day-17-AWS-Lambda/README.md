<p align="center">
  <img src="https://img.shields.io/badge/AWS-Lambda-orange" alt="AWS Badge">
</p>


# Day-17: AWS Lambda with Amazon EventBridge Scheduler

## Overview

On Day-17, I learned how to build a serverless automation using **AWS Lambda**, **Amazon EventBridge Scheduler**, **IAM Roles**, **Amazon EC2**, **CloudWatch**, and **Python (boto3)**.

Instead of manually stopping and starting an EC2 instance, I created an automated workflow that performs these tasks based on a predefined schedule.

This project demonstrates how multiple AWS services work together to automate cloud infrastructure without managing servers.

---

# Architecture

<img width="402" height="762" alt="LAmbdoo drawio" src="https://github.com/user-attachments/assets/b59c18c3-1f0f-429f-a88a-381ef528c022" />

---

# AWS Services Used

- AWS Lambda
- Amazon EventBridge Scheduler
- Amazon EC2
- AWS Identity and Access Management (IAM)
- Amazon CloudWatch
- Python
- boto3 (AWS SDK for Python)

---

# What is AWS Lambda?

AWS Lambda is a serverless compute service that allows developers to run code without provisioning or managing servers.

AWS automatically:

- Creates the execution environment
- Runs the code
- Scales automatically
- Manages the infrastructure
- Stops the execution environment after completion

---

# Why Serverless?

In traditional applications, developers are responsible for:

- Creating servers
- Installing operating systems
- Configuring software
- Scaling infrastructure
- Managing availability

With AWS Lambda, AWS manages all of these tasks automatically.

Developers only need to write the business logic.

---

# Real World Use Cases of AWS Lambda

- Automatically resize uploaded images
- Backup databases
- Process uploaded files
- Send email notifications
- Start and stop EC2 instances automatically
- Log monitoring
- Scheduled infrastructure automation

---

# What is EventBridge Scheduler?

Amazon EventBridge Scheduler is a fully managed scheduling service used to invoke AWS services based on time.

It allows automation using:

- One-time schedules
- Recurring schedules
- Cron expressions
- Rate expressions

---

# Difference Between Rate and Cron

## Rate Expression

Runs at a fixed interval.

Examples:

- Every 5 minutes
- Every 1 hour
- Every 2 days

Example:

```
rate(1 hour)
```

---

## Cron Expression

Runs at a specific date and time.

Example:

```
cron(0 20 * * ? *)
```

Meaning:

- Minute = 0
- Hour = 20 (8 PM)
- Every Day
- Every Month
- Every Year

---

# Project Workflow

```
08:00 PM

↓

Amazon EventBridge Scheduler

↓

Invokes AWS Lambda

↓

Lambda executes Python code

↓

boto3 communicates with EC2 API

↓

EC2 Instance Stops

↓

CloudWatch Logs Generated
```

---

# Components Used

## 1. IAM Role for Lambda

Execution Role attached to Lambda.

Purpose:

- Authenticate Lambda
- Authorize access to EC2
- Provide temporary AWS credentials

Policy Used:

```
AmazonEC2FullAccess
```

---

## 2. IAM Role for EventBridge Scheduler

Execution Role created automatically by AWS.

Purpose:

- Allow EventBridge Scheduler to invoke Lambda

This role is different from the Lambda Execution Role.

---

# Python Code Used

## Stop EC2 Instance

```python
import boto3

region = "ap-south-2"

instances = [
    "YOUR_INSTANCE_ID"
]

ec2 = boto3.client("ec2", region_name=region)

def lambda_handler(event, context):

    response = ec2.stop_instances(
        InstanceIds=instances
    )

    return {
        "statusCode": 200,
        "body": "EC2 Instance Stop Request Sent Successfully"
    }
```

---

## Start EC2 Instance

```python
import boto3

region = "ap-south-2"

instances = [
    "YOUR_INSTANCE_ID"
]

ec2 = boto3.client("ec2", region_name=region)

def lambda_handler(event, context):

    response = ec2.start_instances(
        InstanceIds=instances
    )

    return {
        "statusCode": 200,
        "body": "EC2 Instance Start Request Sent Successfully"
    }
```

---

# Understanding boto3

boto3 is the official AWS SDK for Python.

It allows Python applications to communicate with AWS services.

Example:

```python
ec2 = boto3.client("ec2")
```

This creates a client for the Amazon EC2 service.

---

# How Lambda Authenticates Without AWS Access Keys

AWS automatically provides temporary credentials to the Lambda execution environment through the attached IAM Execution Role.

When boto3 is initialized, it automatically discovers these credentials.

No Access Key or Secret Key needs to be written in the code.

---

# EventBridge Scheduler Configuration

## Stop EC2 Scheduler

Schedule Name

```
StopEC2EveryNight
```

Cron Expression

```
cron(0 20 * * ? *)
```

Meaning

Every day at 08:00 PM

Target

```
StopEC2Instance
```

Payload

```json
{}
```

---

## Start EC2 Scheduler

Schedule Name

```
StartEC2EveryMorning
```

Cron Expression

```
cron(45 8 * * ? *)
```

Meaning

Every day at 08:45 AM

Target

```
StartEC2Instance
```

Payload

```json
{}
```

---

# Complete Automation Flow

```
08:45 AM

↓

EventBridge Scheduler

↓

StartEC2Instance Lambda

↓

Amazon EC2 Running

↓

Developers Use Instance

↓

08:00 PM

↓

EventBridge Scheduler

↓

StopEC2Instance Lambda

↓

Amazon EC2 Stopped
```

---

# CloudWatch

Every Lambda execution automatically generates logs in CloudWatch.

These logs help in:

- Debugging
- Monitoring
- Error tracking
- Performance analysis

---

# Screenshots

- AWS Lambda Dashboard
  <img width="1907" height="1014" alt="Screenshot 2026-07-29 193203" src="https://github.com/user-attachments/assets/41978f9c-d8ab-427f-9180-7c3a3d8a2dbf" />
 
- Lambda Function Creation Start and Stop
  <img width="1907" height="1012" alt="Screenshot 2026-07-29 225149" src="https://github.com/user-attachments/assets/27a9d7b1-0e42-48a8-983c-130e43c56d4d" />
  <img width="1907" height="1008" alt="Screenshot 2026-07-29 225205" src="https://github.com/user-attachments/assets/9d3d93a8-47cf-4ef1-bf65-9a872b435d62" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-29 225238" src="https://github.com/user-attachments/assets/ede413ed-98ce-405d-a84e-d450a1ad9d8d" />
  <img width="1905" height="1011" alt="Screenshot 2026-07-29 193347" src="https://github.com/user-attachments/assets/01522efe-7a6f-48e2-9ebb-dd9f8fb15589" />
  <img width="1907" height="1012" alt="Screenshot 2026-07-29 193642" src="https://github.com/user-attachments/assets/7ef5128f-36ea-4c3f-adba-3eb0f5e526a6" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-29 193748" src="https://github.com/user-attachments/assets/7bf238bf-a8eb-45dc-8b89-35c78c9c9748" />

- IAM Role Creation
  <img width="1907" height="1012" alt="Screenshot 2026-07-29 192449" src="https://github.com/user-attachments/assets/ffafb73e-21d6-4138-8ca6-cfc546fd94bf" />
  <img width="1907" height="1008" alt="Screenshot 2026-07-29 192507" src="https://github.com/user-attachments/assets/ed35565f-3016-4f6e-a8e4-b8e39181fb8c" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-29 192801" src="https://github.com/user-attachments/assets/94a09053-2f89-4f35-ae70-8fce4eedc954" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-29 192809" src="https://github.com/user-attachments/assets/32aa0fa2-55ac-410a-a8a0-5ea6869000c0" />
  <img width="1907" height="1013" alt="Screenshot 2026-07-29 192833" src="https://github.com/user-attachments/assets/1f2bd1a3-d783-4c0e-9873-6a3577e0c974" />

- Lambda Code for Start and Stop
  <img width="1907" height="1011" alt="Screenshot 2026-07-29 231309" src="https://github.com/user-attachments/assets/fd6a8a00-2fb7-44d1-aca3-4f4a3ce215b8" />
  <img width="1907" height="1012" alt="Screenshot 2026-07-29 195804" src="https://github.com/user-attachments/assets/ebaf8023-e13c-486e-b96d-655cb413d348" />

- Successful Test Results for Start and Stop
  <img width="1906" height="1009" alt="Screenshot 2026-07-29 231415" src="https://github.com/user-attachments/assets/8e7bb96a-3238-4601-ac6d-d3b7b7a1b7f3" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-29 231433" src="https://github.com/user-attachments/assets/3993fdea-9828-4c2a-bf0f-5cc55bb6bf05" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-29 200103" src="https://github.com/user-attachments/assets/3a8ab430-2620-4552-abcb-0073d7d58891" />
  <img width="1907" height="1011" alt="Screenshot 2026-07-29 200258" src="https://github.com/user-attachments/assets/17fe4986-80e5-485b-bac0-9523bab55dc3" />

- EC2 Running State
  <img width="1905" height="1013" alt="Screenshot 2026-07-29 231450" src="https://github.com/user-attachments/assets/a970ad5e-2ede-4f70-8765-e0d67ac4f18f" />

- EC2 Stopped State
  <img width="1907" height="1010" alt="Screenshot 2026-07-29 200323" src="https://github.com/user-attachments/assets/0a3b7556-24ea-4979-8ab6-ee85e9c66fbb" />

- Amazon EventBridge Dashboard
  <img width="1907" height="996" alt="Screenshot 2026-07-29 202812" src="https://github.com/user-attachments/assets/7427df66-1ec9-47d8-9797-b7b480d7879a" />

- EventBridge Scheduler (Stop)
  <img width="1907" height="1013" alt="Screenshot 2026-07-29 204008" src="https://github.com/user-attachments/assets/3e57aea0-ed70-4deb-9aca-ec26c62c3eb9" />
  <img width="1907" height="1011" alt="Screenshot 2026-07-29 205058" src="https://github.com/user-attachments/assets/4e5cfd0e-9421-4258-9441-0139997dfd63" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-29 205115" src="https://github.com/user-attachments/assets/f748a3eb-8d3d-40ee-8434-1281a42c578d" />
  <img width="1903" height="1004" alt="Screenshot 2026-07-29 205127" src="https://github.com/user-attachments/assets/444f5ebf-c368-467a-9e1c-e9af0486d37f" />
  <img width="1907" height="1008" alt="Screenshot 2026-07-29 213053" src="https://github.com/user-attachments/assets/aa8b9852-9bc4-482c-a290-415a06d1611c" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-29 214233" src="https://github.com/user-attachments/assets/aab79fec-4944-4f42-9543-98e239d3874d" />
  <img width="1907" height="1013" alt="Screenshot 2026-07-29 215929" src="https://github.com/user-attachments/assets/047dfe29-9b98-44d8-8861-359fdac72961" />
  <img width="1904" height="1002" alt="Screenshot 2026-07-29 215942" src="https://github.com/user-attachments/assets/3053eded-9cce-42e7-9e09-c7803ca8136f" />
  <img width="1907" height="1003" alt="Screenshot 2026-07-29 220650" src="https://github.com/user-attachments/assets/9c676630-18a7-4dee-a390-291c5cafa42b" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-29 220717" src="https://github.com/user-attachments/assets/04162fdb-fb9e-4678-834a-327138d035a6" />
  <img width="1907" height="1008" alt="Screenshot 2026-07-29 220944" src="https://github.com/user-attachments/assets/c36f6ad8-6914-497a-b257-9441bd3f2dd8" />

- EventBridge Scheduler (Start)
  <img width="1907" height="1008" alt="Screenshot 2026-07-29 231647" src="https://github.com/user-attachments/assets/112461f0-889f-4182-ba0e-4721a1932770" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-29 231655" src="https://github.com/user-attachments/assets/2c6f6536-7f2e-4ee1-8906-f8ee4e163316" />
  <img width="1907" height="1011" alt="Screenshot 2026-07-29 231707" src="https://github.com/user-attachments/assets/cf795ca7-bec1-4fdc-a1be-f3bb1c857e87" />
  <img width="1904" height="1008" alt="Screenshot 2026-07-29 231758" src="https://github.com/user-attachments/assets/b5288ec5-ae82-4faf-865c-e4cbf7ece2a7" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-29 231806" src="https://github.com/user-attachments/assets/342ad89c-bbe2-45df-8dfb-a16b0c8b2e4d" />
  <img width="1907" height="1008" alt="Screenshot 2026-07-29 231832" src="https://github.com/user-attachments/assets/36ea2863-a1a9-4922-bc3d-b24e24d17875" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-29 231842" src="https://github.com/user-attachments/assets/5841c6d9-a266-404f-83f6-0fe8aec00799" />
  <img width="1907" height="1012" alt="Screenshot 2026-07-29 231855" src="https://github.com/user-attachments/assets/9fafcb48-84dd-4cf6-a8e7-b939ae46cd69" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-29 231903" src="https://github.com/user-attachments/assets/83e7f7e9-b334-4ba6-9345-2154b4f48a84" />
  <img width="1917" height="1018" alt="image" src="https://github.com/user-attachments/assets/c5bf3bf9-8c5a-45e8-99b6-1ec994055d38" />

- CloudWatch Logs
  
  Start<img width="1903" height="1010" alt="Screenshot 2026-07-30 112329" src="https://github.com/user-attachments/assets/420d7e3d-c7a3-483c-89cb-8aafabb2c86c" />
  Stop<img width="1917" height="1018" alt="Screenshot 2026-07-31 110532" src="https://github.com/user-attachments/assets/ed4d8a34-f132-4b6c-825b-5406bb27e1a5" />

---

# Interview Questions

### What is AWS Lambda?

A serverless compute service that executes code in response to events without managing servers.

---

### Why is Lambda called serverless?

AWS manages the infrastructure, scaling, operating system, and execution environment.

---

### What is EventBridge Scheduler?

A managed AWS service that invokes AWS resources based on a predefined schedule.

---

### What is boto3?

The official AWS SDK for Python used to interact with AWS services.

---

### Why are two IAM Roles used in this project?

1. Lambda Execution Role
   - Allows Lambda to access EC2.

2. EventBridge Scheduler Execution Role
   - Allows Scheduler to invoke Lambda.

---

### Does EventBridge directly stop EC2?

No.

EventBridge invokes Lambda.

Lambda communicates with EC2 using boto3.

---

### How does Lambda authenticate without Access Keys?

AWS automatically injects temporary credentials into the Lambda execution environment using the attached IAM Execution Role.

---

### What is the difference between Rate and Cron expressions?

Rate:

Runs after fixed intervals.

Example:

```
rate(1 hour)
```

Cron:

Runs at a specific time.

Example:

```
cron(0 20 * * ? *)
```

---

# Key Learnings

- AWS Lambda Fundamentals
- Serverless Computing
- Event-Driven Architecture
- EventBridge Scheduler
- Cron Expressions
- Rate Expressions
- IAM Execution Roles
- Temporary AWS Credentials
- boto3 SDK
- EC2 Automation
- CloudWatch Logging
- Infrastructure Automation
- Production Workflow Design

---

# Conclusion

This project demonstrates a complete serverless automation workflow using AWS Lambda and Amazon EventBridge Scheduler.

By integrating Lambda, EventBridge Scheduler, IAM, EC2, CloudWatch, and Python, repetitive infrastructure tasks such as starting and stopping EC2 instances can be automated efficiently without manual intervention.

This implementation follows cloud automation best practices and provides hands-on experience with event-driven architecture in AWS.
