<p align="center">
  <img src="https://img.shields.io/badge/AWS-EBS-orange" alt="AWS Badge">
</p>

# ☁ Day 09 - Amazon Elastic Block Store (EBS)

## Objective

To understand Amazon Elastic Block Store (EBS), learn how to create and attach EBS volumes to EC2 instances, and create snapshots for backup and recovery.

---

# What is Amazon EBS?

Amazon Elastic Block Store (EBS) is a block-level storage service that provides persistent storage for Amazon EC2 instances.

Unlike the instance store, EBS volumes retain data even if the EC2 instance is stopped.

---

# Features of Amazon EBS

* Persistent block storage
* High durability and availability
* Easy to resize volumes
* Supports encryption
* Backup using Snapshots
* Can be attached and detached from EC2 instances

---

# Types of EBS Volumes

## 1. General Purpose SSD (gp3)

* Most commonly used
* Suitable for web servers and development environments
* Balanced performance and cost

---

## 2. Provisioned IOPS SSD (io2)

* High-performance storage
* Designed for mission-critical databases

---

## 3. Throughput Optimized HDD (st1)

* Suitable for large, sequential workloads
* Used for big data and log processing

---

## 4. Cold HDD (sc1)

* Low-cost storage
* Used for infrequently accessed data

---

# EBS Architecture

<img width="521" height="481" alt="EBS drawio" src="https://github.com/user-attachments/assets/ec3713b6-4edc-4f6b-93d0-c034d56e9538" />

---

# What is an EBS Snapshot?

An EBS Snapshot is a point-in-time backup of an EBS volume.

Snapshots are stored in Amazon S3 (managed internally by AWS) and can be used to:

* Restore lost data
* Create new EBS volumes
* Backup critical information

---

# Practical Performed

## Step 1: Create an EBS Volume

Navigate to:

EC2 → Elastic Block Store → Volumes

Configuration:

* Volume Type: gp3
* Size: 10 GB
* Availability Zone: Same as EC2 Instance

---

## Step 2: Attach Volume

Select the created volume.

Click:

Actions → Attach Volume

Choose the running EC2 instance.

Example Device Name:

```text
/dev/nvmw1n1
```

---

## Step 3: Verify the Volume

Connect to the EC2 instance and verify the new disk:

```bash
lsblk
```

Expected output:

```text
nvme1n1      259:5    0    9G  0 disk 
```

---

## Step 4: List the disk partition on the system:

```bash
sudo fdisk -l
```

---

## Step 5: Check the file system:

```bash
sudo file -s /dev/nvme1n1
```

---

## Step 6: If the output is data, then create the file system:

```bash
sudo mkfs -t xfs /dev/nvme1n1
```

## Step 7: Recheck the file system:

```bash
sudo file -s /dev/nvme1n1
```

---

## Step 8: Create a mount point directory for the volume:

```bash
sudo mkdir /mydata
```

## Step 9: Mount the volume:

```bash
sudo mount /dev/nvme1n1 /mydata
```

## Step 10: Run df -h to view the data: 

```bash
df -h
```

Navigate to:

EC2 → Volumes

Select the volume.

Click:

Actions → Create Snapshot

Provide a name and description.

Create the snapshot.

---

# Practical Outcome

✅ Created an EBS Volume.

✅ Attached the volume to an EC2 instance.

✅ Formatted and mounted the volume.

✅ Verified the mounted storage.

✅ Created an EBS Snapshot for backup.

---

# Advantages of EBS

* Persistent storage
* High availability
* Easy backup using snapshots
* Data survives EC2 stop/start
* Supports encryption
* Can increase storage without replacing the instance

---

# Key Learnings

* Learned the purpose of Amazon EBS.
* Understood different EBS volume types.
* Attached storage to an EC2 instance.
* Mounted a new volume in Linux.
* Created an EBS Snapshot.

---

# Interview Questions

### What is Amazon EBS?

Amazon Elastic Block Store (EBS) is a persistent block storage service for Amazon EC2 instances.

---

### Is EBS persistent?

Yes. Data stored in an EBS volume remains even if the EC2 instance is stopped.

---

### What is an EBS Snapshot?

An EBS Snapshot is a point-in-time backup of an EBS volume.

---

### Can one EBS volume be attached to multiple EC2 instances?

Generally, an EBS volume can be attached to only one EC2 instance at a time (with some specialized Multi-Attach exceptions for supported volume types).

---

### Difference between EBS and S3

| Amazon EBS      | Amazon S3                       |
| --------------- | ------------------------------- |
| Block Storage   | Object Storage                  |
| Attached to EC2 | Standalone Storage              |
| Used as a Disk  | Used to Store Files and Objects |

---

# Screenshots

* EBS Volume Creation<img width="1907" height="1008" alt="Screenshot 2026-07-10 223946" src="https://github.com/user-attachments/assets/0a26a514-5d04-4313-89b3-3b60b7d47c91" />
  <img width="1906" height="1010" alt="Screenshot 2026-07-10 223953" src="https://github.com/user-attachments/assets/24a8a9fb-8a55-417a-af2a-607db9a81662" />

* Volume Details<img width="1907" height="1012" alt="Screenshot 2026-07-10 224058" src="https://github.com/user-attachments/assets/38b0a4b6-502f-45a8-b0e2-2c686636fc69" />
  <img width="1907" height="1009" alt="Screenshot 2026-07-10 224106" src="https://github.com/user-attachments/assets/8dc208ad-0eaf-4600-8454-33b50872bcb5" />

* Attach Volume Window<img width="1907" height="1010" alt="Screenshot 2026-07-10 224252" src="https://github.com/user-attachments/assets/e64ff7c3-2118-48fc-8024-e12ba74a92e1" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-10 224323" src="https://github.com/user-attachments/assets/3b43d77e-b22c-4ba0-8035-e2f138dda03f" />

* EC2 Instance with Attached Volume<img width="1907" height="1011" alt="Screenshot 2026-07-10 224509" src="https://github.com/user-attachments/assets/8671946e-46c3-4a1f-92fe-f36c769c3d36" />

* Linux Terminal (`lsblk`)<img width="1907" height="1008" alt="Screenshot 2026-07-10 221455" src="https://github.com/user-attachments/assets/854b0dc3-f61c-4447-98a9-0e66e9d69fa7" />

* Mounted Volume (`df -h`)<img width="1907" height="1008" alt="Screenshot 2026-07-10 223416" src="https://github.com/user-attachments/assets/b562f33c-c559-49c9-b1d1-dc7cb6f6c317" />

* Snapshot Creation<img width="1907" height="1007" alt="Screenshot 2026-07-10 223616" src="https://github.com/user-attachments/assets/712c054d-8f06-4795-b84e-6136d039c41d" />
  <img width="1907" height="1010" alt="Screenshot 2026-07-10 223623" src="https://github.com/user-attachments/assets/d9aca71c-927e-49c5-8dbd-188def4db4b3" />
  <img width="1907" height="1007" alt="Screenshot 2026-07-10 223659" src="https://github.com/user-attachments/assets/bb1feae5-c602-4c7d-888e-cd82885b9b54" />

* Snapshot Details<img width="1907" height="1009" alt="Screenshot 2026-07-10 223721" src="https://github.com/user-attachments/assets/b86bd8c1-19fe-43a5-b554-6625e1be7e07" />

---

# Conclusion

Successfully created an Amazon EBS volume, attached it to an EC2 instance, formatted and mounted the storage, and created an EBS Snapshot for backup and recovery. This practical demonstrated how persistent block storage is managed in AWS.
