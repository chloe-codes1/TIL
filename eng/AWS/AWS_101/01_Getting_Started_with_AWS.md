# Intro to AWS

<br>

#### Contents for Today

- Cloud Computing
- AWS 
- Main services
- Security
- Architecture

<br>

####  Useful Informations

1. On-premise

   : A model where users directly manage Infrastructure, Platform, and Applications

2. Saas (Software as a Service)

   : The most common type of Cloud Service where the service provider offers everything from Infrastructure to Software, providing services up to the Application Level

<br>

<br>

## Intro to AWS Cloud

<br>

### What is Cloud Computing?

- A type of `Internet based computing` that processes information on other computers connected to the Internet rather than on your own computer
- Served when shared computer manage resources & data are requested 
- A model that enables ubiquitous, convenient, on-demand network access to a shared pool of `configurable computer resources` (e.g., networks, servers, storage, applications, and services)
- Can be rapidly provisioned and released with minimal management effort
- `Cloud computing` and `Storage Solutions` provide users and businesses with various capabilities to store and process data in privately-owned data centers or third-party data centers
- Relies on sharing of resources to achieve coherence and economies of scale, similar to a utility over an electricity network

<br>

![image-20200226112333821](../../../kor/images/image-20200226112333821.png)

<br/>

<br>

### Cloud Computing Services

<br>

#### 1. On-premise (Traditional IT)

- Users directly manage Infrastructure, Platform, and Applications
- Large companies build their own **IDC (Internet Data Center)**, while typical cases involve renting space in an IDC, installing physical servers, and managing all Hardware, Operating System, and Server Applications

<br>

#### 2. IaaS (Infrastructure as a Service)

- `AWS EC2` is representative
- A service that supports **IT Infrastructure** such as Virtual Servers, Data Storage & Hosting Computers, Networks - a Cloud Model that provides Hardware as a Service
- Manage OS & Applications

<br>

#### 3. PaaS (Platform as a Service)

- `AWS Elastic Beanstalk` is representative

  - Using Elastic Beanstalk, you can **quickly deploy, operate, and manage** applications in the AWS Cloud without worrying about the **infrastructure** that runs the application!

- Serves Fundamental IaaS + Development Tools & Functions + Deployment

  -> They serve pretty much everything you need when you develop & deploy

- Developers only have to write `logic` to connect their application & served services 

<br>

#### 4. Saas (Software as a Service)

- `Google Apps`, `Office 365` are representative

- The most common type of Cloud Service where the service provider offers everything from Infrastructure to Software

  -> Serves **application level service**

- Provided directly to actual users rather than developers

<br>

<br>

## AWS (Amazon Web Service) Cloud Computing

### AWS

> Provides various Infrastructure and Application Services that allow you to run almost all physical computing resources through the Cloud, from Web and mobile Apps, Big data projects, to Social games

- The most secure and reliable Cloud Service
- Provides easy and fast **scalability**
- Provides a platform that can **reduce costs** by paying only for **what you use** without upfront costs or long-term commitments

<br>

### Amazon Cloud Service

1. Provides various Application Services including Computing, Storage, Database, Networking, Analytics, Machine Learning, AI, IoT, Security, Application Development, Deploy & Maintenance

2. Not only provides the most **comprehensive range of services**, but also supports the **deepest functionality** in those services

3. `Amazon Elastic Container Service(ECS)`, `Amazon Elastic Container Service for Kubernetes(EKS)` and `AWS Fargate` gives you the most effective way to execute container

4. the most safe and flexible cloud computing environment 

5. AWS's core infrastructure is designed to meet the **security requirements** of military, international banks, and other security-critical organizations

6. Each region is built & operated using the same secure hardware/software

   - All AWS customers can benefit from the only commercial cloud that supports a supply chain associated with **secure** and **proven** service offerings that are safe enough to handle security-critical workloads

   - Supports a deep **cloud security set** including 263 **security**, **compliance** and governance services/main functions

7. Supports 85 **security standards** and **compliance certifications**, and all 116 AWS services that store customer data provide the ability to **encrypt** that data

8. Achieved very rapid innovation in new areas such as `Machine Learning`, `AI`, `IoT`, `Serverless Computing`

9. With AWS, you can leverage the latest technologies to innovate, differentiate, and deliver solutions faster

   ex)

   - In 2014, launched AWS Lambda, first introducing the event-driven serverless computing space
   - With AWS Lambda, developers can run code without provisioning or managing servers, without worrying about provisioning, modification, patch or manage of underlying servers
     - Lambda rocks

<br><br>

<br>

## AWS Main Services

<br>

![Image result for aws main services](https://images.clickittech.com/wp-content/uploads/2018/01/17171820/why-aws-service-catalog.jpg)

<br>

### AWS Security

: Security, identity and compliance products

- AWS's highest priority == `Cloud Security`
- AWS customers can benefit from data center & network architecture built to meet the requirements of the most security-sensitive organizations

<br>

### AWS Architecture

- ex) AWS Industrial Predictive Maintenance Machine Learning Model
  - Using AWS IoT SiteWise & AWS IoT Analytics with Amazon SNS anomaly detection notifications to create Predictive Maintenance ML models

#### AWS Reference Model Architecture 

1. Web Application Hosting

   : Build highly scalable and reliable web or mobile applications

2. Content & Media Serving

   : Build reliable systems that serve huge amounts of content and media

3. Batch Processing

   : Build auto-scalable batch processing systems like video processing pipelines

4. Fault Tolerance and HA

   : Build systems with high availability that quickly fail over to new instances when failures occur

5. Large-scale Computing

   : Build high-performance computing systems that process Big data

6. Ad Support

   : Build highly scalable online advertising serving solutions

7. DR (Disaster Recovery) for Local Applications

   : Build cost-effective disaster recovery (DR) solutions for on-premise applications 
