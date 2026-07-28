<p align="center">
  <img src="https://img.shields.io/badge/AWS-Lambda-orange" alt="AWS Badge">
</p>


# ☁ Day 17 - AWS Lambda (Serverless Computing)

## Objective

To understand AWS Lambda, create a serverless function, and automate the stopping of an Amazon EC2 instance using Amazon EventBridge.

---

# What is AWS Lambda?

AWS Lambda is a serverless compute service that runs your code automatically in response to events without requiring you to provision or manage servers.

AWS manages:

- Infrastructure
- Scaling
- Availability
- Server maintenance

You only upload your code.

---

# Why Do We Need Lambda?

Traditional applications require:

- Launching EC2 instances
- Managing operating systems
- Installing updates
- Scaling servers

With Lambda:

- No server management
- Automatic scaling
- Pay only when code executes
- Event-driven execution

---

# Real-World Use Case

Many companies have:

- Development Servers
- Testing Servers
- QA Servers

These servers are only needed during working hours.

Instead of leaving them running 24×7, AWS Lambda can automatically stop them every evening.

Benefits:

- Reduces AWS costs
- Eliminates manual effort
- Improves automation

---

# Services Used

- AWS Lambda
- Amazon EC2
- Amazon EventBridge
- IAM Role
- Amazon CloudWatch Logs

---

# Architecture

<img width="521" height="621" alt="Lambda drawio" src="https://github.com/user-attachments/assets/4420428d-fc52-4343-b194-50fe8200ea35" />

---

# Practical Performed

## Step 1

Create an IAM Role.

Attach Policy:

AmazonEC2FullAccess

Trusted Entity:

Lambda

---

## Step 2

Create Lambda Function.

Runtime:

Python 3.x

Execution Role:

Existing IAM Role

---

## Step 3

Write Lambda Function

```python
import boto3

region = "ap-south-1"

instances = ["i-xxxxxxxxxxxxxxxxx"]

ec2 = boto3.client("ec2", region_name=region)

def lambda_handler(event, context):

    ec2.stop_instances(
        InstanceIds=instances
    )

    return {
        "statusCode":200,
        "body":"EC2 Instance Stopped Successfully"
    }
```

---

## Step 4

Deploy the Function.

---

## Step 5

Create an Amazon EventBridge Rule.

Schedule:

Every day at 8:00 PM

Target:

AWS Lambda

---

## Step 6

Start an EC2 instance manually.

Wait until the EventBridge schedule runs.

Lambda automatically stops the instance.

---

## Step 7

Verify Execution

Open:

CloudWatch Logs

Check:

START

END

REPORT

Status:

Success

---

# How the Workflow Operates

1. EventBridge triggers the Lambda function at the scheduled time.

2. Lambda starts automatically.

3. Lambda uses the boto3 SDK.

4. boto3 sends a request to Amazon EC2.

5. Amazon EC2 stops the selected instance.

6. CloudWatch stores the execution logs.

---

# Advantages

- No servers to manage
- Automatic scaling
- Pay only when code runs
- Event-driven automation
- Cost optimization

---

# Key Learnings

- Understood serverless computing.
- Created a Lambda Function.
- Used Python inside Lambda.
- Used boto3 to interact with EC2.
- Scheduled automation using EventBridge.
- Verified execution using CloudWatch Logs.

---

# Interview Questions

### What is AWS Lambda?

AWS Lambda is a serverless compute service that executes code automatically in response to events.

---

### Why is Lambda called Serverless?

Because AWS manages the servers, operating system, scaling, and infrastructure.

---

### What is boto3?

boto3 is the AWS SDK for Python used to interact with AWS services programmatically.

---

### Which AWS service can trigger Lambda on a schedule?

Amazon EventBridge.

---

### Where are Lambda logs stored?

Amazon CloudWatch Logs.

---

### Why do we need an IAM Role for Lambda?

Lambda requires permissions to access AWS services.

The IAM Role grants those permissions securely.

---

# Screenshots

- Lambda Dashboard

- IAM Role

- Lambda Code

- Deploy Success

- EventBridge Rule

- CloudWatch Logs

- EC2 Instance Before Execution

- EC2 Instance After Execution

---

# Conclusion

Successfully created an AWS Lambda function that automatically stops an EC2 instance using Amazon EventBridge. This implementation demonstrates how serverless computing can automate cloud operations, reduce infrastructure costs, and eliminate manual administrative tasks.
