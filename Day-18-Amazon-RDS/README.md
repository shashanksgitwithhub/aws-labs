<p align="center">
  <img src="https://img.shields.io/badge/AWS-RDS-darkblue" alt="AWS Badge">
</p>


# ☁ Day 18 - Amazon RDS (Relational Database Service) with EC2 Web Application

## Overview

On Day-18, I learned how to deploy a fully managed relational database using **Amazon RDS** and connect it to a PHP web application running on an Amazon EC2 instance.

The project demonstrates how a web server communicates securely with a MySQL database hosted on Amazon RDS. I also configured networking, security groups, database subnet groups, and Multi-AZ deployment to understand how production-grade database services are designed in AWS.

---

# Architecture

<img width="402" height="882" alt="RDS1 drawio" src="https://github.com/user-attachments/assets/1b04958c-9339-45c0-a33b-72b17a1c207b" />

---

# AWS Services Used

- Amazon RDS
- Amazon EC2
- Amazon VPC
- Security Groups
- DB Subnet Group
- MySQL
- Internet Gateway
- NAT Gateway
- CloudWatch
- Multi-AZ Deployment

---

# What is Amazon RDS?

Amazon Relational Database Service (Amazon RDS) is a fully managed database service that allows developers to create, operate, and scale relational databases without managing the underlying infrastructure.

AWS automatically manages:

- Database installation
- Operating system maintenance
- Software patching
- Storage management
- High Availability
- Monitoring
- Database backups (optional)
- Automatic failover (Multi-AZ)

---

# Why Amazon RDS Instead of Installing MySQL on EC2?

If MySQL is installed manually on an EC2 instance, the administrator is responsible for:

- Installing MySQL
- Managing updates
- Performing backups
- Handling replication
- Configuring failover
- Scaling storage
- Recovering from failures

With Amazon RDS, AWS performs these operational tasks automatically, allowing developers to focus on building applications instead of managing database servers.

---

# What is a Relational Database?

A relational database stores data in the form of tables.

Example:

## Users Table

| User ID | Name | Email |
|---------|------|-------|
| 101 | Shashank | shashank@email.com |
| 102 | Rajkumar | kumar@email.com |
| 103 | Divyashree | shree@email.com |
| 104 | Ujwal | uju@email.com |

Relationships between tables are established using primary keys and foreign keys.

Amazon RDS supports several relational database engines including:

- MySQL
- PostgreSQL
- MariaDB
- Oracle
- Microsoft SQL Server

---

# Database Architecture

<img width="402" height="550" alt="RDS22 drawio" src="https://github.com/user-attachments/assets/474dcbc8-a8d6-4dfb-8789-1aa8bc5d63ca" />

The web application communicates with the database using the RDS Endpoint.

---

# VPC Configuration

Create VPC:

```
RDS-VPC
```

Create Internet Gateway:

```
RDS-IGW
```

Create Subnets:

```
RDS-Public-subnet-1
RDS-Public-subnet-2
RDS-Private-subnet-1
RDS-Private-subnet-2
```

Create Route Table:

```
RDS-Public-RT --> Edit subnet association --> Edit routes --> Internet Gateway
RDS-Private-RT --> Edit subnet association --> Edit routes --> Nat Gateway
```

Create Nat Gateway:

```
RDS-NAT
```

---

# EC2 Instance Configuration

```
Name - RDS-Server
AMI - Amazon-Linux
Key pair - rdskey
Configure Network settings
COnfigure storage - 15 GiB
```
User Data:

```
#!/bin/bash -ex
# Updated to use Amazon Linux 2023
dnf update -y
dnf install -y httpd wget php-fpm php-mysqli php-json php php-devel
dnf install -y mariadb105-server
/usr/bin/systemctl enable httpd
/usr/bin/systemctl start httpd
cd /var/www/html
wget
https://aws-tc-largeobjects.s3.amazonaws.com/CUR-TF-100-ACCLFO-2/lab5-rds/lab-app-p
hp7.zip
unzip lab-app-php7.zip -d /var/www/html/
chown -R apache:root /var/www/html 
```

---

# Security Architecture

A dedicated Database Security Group was created.

Inbound Rule:

```
Port : 3306

Source :

Web Security Group
```

This configuration allows only the EC2 web server to communicate with the database.

The database remains inaccessible directly from the Internet.

---

# DB Subnet Group

A DB Subnet Group defines the subnets where Amazon RDS is allowed to deploy database instances.

In this project:

- Private Subnet 1
- Private Subnet 2

were associated with the DB Subnet Group.

This enables Multi-AZ deployment across different Availability Zones.

---

# Multi-AZ Deployment

Amazon RDS automatically creates:

```
Primary Database

↓

Synchronous Replication

↓

Standby Database
```

Advantages:

- High Availability
- Automatic Failover
- Improved Reliability
- Disaster Recovery

Applications always communicate with the primary database.

If the primary instance fails, AWS automatically redirects traffic to the standby instance.

---

# RDS Configuration

Database Engine

```
MySQL
```

Deployment

