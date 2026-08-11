<p align="center">
  <img src="https://img.shields.io/badge/AWS-DynomoDB-5865F2" alt="AWS Badge">
</p>

# ☁ Day 21 – Amazon DynamoDB

#  Overview

This repository documents my hands-on learning and implementation of **Amazon DynamoDB**, AWS's fully managed NoSQL database service.

The objective was to understand how DynamoDB stores data and how different access patterns are implemented using partition keys, sort keys, and secondary indexes.

---

#  Objectives

The main objectives of this hands-on were:

* Understand DynamoDB and NoSQL databases
* Create and configure DynamoDB tables
* Understand partition keys
* Understand sort keys
* Insert items into DynamoDB
* Perform CRUD operations
* Perform Query operations
* Perform Scan operations
* Filter query results
* Create composite primary keys
* Create a Global Secondary Index (GSI)
* Query data using a GSI
* Understand DynamoDB access patterns

---

#  AWS Service Used

## Amazon DynamoDB

**Amazon DynamoDB** is a fully managed, serverless NoSQL database designed to provide fast and predictable performance at scale.

DynamoDB stores data as **items**, which contain **attributes**.

Unlike relational databases such as MySQL, DynamoDB does not require a fixed table schema for every attribute.

---

#  DynamoDB Concepts

## 1. Table

A DynamoDB table is a collection of items.

Example:

```text
student-management
```

---

## 2. Item

An item is an individual record stored inside a DynamoDB table.

Example:

```text
Student ID: STU001
Name: Shashank
Age: 22
Course: Cloud Computing
```

---

## 3. Attribute

Attributes are the individual pieces of data stored inside an item.

Example:

```text
student_id
name
age
course
status
```

---

## 4. Partition Key

The partition key uniquely identifies an item when using a simple primary key.

Example:

```text
student_id
```

The value:

```text
STU001
```

can identify a particular student.

---

## 5. Sort Key

A sort key is used together with a partition key to create a **composite primary key**.

Example:

```text
Partition Key → student_id
Sort Key       → course_id
```

This allows multiple related items to exist under the same partition key.

---

#  Hands-On Implementation

## Step 1 — Open DynamoDB

1. Sign in to the AWS Management Console.
2. Search for:

```text
DynamoDB
```

3. Open **Amazon DynamoDB**.
4. Select the AWS region:

```text
ap-south-2
```

---

## Step 2 — Create `student-management` Table

I created a DynamoDB table named:

```text
student-management
```

The primary key used was:

```text
student_id
```

### Configuration

```text
Table Name: student-management
Partition Key: student_id
```

The table was then created through the AWS Management Console.

---

## Step 3 — Add Student Items

Student records were inserted into the table.

Example:

```text
student_id = STU001
name       = Shashank
age        = 22
course     = Cloud Computing
status     = Active
```

Additional student records were also added for practicing DynamoDB operations.

---

## Step 4 — Create Operation

The first CRUD operation performed was **Create**.

A new item was added to the:

```text
student-management
```

table.

Example:

```text
student_id = STU001
name       = Shashank
age        = 22
course     = Cloud Computing
status     = Active
```

This demonstrated how new records can be stored in DynamoDB.

---

## Step 5 — Read Operation

The **Read** operation was performed to retrieve an existing item from DynamoDB.

The partition key was used to identify the required student.

Example:

```text
student_id = STU001
```

DynamoDB returned the corresponding student item.

---

## Step 6 — Update Operation

The student record was modified using the **Update** operation.

For example, an existing attribute could be changed:

```text
status = Active
```

to another value.

This demonstrated how existing DynamoDB items can be modified without updating an entire table.

---

## Step 7 — Delete Operation

The **Delete** operation was also performed.

An item was selected using its primary key and removed from the table.

Example:

```text
student_id = STU001
```

This demonstrated the final CRUD operation.

---

## Step 8 — Query Operation

I performed a **Query** operation on the DynamoDB table.

A Query retrieves items based on the table's key structure.

Example:

```text
student_id = STU001
```

The Query operation is efficient because it uses the table's key rather than examining every item.

---

## Step 9 — Scan Operation

I also performed a **Scan** operation.

Unlike Query, Scan examines every item in the table before returning matching results.

Conceptually:

```text
Query → Uses key
Scan  → Examines all items
```

### Query

```text
Search using partition key
```

### Scan

```text
Read all items and then filter results
```

This hands-on helped demonstrate the practical difference between Query and Scan.

---

## Step 10 — Create `student-courses` Table

To understand DynamoDB composite keys, I created another table:

```text
student-courses
```

The table used a composite primary key.

### Primary Key Configuration

```text
Partition Key → student_id
Sort Key       → course_id
```

Therefore:

```text
student_id + course_id
```

together uniquely identify an item.

---

## Step 11 — Add Course Records

Course records were added to the:

```text
student-courses
```

table.

Example structure:

```text
student_id = STU001
course_id  = AWS001
course     = AWS Cloud
status     = Completed
```

