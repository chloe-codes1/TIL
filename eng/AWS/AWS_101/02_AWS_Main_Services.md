# AWS Main Services

<br>

#### Today's Contents

- Amazon Elastic Compute Cloud(EC2)
- Amazon Simple Storage Service(S3)
- Amazon Aurora
- Amazon DynamoDB
- Amazon RDS
- AWS Lambda
- Amazon VPC
- Amazon Lightsail
- Amazon SageMaker

<br>

#### Useful Informations

1. Through Amazon EC2's simple **Web service interface**, you can easily obtain and **configure** the required capacity.
2. Amazon Simple Storage Service(S3) is **object storage** built to store/retrieve **any amount of data** from anywhere.

<br>

<br>

## Amazon Elastic Compute Cloud (EC2)

> Cloud's virtual server

<br>

### What is Amazon EC2?

: A web service that provides **secure** and **resizable** computing power in the cloud

- Designed to make web-scale cloud computing easier for developers
- Through Amazon EC2's simple **web service interface**, you can easily obtain and configure the required capacity
  - With EC2, you can create new servers in just minutes and build infrastructure for services!
- Provides comprehensive **control** over **computing resources**, allowing you to run on Amazon's proven computing infrastructure
- Virtual servers are called `Instances`
- Amazon EC2 reduces the time required to obtain and boot new `Server Instances` to just minutes, allowing you to quickly **scale** capacity **up** or **down** as **computing requirements** **change**
  - Can scale from one to thousands of instances
- Available in all public AWS Regions
- You can **create**, **start**, **modify**, **stop**, and **delete** instances as needed
- Provides **tools** that allow developers to build applications that are **resilient** to **failures** and isolated from common **error scenarios**
- You can choose from various cost models (`On-demand`, `Spot`, `Reserved`)

<br>

<br>

### Key Features of Amazon EC2

: Amazon EC2 Instances are configured so users can select the type they want based on **usage purpose** and **payment method**

<br>

#### 1. Amazon EC2 Instance Types

- Instance types are broadly divided into five categories:
  - **General Purpose (M Series)**
  - **Compute Optimized (C Series)**
  - **Storage Optimized (I Series, D Series)**
  - **GPU Optimized (G Series)**
  - **Memory Optimized (R Series)**

- Instance types allow you to use **optimized computing power** by selecting the instance type according to the **purpose** of using EC2!

<br>

![Amazon EC2 인스턴스 유형 및 표기법 인스턴스 패밀리 인스턴스 세대 인스턴스 크기 c4.large 애플리케이션 요구에 따라 인스턴스 패밀리, 세대 및 크기 결정: ① 인스턴스 패밀리 • M, T, C, X, R,...](https://image.slidesharecdn.com/amazonec2deepdive-170830022453/95/amazon-ec2-deep-dive-aws-8-7-638.jpg?cb=1504060127)

- As shown in the figure above, depending on the EC2 Instance and type size you choose, you can select the following as needed:
  - **Instance Type**
  - **Number of CPU Cores**
  - **Memory Capacity**
  - **Network Interface Speed**

<br>

#### 2. Amazon EC2 Instance Purchase Options

: Amazon EC2 provides the following purchase options to **optimize costs** according to user requirements

| Category                         | Type                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| **On-Demand Instances**         | - A method of creating and using as needed, paying per-second costs for instances<br>- Suitable for **fluctuating loads**! |
| **Reserved Instances**          | - Pay up to 75% **less** than On-Demand through 1-year or 3-year commitments<br>- Suitable for **confirmed usage**! |
| **Spot Instances**              | - **Auction-style** instances where you **bid** on **costs** for unused EC2 capacity, with instances allocated to users who enter higher prices<br>- Suitable for **time-independent loads**! |
| **Dedicated Instances**         | - Launch instances in customer-dedicated hardware `VPC`<br>- Suitable for **highly sensitive loads**! |

- These EC2 purchase options allow you to select the most appropriate purchase option for your service type
  - **Cost optimization** is possible by selecting the purchase option that fits the purpose of your EC2 service!

<br>

<br>

## Amazon Simple Storage Service (S3)

> Scalable Storage in the Cloud

Object storage built to store/retrieve any amount of data from anywhere

- An `object storage service` that provides industry-leading scalability, data availability, security, and performance
- Customers of any size and industry can use this service to store and protect *any amount of data* for various use cases such as websites, mobile applications, backup & recovery, archive, enterprise applications, IoT devices, and Big data analytics
- Provides easy-to-use management features, allowing you to organize data and implement detailed access control according to specific business, organizational, and compliance requirements
- Designed to provide 99.999999% durability and stores data for millions of applications worldwide

<br><br>

## Amazon Aurora

> Managed High-Performance Relational Database

- MySQL and PostgreSQL compatible relational database built for the Cloud

- Combines the performance and availability of high-performance commercial databases with the simplicity and cost-effectiveness of open source databases

  - High Availability (HA)

    : The ability of information systems such as servers, networks, and programs to operate continuously and normally for extended periods

- Up to 5 times faster than standard MySQL databases and 3 times faster than standard PostgreSQL

- Provides commercial database-level security, performance, availability, and reliability at 1/10 the cost

- All of Amazon Aurora is managed by `Amazon Relational Database Service(RDS)`, which automates time-consuming administrative tasks such as hardware provisioning, database setup, patching, and backup

- A fault-tolerant, self-healing distributed storage system that automatically scales up to 64TB per database instance

  - `Fault tolerance`

    : The ability of a computer or operating system to prepare for unexpected situations such as power shortages or hardware failures so that data in running systems is not lost or ongoing work is not damaged

- Outstanding performance and availability

  - Up to 15 low-latency read-only replicas
  - Point-in-time recovery
  - Continuous backup to Amazon S3

<br>

<br>

## Amazon DynamoDB

> Managed NoSQL Database

- Fast and flexible NoSQL database service at any scale

- A key-value and document database that delivers single-digit millisecond performance at any scale

- A fully managed, multi-region, multi-master database that provides security, backup, recovery, and in-memory caching capabilities by default for internet-scale applications

  - `In-memory Database`

    : A DBMS that is installed and operated in the main memory of data storage

    -> Faster than disk-optimized databases because disk access is slower than memory access

    -> Internal optimization algorithms are simpler, executing fewer CPU instructions

    -> Accessing data in memory reduces search time when querying data and provides faster and more predictable performance than disks

- Can handle more than 10 trillion requests per day

- Supports more than 20 million peak requests per second

<br><br>

## Amazon RDS

> RDBMS for MySQL, PostgreSQL, Oracle, SQL Server, and MariaDB

- Easy to set up, operate, and scale RDBMS in the cloud
- Provides cost-effective and resizable capacity while automating time-consuming tasks such as hardware provisioning, database setup, patching, and backup
- Allows users to focus on applications and receive fast performance, high availability, security, and compatibility
- Available in multiple database instance types (memory, performance, I/O optimization, etc.) and you can choose from 6 database engines including Amazon Aurora, PostgreSQL, MariaDB, Oracle Database, and SQL Server
- Use AWS Database Migration Service to easily migrate or replicate existing databases to Amazon RDS

<br><br>

## AWS Lambda

> Serverless computing system

- Execute codes without worrying about server
  - you don't have to provision or manage server
- Only pay for the used computing time
- Execute all kinds of applications or back-end server without management
- All you have to do is upload your codes and Lambda will take care of everything with the high availability
- You can make it automatically triggered by other AWS services or trigger it manually from your web/mobile application

<br>

<br> 