```
Multi-AZ
```

DB Instance Class

```
db.t3.micro
```

Storage

```
20 GB General Purpose SSD
```

Database Name

```
lab
```

Master Username

```
main
```

---

# Components Used

## Amazon EC2

Hosts the PHP web application.

---

## Amazon RDS

Stores all application data.

---

## Security Groups

Controls network-level access.

---

## DB Subnet Group

Determines where the database can be deployed.

---

## Multi-AZ

Maintains a standby database for high availability.

---

# Application Workflow

<img width="402" height="650" alt="RDS3 drawio" src="https://github.com/user-attachments/assets/2890c19e-3e57-4fe3-a3b8-fd96a4a42f0d" />

---

# CRUD Operations Performed

The web application successfully performed:

- Create Contact
- Read Contact
- Update Contact
- Delete Contact

The data is stored in Amazon RDS and remains persistent.

---

# Advantages of Amazon RDS

- Fully Managed Service
- Automatic Software Updates
- High Availability
- Automatic Failover
- Storage Scalability
- Database Monitoring
- Easy Deployment
- Secure Networking
- Multi-AZ Support

---

# Difference Between EC2 Database and Amazon RDS

| EC2 MySQL | Amazon RDS |
|-----------|------------|
| Manual installation | AWS managed |
| Manual patching | Automatic patching |
| Manual backups | Automated backups |
| Manual replication | Multi-AZ support |
| Manual monitoring | CloudWatch integration |
| High administration effort | Low administration effort |

---

# Screenshots

- VPC and Network Configuration
  <img width="1907" height="1009" alt="Screenshot 2026-07-30 121014" src="https://github.com/user-attachments/assets/d4eb293b-d2df-4160-977c-b2ea99cc0ca3" />
  <img width="1907" height="1012" alt="Screenshot 2026-07-30 121058" src="https://github.com/user-attachments/assets/2317fcd3-b013-4cef-a84d-6614d93cc10d" />
  <img width="1907" height="1011" alt="Screenshot 2026-07-30 121355" src="https://github.com/user-attachments/assets/21d9abf2-9a71-446e-bd25-f1195ee2c882" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-30 121631" src="https://github.com/user-attachments/assets/cc2b6694-52bb-4bd2-be8b-17bec5925094" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-30 121832" src="https://github.com/user-attachments/assets/c145907b-5181-4b33-bcd1-eeed9d9aabfc" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-30 122120" src="https://github.com/user-attachments/assets/5e563605-9a4e-495f-b1ba-c51e87cb91bf" />
  <img width="1597" height="359" alt="Screenshot 2026-07-30 122609" src="https://github.com/user-attachments/assets/a2873aa2-721d-4cd3-8e0e-80e53b08ddad" />
  <img width="1907" height="676" alt="Screenshot 2026-07-30 122735" src="https://github.com/user-attachments/assets/6aa7cc1d-8d11-4dca-a727-a3f08f48f969" />

- EC2 Configuration
  <img width="1907" height="1010" alt="Screenshot 2026-07-30 122833" src="https://github.com/user-attachments/assets/00b15992-a91d-4cc2-9673-6ec477350a51" />
  <img width="1907" height="1012" alt="Screenshot 2026-07-30 123254" src="https://github.com/user-attachments/assets/c8f95577-f30a-468c-b113-2455aaef4420" />
  <img width="1907" height="1012" alt="Screenshot 2026-07-30 123303" src="https://github.com/user-attachments/assets/898c157a-e4c4-4f47-bf8e-88346f194503" />
  <img width="1907" height="1011" alt="Screenshot 2026-07-30 123317" src="https://github.com/user-attachments/assets/b11f3ab9-0cd7-405f-a8ac-f4de500094a1" />
  <img width="1907" height="1013" alt="Screenshot 2026-07-30 123619" src="https://github.com/user-attachments/assets/047a1a7a-0211-4480-9b00-eda24c408af0" />
  <img width="1907" height="1011" alt="Screenshot 2026-07-30 123629" src="https://github.com/user-attachments/assets/9e939f3a-0c1b-4df2-92f0-3c9cfa49c90a" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-30 123643" src="https://github.com/user-attachments/assets/ca6cd28d-7c59-437b-b56f-10e510991e13" />
  <img width="1907" height="1006" alt="Screenshot 2026-07-30 123708" src="https://github.com/user-attachments/assets/40546c37-c5aa-47ff-98cd-2cdccd5e1687" />

- RDS Security Group
  <img width="1907" height="1012" alt="Screenshot 2026-07-30 123850" src="https://github.com/user-attachments/assets/fc8a4084-d230-4f1a-9c5d-f96116cc02df" />

- DB Subnet Group
  <img width="1907" height="1012" alt="Screenshot 2026-07-30 124051" src="https://github.com/user-attachments/assets/3ebbbd9a-1e5f-427a-a371-f444daba21f0" />
  <img width="1907" height="1008" alt="Screenshot 2026-07-30 124056" src="https://github.com/user-attachments/assets/07458014-9161-44ba-be79-65463b0f84ae" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-30 124108" src="https://github.com/user-attachments/assets/8bf3d717-6fce-4caf-a6fd-02add0cbbd79" />

