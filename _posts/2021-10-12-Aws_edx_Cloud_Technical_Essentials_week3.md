---
title: "AWS - AWS Cloud Technical Essentials_week3"
categories:
  - AWS
tags:
  - AWS
---

> **Work hard, have fun, and make history.**  
> [AWS Cloud Technical Essentials](https://www.edx.org/course/aws-cloud-technical-essentials)

# AWS Cloud Technical Essentials - Week3

## Storage Types on AWS

> AWS storage services are grouped into three different categories: block storage, file storage, and object storage.


![storage Types](https://raw.githubusercontent.com/sujinsjlee/TIL/master/assets/images/storageTypes.png)

- **File Storage**
  - You may be familiar with file storage if you’ve interacted with file storage systems like Windows File Explorer or Finder on MacOS. 
  - You place your files in a tree-like hierarchy that consists of folders and subfolders. 

- **Block Storage**
  - While file storage treats files as a singular unit, block storage splits files into fixed-size chunks of data called blocks that have their own addresses. Since each block is addressable, blocks can be retrieved efficiently.

- **Object Storage**
  - Objects, much like files, are also treated as a single unit of data when stored.
  - However, unlike file storage, these objects are stored in a flat structure instead of a hierarchy. Each object is a file with a unique identifier. This identifier, along with any additional metadata, is bundled with the data and stored.

## Amazon EC2 Instance Storage and Amazon Elastic Block Store

- **Amazon EC2 Instance Store**
  - EC2 Instance Store is located on disks that are physically attached to the host computer. 

- **Amazon Elastic Block Storage (Amazon EBS)**
  - Amazon EBS is a block-level storage device that you can attach to an Amazon EC2 instance
  - These storage devices are called Amazon EBS volumes. EBS volumes are essentially drives of a user-configured size attached to an EC2 instance, similar to how you might attach an external drive to your laptop.

  - Most Amazon EBS volumes can only be connected with one computer at a time. Most EBS volumes have a one-to-one relationship with EC2 instances, so they cannot be shared by or attached to multiple instances at one time. *Note: Recently, AWS announced the Amazon EBS multi-attach feature that enables volumes to be attached to multiple EC2 instances at one time. This feature is not available for all instance types and all instances must be in the same Availability Zone.*

  - You can detach an EBS volume from one EC2 instance and attach it to another EC2 instance in the same Availability Zone, to access the data on it.

  - If an accident happens and the computer goes down, you still have your data on your external drive. 
  - You’re limited to the size of the external drive, since it has a fixed limit to how scalable it can be. 

- **Scale Amazon EBS Volumes**
  - You can scale Amazon EBS volumes in two ways.
    - Increase the volume size, as long as it doesn’t increase above the maximum size limit. 
    - Attach multiple volumes to a single Amazon EC2 instance. EC2 has a one-to-many relationship with EBS volumes.

- **Amazon EBS Volume Types**
  - There are two main categories of Amazon EBS volumes
    - solid-state drives (SSDs)
    - hard-disk drives (HDDs)

- **Benefits of Using Amazon EBS**
  - High availability: When you create an EBS volume, it is automatically replicated within its Availability Zone to prevent data loss from single points of failure.
  - Data persistence: The storage persists even when your instance doesn’t.
  - Data encryption: All EBS volumes support encryption.
  - Flexibility: EBS volumes support on-the-fly changes. You can modify volume type, volume size, and input/output operations per second (IOPS) capacity without stopping your instance.
  - Backups: Amazon EBS provides you the ability to create backups of any EBS volume.

- **EBS Snapshots (Backups of EBS volumes)**
> Errors happen. One of those errors is not backing up data, and then, inevitably losing that data. To prevent this from happening to you, you should back up your data—even in AWS with EBS snapshots.


## Object Storage with Amazon S3

- **What Is Amazon S3?**
  - Unlike Amazon EBS, Amazon S3 is a standalone storage solution that isn’t tied to compute. 
  - Amazon S3 is an object storage service. 

- **Understand Amazon S3 Concepts**
  - In Amazon S3, you have to store your objects in containers called *buckets*. 
  - Create bucket : Choose Region / bucket name
  -  Once you choose a name, that name is yours and cannot be claimed by anyone else unless you delete that bucket, which then releases the name for others to use.

- **Choose the Right Connectivity Option for Your Resources**
  - Everything in Amazon S3 is private by default. 

- **Understand S3 Bucket Policies**
  - S3 bucket policies are similar to IAM policies, in that they are both defined using the same policy language in a JSON format. 
  -  The difference is IAM policies are attached to users, groups, and roles, whereas S3 bucket policies are only attached to buckets. S3 bucket policies specify what actions are allowed or denied on the bucket.

- **S3 bucket policy**

  ```json
  {
      "Version":"2012-10-17",
          "Statement":[{
              "Sid":"PublicRead",
              "Effect":"Allow",
              "Principal": "*",
              "Action":["s3:GetObject"],
              "Resource":["arn:aws:s3:::employeebucket/*"]
          }]
  }
  ```
  - S3 Bucket policies can only be placed on buckets, and cannot be used for folders or objects. However, the policy that is placed on the bucket applies to every object in that bucket.

## Reading 3.3 for more information on Amazon S3 Glacier Deep Archive.
> When you upload an object to Amazon S3 and you don’t specify the storage class, you’re uploading it to the default storage class—often referred to as standard storage.  
> There are six S3 storage classes.  


1) **Amazon S3 Standard**: This is considered general purpose storage for cloud applications, dynamic websites, content distribution, mobile and gaming applications, and big data analytics.  
2) **Amazon S3 Intelligent-Tiering**: This tier is useful if your data has unknown or changing access patterns. S3 Intelligent-Tiering stores objects in two tiers, a frequent access tier and an infrequent access tier. Amazon S3 monitors access patterns of your data, and automatically moves your data to the most cost-effective storage tier based on frequency of access.  
3) **Amazon S3 Standard-Infrequent Access (S3 Standard-IA)**: S3 Standard-IA is for data that is accessed less frequently, but requires rapid access when needed. S3 Standard-IA offers the high durability, high throughput, and low latency of S3 Standard, with a low per-GB storage price and per-GB retrieval fee. This storage tier is ideal if you want to store long-term backups, disaster recovery files, and so on.  
4) **Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA)**: Unlike other S3 storage classes which store data in a minimum of three Availability Zones (AZs), S3 One Zone-IA stores data in a single AZ and costs 20% less than S3 Standard-IA. S3 One Zone-IA is ideal for customers who want a lower-cost option for infrequently accessed data but do not require the availability and resilience of S3 Standard or S3 Standard-IA. It’s a good choice for storing secondary backup copies of on-premises data or easily re-creatable data.  
5) **Amazon S3 Glacier**: S3 Glacier is a secure, durable, and low-cost storage class for data archiving. You can reliably store any amount of data at costs that are competitive with or cheaper than on-premises solutions. To keep costs low yet suitable for varying needs, S3 Glacier provides three retrieval options that range from a few minutes to hours.  
6) **Amazon S3 Glacier Deep Archive**: S3 Glacier Deep Archive is Amazon S3’s lowest-cost storage class and supports long-term retention and digital preservation for data that may be accessed once or twice in a year. It is designed for customers—particularly those in highly regulated industries, such as the Financial Services, Healthcare, and Public Sectors—that retain data sets for 7 to 10 years or longer to meet regulatory compliance requirements.  

