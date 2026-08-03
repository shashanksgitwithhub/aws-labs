<p align="center">
  <img src="https://img.shields.io/badge/AWS-Cloud watch-c71585" alt="AWS Badge">
</p>


# ☁ Day 19 - Amazon CloudWatch Monitoring with Amazon SNS Email Notifications

# Overview

On Day-19, I learned how to monitor Amazon EC2 instances using **Amazon CloudWatch** and configured **CloudWatch Alarms** to send email notifications through **Amazon Simple Notification Service (SNS)** whenever the EC2 instance CPU utilization crossed a predefined threshold.

This project demonstrates how AWS services work together to provide real-time monitoring and alerting for cloud infrastructure.

---

# Architecture

<img width="402" height="920" alt="CW drawio" src="https://github.com/user-attachments/assets/a746cc16-fc61-4360-a1b8-84a5a96a3b18" />

---

# AWS Services Used

- Amazon EC2
- Amazon CloudWatch
- Amazon CloudWatch Alarms
- Amazon Simple Notification Service (SNS)
- IAM

---

# Project Objective

To automatically monitor the CPU utilization of an EC2 instance and notify the administrator through email whenever CPU utilization reaches or exceeds **50%**.

---

# What is Amazon CloudWatch?

Amazon CloudWatch is a monitoring and observability service that collects metrics, logs, and events from AWS resources.

It helps administrators:

- Monitor resource health
- Detect performance issues
- Create alarms
- Trigger automated actions
- Analyze application logs

---

# What is Amazon SNS?

Amazon Simple Notification Service (SNS) is a fully managed messaging service used to send notifications to subscribers.

SNS supports:

- Email
- SMS
- HTTP/HTTPS
- AWS Lambda
- Amazon SQS

In this project, SNS was used to send **email alerts** whenever the CloudWatch alarm entered the **ALARM** state.

---

# Services Workflow

<img width="402" height="850" alt="SNS drawio" src="https://github.com/user-attachments/assets/f7816033-bfa0-418f-9126-7e3dbeb24680" />

---

# Hands-on Implementation

## Step 1 - Create SNS Topic

- Open Amazon SNS
- Create a Standard Topic
- Topic Name:
```
EC2-CPU-Alerts
```

---

## Step 2 - Create Subscription

Protocol

```
Email
```

Endpoint

```
your-email@example.com
```

Confirm the subscription from the email received.

---

## Step 3 - Launch EC2 Instance

Launch an Amazon EC2 instance that will be monitored by CloudWatch.

---

## Step 4 - Create CloudWatch Alarm

Navigate to:

```
CloudWatch

↓

Alarms

↓

Create Alarm
```

Choose Metric:

```
EC2

↓

Per-Instance Metrics

↓

CPUUtilization
```

---

## Step 5 - Configure Threshold

Statistic

```
Average
```

Threshold Type

```
Static
```

Condition

```
Greater than or Equal to
```

Threshold Value

```
50%
```

---

## Step 6 - Configure Notification

Whenever Alarm State becomes

```
ALARM
```

Send notification to

```
EC2-CPU-Alerts
```

SNS Topic.

---

## Step 7 - Review and Create Alarm

CloudWatch continuously monitors the EC2 instance.

Whenever CPU utilization reaches **50% or above**, CloudWatch automatically sends a notification to Amazon SNS.

SNS then delivers the notification to the configured email address.

---

# Alarm States

CloudWatch Alarm can have three states.

## OK

```
CPU Utilization < 50%
```

Everything is operating normally.

---

## ALARM

```
CPU Utilization ≥ 50%
```

Threshold exceeded.

SNS sends notification.

---

## INSUFFICIENT DATA

CloudWatch does not have enough metric data to determine the current state.

---

# CloudWatch Metrics Used

Metric

```
CPUUtilization
```

Namespace

```
AWS/EC2
```

Statistic

```
Average
```

Threshold

```
50%
```

Comparison

```
GreaterThanOrEqualToThreshold
```

---

# Notification Flow

```
CPU = 30%

↓

CloudWatch

↓

OK
```

```
CPU = 54%

↓

CloudWatch

↓

ALARM

↓

SNS

↓

Email Sent
```

```
CPU = 18%

↓

CloudWatch

↓

Back to OK
```

---

# Real World Use Cases

- CPU Monitoring
- Memory Monitoring (CloudWatch Agent)
- Disk Utilization Alerts
- Production Server Monitoring
- Application Health Monitoring
- Infrastructure Monitoring
- Security Monitoring

---

# Interview Questions

### What is Amazon CloudWatch?

Amazon CloudWatch is a monitoring and observability service that collects metrics, logs, and events from AWS resources.

---

### What is Amazon SNS?

Amazon SNS is a managed messaging service used to deliver notifications to subscribers.

---

### Why is SNS used with CloudWatch?

CloudWatch detects events and alarms, while SNS delivers notifications such as emails or SMS messages.

---

### What is a CloudWatch Alarm?

A CloudWatch Alarm continuously evaluates a CloudWatch metric against a predefined threshold and changes state when the threshold is crossed.

---

### Which metric was monitored?

```
CPUUtilization
```

---

### What threshold was configured?

```
CPU Utilization ≥ 50%
```

---

### What happens when the threshold is crossed?

```
CloudWatch Alarm

↓

Alarm State = ALARM

↓

SNS Topic

↓

Email Notification
```

---

# Key Learnings

- Amazon CloudWatch Fundamentals
- CloudWatch Metrics
- CloudWatch Alarms
- Threshold Monitoring
- Amazon SNS
- Email Notifications
- EC2 Monitoring
- Infrastructure Monitoring
- Event-Driven Alerting
- AWS Monitoring Architecture