- Amazon RDS Database
  <img width="1907" height="1011" alt="Screenshot 2026-07-30 124135" src="https://github.com/user-attachments/assets/54a9a995-2099-4ce0-81bb-1da99677a408" />
  <img width="1904" height="1010" alt="Screenshot 2026-07-30 130348" src="https://github.com/user-attachments/assets/cd7d7ecf-0013-4870-aa9c-7ff7428dad84" />
  <img width="1907" height="1013" alt="Screenshot 2026-07-30 130407" src="https://github.com/user-attachments/assets/90deb421-eabf-4023-9fdc-ec75b55cfd5a" />
  <img width="1907" height="1008" alt="Screenshot 2026-07-30 130415" src="https://github.com/user-attachments/assets/296d8cbc-7600-4b4d-a90a-e803c6aab709" />
  <img width="1907" height="1012" alt="Screenshot 2026-07-30 130423" src="https://github.com/user-attachments/assets/50f0405b-c2d9-4e20-a4de-f9d8746903c8" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-30 130430" src="https://github.com/user-attachments/assets/c8a10bdc-be46-4b0d-8403-9cefc7f49948" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-30 130439" src="https://github.com/user-attachments/assets/e237ab88-8756-433a-b866-c62328c3e45a" />
  <img width="1907" height="1011" alt="Screenshot 2026-07-30 130445" src="https://github.com/user-attachments/assets/3a07030d-977e-475e-81cd-7f16425f40a7" />
  <img width="1906" height="1006" alt="Screenshot 2026-07-30 130455" src="https://github.com/user-attachments/assets/b509caa3-1222-43c2-b9c5-f50fb59ff374" />
  <img width="1905" height="1004" alt="Screenshot 2026-07-30 130501" src="https://github.com/user-attachments/assets/54670eb0-6ea3-4c71-a7a9-d12c9e1f7cf8" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-30 130848" src="https://github.com/user-attachments/assets/6a409d41-ed6a-4fbd-9e5e-e7c2c12e86e6" />

- Single-AZ Deployment
  <img width="1907" height="1009" alt="Screenshot 2026-07-30 130402" src="https://github.com/user-attachments/assets/d8d2b36c-15fe-4b4b-a774-c75728ec5d71" />

- RDS Endpoint
  <img width="1907" height="1009" alt="Screenshot 2026-07-30 131034" src="https://github.com/user-attachments/assets/bc39a6a3-211b-456f-a6d3-a6b9d71ce7c3" />

- EC2 Web Application
  <img width="1907" height="1009" alt="Screenshot 2026-07-30 131058" src="https://github.com/user-attachments/assets/22da65b0-af5d-4701-827c-82c98405cc18" />

- Address Book Application
  <img width="1907" height="1012" alt="Screenshot 2026-07-30 131431" src="https://github.com/user-attachments/assets/13ce8ce8-d129-4df4-9022-deb2af497a64" />

- CRUD Operations
  <img width="1907" height="1009" alt="Screenshot 2026-07-30 131716" src="https://github.com/user-attachments/assets/b1447fa9-e04b-4050-880d-7e0eb692024e" />

---

# Interview Questions

### What is Amazon RDS?

Amazon RDS is a fully managed relational database service provided by AWS.

---

### Why use Amazon RDS?

To eliminate database administration tasks such as installation, patching, backups, monitoring, and failover.

---

### What is Multi-AZ?

A deployment model where Amazon RDS maintains a synchronous standby database in another Availability Zone to provide high availability.

---

### What is a DB Subnet Group?

A collection of subnets where Amazon RDS is permitted to deploy database instances.

---

### Why is Amazon RDS deployed inside private subnets?

To prevent direct Internet access and improve security.

---

### What is the RDS Endpoint?

The DNS address used by applications to communicate with the database.

---

### Which protocol does EC2 use to communicate with MySQL?

MySQL Protocol

Port:

```
3306
```

---

### Can users directly access Amazon RDS from the Internet?

No.

Users communicate with the EC2 web application, and the application communicates with Amazon RDS.

---

# Key Learnings

- Amazon RDS Fundamentals
- Relational Databases
- MySQL
- DB Instance
- DB Endpoint
- DB Subnet Group
- Security Groups
- Multi-AZ Deployment
- High Availability
- EC2 to RDS Connectivity
- CRUD Operations
- PHP Web Application Integration
- Database Networking
- Production Database Architecture

---

# Conclusion

On Day-18, I successfully deployed a MySQL database using Amazon RDS and integrated it with a PHP web application hosted on an Amazon EC2 instance.

I configured networking, security groups, DB subnet groups, and Multi-AZ deployment to create a secure and highly available database environment. The application successfully performed Create, Read, Update, and Delete (CRUD) operations, demonstrating end-to-end communication between the web server and the managed database service.

This project provided hands-on experience with building scalable, secure, and production-ready database architectures on AWS.