## Choose the Right Storage Service

- **Amazon EC2 Instance Store**
  - Instance store is ephemeral block storage. 
  - a built-in drive for your EC2 instance.
  - Instance store is generally well-suited for temporary storage of information that is constantly changing, such as buffers, caches, and scratch data. It is not meant for data that is persistent or long-lasting.

- **Amazon EBS**
  - Amazon EBS is meant for data that changes frequently and needs to persist through instance stops, terminations, or hardware failures. 
  - It is block storage.
  - You pay for what you provision (you have to provision storage in advance).
  - EBS volumes are replicated across multiple servers in a single Availability Zone.
  - Most EBS volumes can only be attached to a single EC2 instance at a time.

- **Amazon S3**
  - If your data doesn’t change that often, Amazon S3 might be a more cost-effective and scalable storage solution.
  - It is object storage.
  - You pay for what you use (you don’t have to provision storage in advance).
  - Amazon S3 replicates your objects across multiple Availability Zones in a Region.
  - Amazon S3 is not storage attached to compute.
      
- **Amazon Elastic File System (Amazon EFS) and Amazon FSx**
  - So, if you need file storage on AWS, which service should you use?
  - For file storage that can mount on to multiple EC2 instances, you can use Amazon Elastic File System (Amazon EFS) or Amazon FSx. 
  - It is file storage.
  - You pay for what you use (you don’t have to provision storage in advance).
  - Amazon EFS and Amazon FSx can be mounted onto multiple EC2 instances.
  

- [Exercise 5: Create an Amazon S3 Bucket](https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/lab-5-storage.html)

## Explore Databases on AWS

- **What Is a Relational Database?**

> 관계형 데이터베이스는 현재 가장 많이 사용되고 있는 데이터베이스의 한 종류  
> 관계형 데이터베이스란 2차원 테이블(Table) 형태로 이루어져 있으며, 이 테이블은 키(Key)와 값(Value)의 관계  
> 이처럼 데이터의 종속성을 관계(Relationship)로 표현하는 것이 관계형 데이터베이스의 특징   


  - A relational database organizes data into tables. Data in one table can be linked to data in other tables to create relationships—hence, the relational part of the name.
  - The tables, rows, columns, and relationships between them is referred to as a logical schema. With relational databases, a schema is fixed. 

- **What Is a Relational Database Management System? (RDBMS)**
  - MySQL
  - PostgresQL
  - Oracle
  - SQL server
  - Amazon Aurora

## Amazon Relational Database Service (RDS)

