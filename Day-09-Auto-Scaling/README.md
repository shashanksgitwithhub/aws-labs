<p align="center">
  <img src="https://img.shields.io/badge/AWS-Auto Scaling-orange" alt="AWS Badge">
</p>

# ☁ Day 09 - Amazon EC2 Auto Scaling

## Objective

To understand Amazon EC2 Auto Scaling and learn how to automatically launch or terminate EC2 instances based on application demand.

---

# What is Auto Scaling?

Amazon EC2 Auto Scaling is an AWS service that automatically adjusts the number of EC2 instances based on traffic, demand, or predefined policies.

It helps maintain application availability while reducing infrastructure costs.

---

# Why Do We Need Auto Scaling?

Without Auto Scaling:

* A single EC2 instance may become overloaded during high traffic.
* Resources remain underutilized during low traffic.
* Manual scaling takes time and may lead to downtime.

With Auto Scaling:

* Automatically launches new EC2 instances when demand increases.
* Automatically terminates unnecessary instances when demand decreases.
* Improves application availability.
* Optimizes infrastructure costs.

---

# Components of Auto Scaling

## 1. Launch Template

A Launch Template stores the configuration required to launch EC2 instances.

It includes:

* Amazon Machine Image (AMI)
* Instance Type
* Key Pair
* Security Group
* User Data Script
* Storage Configuration

---

## 2. Auto Scaling Group (ASG)

An Auto Scaling Group manages a collection of EC2 instances.

It ensures that the desired number of healthy instances is always running.

---

## 3. Scaling Policies

Scaling Policies define when Auto Scaling should add or remove EC2 instances.

Examples:

* CPU Utilization
* Network Traffic
* Memory Usage (via CloudWatch Agent)

---

## 4. CloudWatch Alarms

CloudWatch continuously monitors metrics such as CPU utilization.

When a threshold is crossed, it triggers scaling actions.

---

# Auto Scaling Architecture

<img width="772" height="692" alt="Auto_scaling drawio (1)" src="https://github.com/user-attachments/assets/08e93c80-1eef-4d98-9e78-1d20bfddfc2c" />

---

# Practical Performed

## Step 1: Create a Launch Template

Navigate to:

EC2 → Launch Templates

Configuration:

* Ubuntu Server AMI
* t3.micro Instance
* Existing Key Pair
* Existing Security Group
* User Data Script

---

## Step 2: Create an Auto Scaling Group

Navigate to:

EC2 → Auto Scaling Groups

Click:

Create Auto Scaling Group

Select the Launch Template.

---

## Step 3: Configure Networking

Select:

* Test_VPC
* Public Subnets

---

## Step 4: Attach Load Balancer

Choose:

* Attach to an Existing Load Balancer

Select:

* Test-LB

Select the Target Group created Test-EC2-SG.

---

## Step 5: Configure Group Size

Example:

Minimum Capacity:

1

Desired Capacity:

2

Maximum Capacity:

3

---

## Step 6: Configure Scaling Policy

Example:

Target Tracking Policy

Metric:

Average CPU Utilization

Target Value:

50%

This means:

* Launch a new EC2 instance when CPU utilization exceeds approximately 50%.
* Terminate unnecessary instances when utilization decreases.

---

## Step 7: Review and Create

Verify all configurations and create the Auto Scaling Group.

---

# Practical Outcome

✅ Created a Launch Template.

✅ Created an Auto Scaling Group.

✅ Attached the Auto Scaling Group to an Application Load Balancer.

✅ Configured scaling policies.

✅ Learned how AWS automatically manages EC2 instances based on demand.

---

# Advantages of Auto Scaling

* High Availability
* Automatic Scaling
* Fault Tolerance
* Cost Optimization
* Improved Performance
* Reduced Manual Intervention

---

# Key Learnings

* Understood the purpose of Auto Scaling.
* Learned the role of Launch Templates.
* Created an Auto Scaling Group.
* Configured scaling policies.
* Integrated Auto Scaling with an Application Load Balancer.

---

# Interview Questions

### What is Amazon EC2 Auto Scaling?

Amazon EC2 Auto Scaling automatically adjusts the number of EC2 instances based on application demand.

---

### What is a Launch Template?

A Launch Template contains the configuration required to launch EC2 instances.

---

### What is an Auto Scaling Group?

An Auto Scaling Group manages a collection of EC2 instances and maintains the desired number of healthy instances.

---

### What is the difference between Desired, Minimum, and Maximum Capacity?

Minimum Capacity:
The minimum number of EC2 instances that must always remain running.

Desired Capacity:
The preferred number of running EC2 instances.

