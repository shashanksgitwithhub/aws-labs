<p align="center">
  <img src="https://img.shields.io/badge/AWS-VPC-purple" alt="AWS Badge">
</p>

# ☁ Day 07 - Amazon VPC (Virtual Private Cloud)

## Objective

To understand Amazon Virtual Private Cloud (VPC), its components, and how to create a custom network environment in AWS.

---

# What is Amazon VPC?

Amazon Virtual Private Cloud (VPC) is a logically isolated virtual network within AWS where you can launch and manage AWS resources securely.

A VPC allows you to control:

* IP Address Range
* Subnets
* Route Tables
* Internet Access
* Network Security

---

# Why Do We Need a VPC?

Without a VPC, all resources would exist in a shared network.

A VPC provides:

✅ Network Isolation

✅ Security

✅ Custom Networking

✅ Public and Private Networks

✅ Traffic Control

---

# Components of a VPC

## 1. VPC

A virtual network dedicated to your AWS account.

Example:

```text id="nmyf6m"
CIDR Block: 10.0.0.0/16
```

---

## 2. Subnet

A subnet is a smaller network inside a VPC.

Example:

```text id="gl75wx"
Public Subnet: 10.0.1.0/24
Private Subnet: 10.0.2.0/24
```

---

## 3. Internet Gateway (IGW)

Allows communication between resources inside the VPC and the internet.

---

## 4. Route Table

Controls where network traffic is directed.

Example:

```text id="n9sc7k"
Destination      Target
0.0.0.0/0        Internet Gateway
```

---

## 5. Route

A rule that determines how network traffic is forwarded.

---

## 6. Security Group

Acts as a virtual firewall for EC2 instances.

---

## 7. Network ACL (NACL)

Acts as a firewall at the subnet level.

---

# VPC Architecture

<img width="771" height="481" alt="Untitled Diagram drawio (1)" src="https://github.com/user-attachments/assets/8d8116f4-7966-400e-9dc4-0dd815178f0e" />

---

# Practical Performed

## Step 1: Create VPC

Navigate to:

```text id="e09ee8"
VPC → Your VPCs → Create VPC
```

Configuration:

```text id="fv8wup"
Name: My-VPC
IPv4 CIDR: 10.0.0.0/16
```

---

## Step 2: Create Public Subnet

Navigate to:

```text id="s6uxo1"
Subnets → Create Subnet
```

Configuration:

```text id="68zz3j"
Name: Public-Subnet
CIDR: 10.0.1.0/24
```

Enable:

```text id="tjlwm7"
Auto Assign Public IPv4 Address
```

---

## Step 3: Create Private Subnet

Configuration:

```text id="14zwkj"
Name: Private-Subnet
CIDR: 10.0.2.0/24
```

---

## Step 4: Create Internet Gateway

Navigate to:

```text id="0sudta"
Internet Gateways → Create Internet Gateway
```

Configuration:

```text id="g68t4o"
Name: My-IGW
```

Attach it to:

```text id="lbe9eg"
My-VPC
```

---

## Step 5: Create Route Table

Navigate to:

```text id="s6ljnr"
Route Tables → Create Route Table
```

Configuration:

```text id="ynoz0k"
Name: Public-RT
```

---

## Step 6: Add Route

```text id="gq4mpy"
Destination: 0.0.0.0/0
Target: Internet Gateway
```

---

## Step 7: Associate Route Table

Associate:

```text id="q1n0f4"
Public-Subnet
```

with

```text id="ic0aq6"
Public-RT
```

---

# Commands Used

No CLI commands were used in this practical.

Configuration was performed through the AWS Management Console.

---

# Key Learnings

✅ Created a custom VPC.

✅ Created Public and Private Subnets.

✅ Attached an Internet Gateway.

✅ Configured Route Tables.

✅ Understood AWS networking fundamentals.

---

# Interview Questions

### What is Amazon VPC?

Amazon VPC is a logically isolated virtual network in AWS.

---

### What is a Subnet?

A subnet is a smaller network inside a VPC.

---

### What is an Internet Gateway?

An Internet Gateway allows communication between the VPC and the internet.

---

### Difference between Public and Private Subnet?

| Public Subnet         | Private Subnet            |
| --------------------- | ------------------------- |
| Has Internet Access   | No Direct Internet Access |
| Uses Internet Gateway | Uses NAT Gateway          |

---

### What is CIDR?

CIDR (Classless Inter-Domain Routing) defines the IP address range of a network.

Example:

```text id="rfp91h"
10.0.0.0/16
```

---

### What is a Route Table?

A Route Table contains rules that determine where network traffic is directed.

---

# Screenshots

* VPC Dashboard<img width="1906" height="1008" alt="Screenshot 2026-07-06 194857" src="https://github.com/user-attachments/assets/65944f14-db27-48f1-ae74-3fbff7e1d020" />

* VPC Creation<img width="1907" height="1009" alt="Screenshot 2026-07-06 194935" src="https://github.com/user-attachments/assets/be2a9b78-803e-4f0f-88ec-a871cca93831" /><img width="1907" height="1007" alt="Screenshot 2026-07-06 195002" src="https://github.com/user-attachments/assets/e8569d96-f941-41b5-8ced-37d0d27359b2" />

* Public Subnet Creation<img width="1906" height="1009" alt="Screenshot 2026-07-06 195054" src="https://github.com/user-attachments/assets/56a23445-27cc-4e1a-9aa9-2a23cf0e5142" /><img width="1906" height="1010" alt="Screenshot 2026-07-06 195123" src="https://github.com/user-attachments/assets/dc99e013-73a9-462b-8c29-e644221f7743" />

* Private Subnet Creation<img width="1907" height="1008" alt="Screenshot 2026-07-06 195150" src="https://github.com/user-attachments/assets/24f67027-d757-4d4b-9499-1a543bc4f084" />

* Internet Gateway<img width="1907" height="1011" alt="Screenshot 2026-07-06 195301" src="https://github.com/user-attachments/assets/e8251dda-955d-499a-84d0-4275ec7bf282" />

* Route Table<img width="1907" height="1011" alt="Screenshot 2026-07-06 195437" src="https://github.com/user-attachments/assets/da70f210-6f0c-4cdd-8cd9-c7b98f43247f" />

* Route Association<img width="1907" height="1010" alt="Screenshot 2026-07-06 195541" src="https://github.com/user-attachments/assets/f7d718f5-88cb-480a-996d-83293b70c756" />

---

# Conclusion

Successfully created a custom Virtual Private Cloud (VPC) with Public and Private Subnets, configured Internet access using an Internet Gateway, and learned the core networking concepts required for designing secure AWS infrastructures.