Another course could belong to the same student:

```text
student_id = STU001
course_id  = LINUX001
course     = Linux Administration
status     = In Progress
```

This demonstrates an important DynamoDB design pattern:

```text
One student
     |
     ├── AWS course
     ├── Linux course
     └── SQL course
```

The same partition key can contain multiple items because the sort key differentiates them.

---

## Step 12 — Query Student Courses

I queried the:

```text
student-courses
```

table using:

```text
student_id = STU001
```

This returned the courses associated with that student.

Example:

```text
STU001
 ├── AWS001
 ├── LINUX001
 └── SQL001
```

This demonstrated how a partition key can be used to retrieve a group of related items.

---

## Step 13 — Update Course Information

I updated the Linux course status.

For example:

```text
course = Linux
status = Completed
```

This demonstrated how individual attributes of an existing DynamoDB item can be updated.

---

## Step 14 — Filter Query Results

I then filtered the course records to retrieve courses with:

```text
status = Completed
```

This allowed completed courses to be identified from the student's course records.

Example:

```text
Student: STU001

Completed:
- AWS
- Linux
```

---

## Step 15 — Create Global Secondary Index

To understand DynamoDB secondary indexes, I created a **Global Secondary Index (GSI)**.

The index was named:

```text
course-index
```

### GSI Configuration

```text
GSI Name: course-index

Partition Key:
course

Sort Key:
student_id
```

This created a different access pattern for the same underlying data.

---

## Step 16 — Query Using GSI

The `course-index` GSI was then used to query students based on their course.

For example:

```text
course = AWS
```

The query returned students associated with the AWS course.

This demonstrated why secondary indexes are useful in DynamoDB.

The original table was designed around:

```text
student_id
```

while the GSI allowed the data to be accessed using:

```text
course
```

---

#  DynamoDB Access Patterns

The hands-on demonstrated multiple ways to access the same data.

### Access Pattern 1 — Find a Student

```text
student_id → STU001
```

### Access Pattern 2 — Find All Courses of a Student

```text
student_id → STU001
```

using the `student-courses` table.

### Access Pattern 3 — Find Students Taking a Course

```text
course → AWS
```

using:

```text
course-index
```

This is an important DynamoDB concept because DynamoDB database design is heavily based on **access patterns**.

---

#  Query vs Scan

| Feature            | Query                    | Scan                     |
| ------------------ | ------------------------ | ------------------------ |
| Uses key           | Yes                      | Not necessarily          |
| Reads entire table | No                       | Yes                      |
| Performance        | Generally more efficient | Generally less efficient |
| Best for           | Known access patterns    | Examining broad datasets |
| Hands-on           | Completed                | Completed                |

### Example

Query:

```text
student_id = STU001
```

Scan:

```text
Examine all student records
```

---

#  Simple Key vs Composite Key

## Simple Primary Key

The `student-management` table uses:

```text
student_id
```

Example:

```text
STU001
```

---

## Composite Primary Key

The `student-courses` table uses:

```text
student_id + course_id
```

Example:

```text
STU001 + AWS001
```

This allows multiple course records to belong to the same student.

---

#  Tables Created

## `student-management`

```text
Partition Key:
student_id
```

Purpose:

```text
Store and manage student information
```

Operations performed:

* Create
* Read
* Update
* Delete
* Query
* Scan

---

## `student-courses`

```text
Partition Key:
student_id

Sort Key:
course_id
```

Purpose:

```text
Store courses associated with students
```

Operations performed:

* Insert course records
* Query courses by student
* Update course status
* Filter completed courses

---

## `course-index`

Global Secondary Index:

```text
Partition Key:
course

Sort Key:
student_id
```

Purpose:

```text
Find students based on their course
```

---

#  Architecture

<img width="682" height="572" alt="DynamoDB drawio" src="https://github.com/user-attachments/assets/b051e50d-e86f-4ae1-b518-53e51835a8ef" />

---

#  Screenshots

- DynamoDB Dashboard
  <img width="1919" height="1020" alt="Screenshot 2026-08-11 101535" src="https://github.com/user-attachments/assets/7688a60a-62bc-485b-af65-484238e8c1fe" />

- Table Creation
  <img width="1919" height="1020" alt="Screenshot 2026-08-11 101703" src="https://github.com/user-attachments/assets/623ac03c-2705-4018-98e6-54c6c19651d8" />
  <img width="1919" height="1018" alt="Screenshot 2026-08-11 101708" src="https://github.com/user-attachments/assets/217589de-8c18-4f91-a7d7-c52304d23475" />
  <img width="1919" height="1017" alt="Screenshot 2026-08-11 102149" src="https://github.com/user-attachments/assets/33cffd4a-ab42-4d6a-bb43-fe8448ad38e0" />
  
- 'student-management` Table
  <img width="1919" height="1019" alt="Screenshot 2026-08-11 102255" src="https://github.com/user-attachments/assets/3cc1f6d0-f68e-4096-b78f-ad9cd2d629c8" />