Maximum Capacity:
The maximum number of EC2 instances that Auto Scaling can launch.

---

### Which AWS service triggers Auto Scaling?

Amazon CloudWatch.

---

### Can Auto Scaling work without a Load Balancer?

Yes. However, it is commonly used with an Application Load Balancer to distribute traffic across automatically managed instances.

---

# Screenshots

* Launch Template Creation<img width="1907" height="1008" alt="Screenshot 2026-07-10 100902" src="https://github.com/user-attachments/assets/b83f9ace-4ac3-48c9-901f-03b4d1f75a6c" />

* Launch Template Details<img width="1907" height="1011" alt="Screenshot 2026-07-10 100937" src="https://github.com/user-attachments/assets/015dab0a-587f-49cb-b7c2-fd87226298a4" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-10 101002" src="https://github.com/user-attachments/assets/b8696871-2f81-41fe-b873-897db33d57b0" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-10 101243" src="https://github.com/user-attachments/assets/88961d62-bff2-4283-828d-de70f2c3ede4" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-10 101330" src="https://github.com/user-attachments/assets/706099e0-96d3-401e-a2dd-09cdbfbcc1b5" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-10 101344" src="https://github.com/user-attachments/assets/e93623b0-80b5-4008-a2bc-ebe039480877" />
  <img width="1907" height="1011" alt="Screenshot 2026-07-10 101415" src="https://github.com/user-attachments/assets/b47eba4b-d850-4814-9d14-eed22ce1ffdd" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-10 101437" src="https://github.com/user-attachments/assets/f4079652-09b1-416c-aca3-916483308f2f" />

* Auto Scaling Group Creation<img width="1907" height="1015" alt="Screenshot 2026-07-10 101459" src="https://github.com/user-attachments/assets/202741d9-8d6c-4453-8f8f-a52a3c73cb64" />

* Auto Scaling Group Configuration<img width="1907" height="1007" alt="Screenshot 2026-07-10 101525" src="https://github.com/user-attachments/assets/dce9f6b2-4eb2-41eb-9eed-63edc79bd22d" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-10 101555" src="https://github.com/user-attachments/assets/0c24bf65-bb19-482c-a9a8-f9316819f2a7" />
  <img width="1907" height="1011" alt="Screenshot 2026-07-10 101636" src="https://github.com/user-attachments/assets/f6ac2f58-0bd9-4434-80a3-5f2b8aa7dfbe" />

* Attached Application Load Balancer<img width="1907" height="1010" alt="Screenshot 2026-07-10 101616" src="https://github.com/user-attachments/assets/777333e0-42d0-426f-832c-2e06066b0d7b"
                                      />
* Scaling Policy<img width="1907" height="1010" alt="Screenshot 2026-07-10 101651" src="https://github.com/user-attachments/assets/7ed53c74-132e-40b8-b9d5-339fdb13fe8e" />

* Target Group Association and creation<img width="1907" height="1004" alt="Screenshot 2026-07-10 101754" src="https://github.com/user-attachments/assets/e565b7cb-0366-43c0-a8c4-ac39af7b6d2a" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-10 101818" src="https://github.com/user-attachments/assets/f018378b-6ca7-41a7-b9bd-bdd2313e9802" />
  <img width="1907" height="1012" alt="Screenshot 2026-07-10 101839" src="https://github.com/user-attachments/assets/f28bde94-8d6e-4850-a5d1-04f648982793" />

* Copy DNS name<img width="1907" height="1007" alt="Screenshot 2026-07-10 102027" src="https://github.com/user-attachments/assets/3f8e3453-f61d-441f-976d-272636a699ff" />

* Output<img width="1907" height="1013" alt="Screenshot 2026-07-10 102104" src="https://github.com/user-attachments/assets/704db521-bcc2-4eba-9a37-29d1ae59e20d" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-10 102122" src="https://github.com/user-attachments/assets/8afe4544-ee64-4a85-a3fc-9b06a1f93dd0" />

* Healthly and two Running EC2 Instances<img width="1907" height="1009" alt="Screenshot 2026-07-10 105029" src="https://github.com/user-attachments/assets/d4563826-5157-4834-ab75-95ca12721171" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-10 105654" src="https://github.com/user-attachments/assets/9b5f21e3-70b3-465f-b06c-108518525e26" />

---

# Conclusion

Successfully created a Launch Template and an Auto Scaling Group, configured automatic scaling policies, and integrated the Auto Scaling Group with an Application Load Balancer. This implementation enables applications to automatically handle changing workloads while maintaining high availability and optimizing infrastructure costs.