---

# Screenshots

- SNS Dashboard<img width="1919" height="1020" alt="Screenshot 2026-08-03 113409" src="https://github.com/user-attachments/assets/8d1973a8-d79d-4607-ba47-f8d893a19b90" />

- Create Topic<img width="1919" height="1017" alt="Screenshot 2026-08-03 113617" src="https://github.com/user-attachments/assets/bd4b60f8-eb62-4973-8330-bc6febc7df7b" />
  <img width="1919" height="1017" alt="Screenshot 2026-08-03 113629" src="https://github.com/user-attachments/assets/813942fd-e1b5-400c-bef6-4c42378a027d" />

- SNS Subscription Create and Confirmation<img width="1919" height="1018" alt="Screenshot 2026-08-03 113749" src="https://github.com/user-attachments/assets/548c20f1-e7f2-4545-8965-efca5d9ff5fc" />
  <img width="1919" height="1017" alt="Screenshot 2026-08-03 113756" src="https://github.com/user-attachments/assets/71aa6e58-de52-4ba9-85ec-4f581ac94848" />
  <img width="1918" height="1019" alt="Screenshot 2026-08-03 113822" src="https://github.com/user-attachments/assets/cbe2d7ae-56e5-414f-9621-b2e40ce5e77d" />
  <img width="1914" height="1014" alt="Screenshot 2026-08-03 113828" src="https://github.com/user-attachments/assets/55e07320-9c2d-4cbd-a5de-c8db3bd4a4bf" />
  <img width="1897" height="1004" alt="Screenshot 2026-08-03 113847" src="https://github.com/user-attachments/assets/5f92bbb4-3dd4-4190-adc5-b2c73ab2ac19" />

- EC2 Instance<img width="1919" height="1018" alt="image" src="https://github.com/user-attachments/assets/dd4bb3af-5839-462c-8d31-6bdc9e3ea928" />

- CloudWatch Alarm Configuration<img width="1919" height="1018" alt="Screenshot 2026-08-03 114334" src="https://github.com/user-attachments/assets/b6aea1f5-37ef-4422-b439-0749e701705a" />
  <img width="1914" height="1009" alt="Screenshot 2026-08-03 114340" src="https://github.com/user-attachments/assets/74c30841-bd5b-4958-822e-7e320de3f826" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-03 114404" src="https://github.com/user-attachments/assets/69456289-e750-42d0-9c0e-3dad6f2f0872" />
  <img width="1913" height="1018" alt="Screenshot 2026-08-03 114520" src="https://github.com/user-attachments/assets/26cfd22c-18d4-4034-b60d-81554d1faa3c" />
  <img width="1919" height="1020" alt="Screenshot 2026-08-03 114525" src="https://github.com/user-attachments/assets/80d2d997-876d-4bdc-815c-0a4f5f4ebeb9" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-03 114549" src="https://github.com/user-attachments/assets/18729ace-fdc0-4314-8cc3-1266a905807a" />
  <img width="1917" height="1020" alt="Screenshot 2026-08-03 114613" src="https://github.com/user-attachments/assets/cbb9f609-6cba-4318-8f90-b2e23207cc62" />
  <img width="1919" height="1018" alt="Screenshot 2026-08-03 114624" src="https://github.com/user-attachments/assets/2b054407-cf4a-4840-8473-5b7189d8e5d3" />

- Connect to Instance<img width="1919" height="1019" alt="Screenshot 2026-08-03 115946" src="https://github.com/user-attachments/assets/d5eb2397-5f43-4094-8a34-2a2167728e8b" />
  <img width="1919" height="1018" alt="Screenshot 2026-08-03 120125" src="https://github.com/user-attachments/assets/fc4d45ce-48a6-4bda-a2eb-5494d7e3facb" />
  <img width="1919" height="1018" alt="Screenshot 2026-08-03 120132" src="https://github.com/user-attachments/assets/d4378dca-64da-46f8-bd4c-c81e55197db9" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-03 120731" src="https://github.com/user-attachments/assets/5918dd3e-b932-4941-9262-3e9bde326ada" />

- CloudWatch Alarm State<img width="1918" height="1017" alt="Screenshot 2026-08-03 121642" src="https://github.com/user-attachments/assets/844bb05f-3407-4b4b-adf6-cc6942cf0c9d" />

- Email Notification<img width="1919" height="1020" alt="Screenshot 2026-08-03 121729" src="https://github.com/user-attachments/assets/71c25358-dcfa-4b69-98eb-a08403a618bb" />

- CloudWatch Alarm State<img width="1919" height="1020" alt="Screenshot 2026-08-03 121804" src="https://github.com/user-attachments/assets/ca2dad44-7fc8-4c22-beee-68fbf5818f2c" />

- CloudWatch Metrics Graph<img width="1919" height="804" alt="image" src="https://github.com/user-attachments/assets/8b129b87-3afb-406d-b513-1910089244e7" />

- CloudWatch Alarm History<img width="1919" height="1018" alt="Screenshot 2026-08-03 121857" src="https://github.com/user-attachments/assets/25db849a-6bd6-4a9b-a011-4c944d111ea1" />

---

# Conclusion

In this project, I implemented an automated monitoring and alerting solution using Amazon CloudWatch and Amazon SNS.

CloudWatch continuously monitored the CPU utilization of an EC2 instance. Whenever CPU utilization reached or exceeded the configured threshold of **50%**, CloudWatch changed the alarm state to **ALARM** and published a notification to an Amazon SNS topic. SNS then delivered the alert to the configured email endpoint.

This project demonstrates how AWS monitoring and notification services can be integrated to proactively detect infrastructure issues and notify administrators in real time.