- **What Is Amazon RDS?**
  - Amazon RDS enables you to create and manage relational databases in the cloud without the operational burden of traditional database management. 

## Introduction to Amazon DynamoDB
- **What Is Amazon DynamoDB?**
  - Non Relational Database
  - Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. 

- **Core Components of Amazon DynamoDB**
  - In DynamoDB, tables, items, and attributes are the core components that you work with. 
  - A table is a collection of items, and each item is a collection of attributes.

[Exercise 6: Amazon DynamoDB](https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/lab-6-databases.html)


## Week 3 Assessment and Discussion (6/8)
> [Week3 Quiz](https://learning.edx.org/course/course-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021/block-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021+type@sequential+block@01699057842f469caa028e61bbe4050d/block-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021+type@vertical+block@d760a113854043b69652fa50374a88ef)  


### Question 1 
- Which of the following is a typical use case for Amazon S3?
  - Object storage for media hosting
  - Object storage for a boot drive
  - Block storage for an EC2 instance
  - File storage for multiple EC2 instances
<!--correct
Answer
Correct:Amazon S3 is an object storage service designed for large objects like media files.Because you can store unlimited objects, and each individual object can be up to 5 TBs, S3 is an ideal location to host video, photo, or music uploads. This information is found in the video “Object Storage with Amazon S3”.-->


### Question 2
- Which of the following services is recommended if you need a storage layer for a high-transaction relational database on an EC2 instance?
  - Amazon EC2 Instance Store
  - Amazon EBS
  - Amazon S3
  - Amazon EFS
<!--correct
Answer
Correct:Amazon EBS would be ideal for a high-transaction database storage layer. Amazon S3 is not ideal, as it’s considered WORM (write once, read many) storage. EC2 Instance Store is ephemeral, and persistence is needed for databases.EFS is for ideal when you have multiple servers that need access to the same set of files. Check out the video “Amazon EC2 Instance Storage and Amazon Elastic Block Store” for more information.-->

### Question 3
- True or false: Amazon EBS volumes are considered ephemeral storage.
  - True
  - False
<!--correct
Answer
Correct:Amazon EC2 Instance Store is considered ephemeral storage. EBS is considered persistent storage. This content is covered inthe video “Amazon EC2 Instance Storage and Amazon Elastic Block Store”.-->

### Question 4 (X) 
- You are an employee at a healthcare facility tasked with storing 7 years of patient information that is rarely accessed. Your boss wants you to consider one of the Amazon S3 storage tiers to store this information. Which storage tier should you suggest?
  - S3 Standard
  - S3 Glacier Deep Archive
  - S3 Standard-Infrequent Access
  - S3 Intelligent-Tiering
<!--incorrect
Answer
Incorrect:Amazon Glacier Deep Archiveis Amazon S3’s lowest-cost storage class and supports long-term retention and digital preservation for data that may be accessed once or twice in a year. It is designed for customers—particularly those in highly regulated industries, such as the Financial Services, Healthcare, and Public Sectors—that retain data sets for 7 to 10 years or longer to meet regulatory compliance requirements. Check out Reading 3.3 for more information on Amazon S3 Glacier Deep Archive.-->

### Question 5
- True or false: Bucket names have to be unique across all AWS accounts.
  - True
  - False
<!--correct
Answer
Correct:Amazon S3 is a regional service. However, the namespace is shared by all AWS accounts, so the bucket name must be a globally unique. This information is covered in the video “Object Storage with Amazon S3”.-->


### Question 6  
- True or false: A Multi-AZ deployment is beneficial when you want to increase the availability of your database.
  - True
  - False
<!--correct
Answer
Correct:When you use Amazon RDS, it places the DB instance into a subnet which is bound by one AZ. For high availability reasons, you should use a Multi-AZ deployment in case one AZ is temporarily unavailable. This information can be found in the Introduction to Amazon Relational Database Service video and corresponding readings.-->

### Question 7 
- Consider this scenario: You are an AWS Architect choosing a database for a dataset that has variation within the data, as in not every piece of data share all the same attributes. What database should you choose for this solution?
  - Amazon Relational Database Service
  - Amazon Neptune
  - Amazon DynamoDB
  - Amazon QLDB
<!--correct
Answer
Correct:Amazon DynamoDB allows for a flexible schema, so each item can have variation in the attributes outside of the primary and secondary key. This information can be found in the Introduction to Amazon DynamoDB video and corresponding reading.-->

### Question 8 (X)
- When using Amazon Relational Database Service you are responsible for what task of running and operating the database?
  - Optimizing the database
  - Provisioning and managing the underlying infrastructure
  - Installing the RDBMS onto the DB instance
  - Installing patches to the OS for the DB instance
<!--incorrect
Answer
Incorrect:When using Amazon RDS, you are no longer responsible for the underlying environment the database runs on, instead you can focus on optimizing the database. This is because Amazon RDS has components that are managed by AWS. This information can be found in the Explore Databases on AWS Video.-->