- Student Items
  <img width="1919" height="1018" alt="Screenshot 2026-08-11 102335" src="https://github.com/user-attachments/assets/7a8c57ed-e2d4-4722-bb98-2ab38ca4c937" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-11 102450" src="https://github.com/user-attachments/assets/7be45f1b-079d-4ae3-9d2c-78fc04ddad14" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-11 102515" src="https://github.com/user-attachments/assets/3dad00bf-72c2-4c58-8c63-a4b22e47b7b7" />

- Query Operation
  <img width="1917" height="1018" alt="Screenshot 2026-08-11 103413" src="https://github.com/user-attachments/assets/33164275-6741-4d58-a56f-9e25b978cc5b" />
  <img width="1919" height="1016" alt="Screenshot 2026-08-11 111956" src="https://github.com/user-attachments/assets/5aae170e-0885-495f-92b4-7680710f47c6" />
  <img width="1919" height="1015" alt="Screenshot 2026-08-11 112005" src="https://github.com/user-attachments/assets/64d1efd6-bfc2-4c79-b2da-0a499684dd2e" />

- Scan Operation

- 'student-courses' Table
  <img width="1919" height="1017" alt="Screenshot 2026-08-11 114340" src="https://github.com/user-attachments/assets/10467dd7-8095-4020-b179-b9d52fc7eda4" />
  <img width="1919" height="1020" alt="Screenshot 2026-08-11 114558" src="https://github.com/user-attachments/assets/86199fd7-e69e-4575-a4aa-a3e3f2b07733" />
  <img width="1917" height="1014" alt="Screenshot 2026-08-11 114710" src="https://github.com/user-attachments/assets/a7412b74-a575-46b7-be1b-66e5c4e53146" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-11 115051" src="https://github.com/user-attachments/assets/c978f127-1fef-4de3-8649-f6c729e8fe86" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-11 115054" src="https://github.com/user-attachments/assets/ff0126cd-beb7-4819-857b-bca398adf967" />
  <img width="1919" height="1018" alt="Screenshot 2026-08-11 120033" src="https://github.com/user-attachments/assets/19103e5c-c53e-4e8a-947f-9770e5992a06" />
  <img width="1919" height="1019" alt="Screenshot 2026-08-11 120048" src="https://github.com/user-attachments/assets/deecbc61-7edc-48fc-b452-021abefb6d5f" />

- Global Secondary Index
  <img width="1919" height="1020" alt="Screenshot 2026-08-11 120549" src="https://github.com/user-attachments/assets/840c644c-08ac-4dcd-a477-b2d67ae5e133" />
  <img width="1919" height="1015" alt="Screenshot 2026-08-11 121504" src="https://github.com/user-attachments/assets/656286f7-314a-4ba8-acc5-a237dddaab8e" />
  
- GSI Query
  <img width="1919" height="1018" alt="Screenshot 2026-08-11 121558" src="https://github.com/user-attachments/assets/b9cc49af-ae69-47e0-b73b-458b0ba27584" />
  <img width="1919" height="1017" alt="Screenshot 2026-08-11 121602" src="https://github.com/user-attachments/assets/22f725be-6645-4afe-a363-01fe3a3fb72e" />

---

#  Key Learnings

Through this hands-on, I learned:

* DynamoDB is a NoSQL database service.
* DynamoDB stores data as items and attributes.
* Partition keys determine how data is organized and accessed.
* Sort keys allow multiple related items under the same partition key.
* CRUD operations can be performed directly on DynamoDB items.
* Query is designed around known key-based access patterns.
* Scan examines the table more broadly and should be used carefully.
* Composite keys enable one-to-many data relationships.
* Global Secondary Indexes provide alternative ways to query data.
* DynamoDB table design should begin with the application's access patterns.

---

#  What I Practiced

The overall workflow was:

```text
Create Table
     ↓
Add Items
     ↓
CRUD Operations
     ↓
Query
     ↓
Scan
     ↓
Composite Keys
     ↓
Filter Data
     ↓
Create GSI
     ↓
Query Using GSI
```

---

#  Important DynamoDB Design Principle

One of the most important concepts I learned is:

> **DynamoDB design should be based on access patterns.**

Instead of designing a DynamoDB table exactly like a traditional relational database, the table and indexes should be designed around how the application needs to retrieve data.

For example:

```text
Requirement:
Find all students taking AWS

Access Pattern:
course = AWS

Solution:
course-index GSI
```

This hands-on demonstrated how DynamoDB indexes can support additional access patterns without changing the original table's primary key.

---

#  Conclusion

This hands-on provided practical experience with **Amazon DynamoDB**, from creating tables and managing items to designing composite keys and Global Secondary Indexes.

The implementation covered both basic database operations and more advanced NoSQL concepts such as **access-pattern-based design, composite keys, filtering, and secondary indexes**.

This project forms part of my AWS hands-on learning journey and provides practical experience with AWS managed database services.

---

