# AWS HA Load Balancing

<br>

#### Contents

- Amazon Elastic Load Balancing
- Amazon Auto Scaling
- Building ELB and Auto Scaling

<br>

#### Useful Informations

1. Amazon Elastic Load Balancing ensures scalability, performance, and security to provide fault tolerance for applications

   - ELB can handle the load of various applications in a single availability zone or across multiple availability zones

2. ELB allows you to choose the appropriate Load Balancer based on your application requirements

   - If flexible application management is needed, it is recommended to use `Application Load Balancer`
   - If the application requires excellent performance and static IP, it is recommended to use `Network Load Balancer`
   - If the existing application is built within the EC2-Classic Network, `Classic Load Balancer` must be used

<br>

<br>

## Amazon Elastic Load Balancing

> Ensure scalability, performance, and security to provide fault tolerance for applications

<br>

- Elastic Load Balancing automatically distributes incoming application traffic across multiple targets such as Amazon EC2 instances, containers, IP addresses, and Lambda functions
- ELB can handle various application loads in a single availability zone or across multiple availability zones
- All three Load Balancers provided by ELB are equipped with **High Availability (HA)**, **automatic scaling**, and **robust security** required for application `fault tolerance`

<br>

### Amazon Elastic Load Balancing Use Cases

<br>

#### 1. Improving Application Fault Tolerance

- ELB provides application fault tolerance by automatically distributing traffic across targets (Amazon EC2 instances, containers, IP addresses, Lambda functions) and multiple availability zones while ensuring only healthy targets receive traffic
- If all targets in a single availability zone are unhealthy, ELB routes traffic to healthy targets in other availability zones
- When targets return to a healthy state, load balancing automatically resumes to the original targets

<br>

#### 2. Automatic Load Balancing for Containerized Applications

- With Elastic Load Balancing's enhanced container support, load balancing is possible across multiple ports on the same Amazon EC2 instance
- You can also leverage full integration with `Amazon EC2 Container Service (ECS)`, which provides a fully managed container offering
- Simply register the service with the Load Balancer, and ECS transparently manages the registration and deregistration of `Docker Containers`
- The Load Balancer automatically detects ports and dynamically reconfigures itself

<br>

#### 3. Automatic Application Scaling

- Elastic Load Balancing provides confidence that applications can scale up and down to meet customer demand
- The ability to trigger `Auto Scaling` of Amazon EC2 instances when the latency of one instance exceeds a predefined threshold ensures that the application is always ready to handle the next customer request

<br>

#### 4. Using Elastic Load Balancing in Amazon Virtual Private Cloud (Amazon VPC)

- With Elastic Load Balancing, you can easily create an internet-facing entry point to a VPC or **route request traffic** between application tiers within the VPC
- You can assign **security groups** to the Load Balancer to control which ports are open to which allowed source lists
- Since Elastic Load Balancing integrates with VPC, all existing Network `ACLs (Access Control Lists)` and `routing tables` continue to provide additional network controls
- When creating a Load Balancer in a VPC, you can specify whether the Load Balancer is **internet-facing** (this is the default) or **internal**
  - If you choose internal, an internet gateway is not required to connect to the Load Balancer, and the Load Balancer's **private IP address** is used in the Load Balancer's `DNS (Domain Name System) record`

<br>

#### 5. Hybrid Load Balancing with Elastic Load Balancing

- Elastic Load Balancing provides the ability to load balance across both AWS and on-premises resources using the same Load Balancer
- e.g., If you need to distribute application traffic across both AWS and on-premises resources, you can register all resources in the same target group and associate that target group with the Load Balancer
- You can also use DNS-based **weighted load balancing** across AWS and on-premises resources by using two Load Balancers — one in AWS and another for on-premises resources
- You can also leverage `Hybrid Load Balancing` to utilize separate applications, one in a VPC and another in an on-premises location
- You can place VPC targets in one target group and on-premises targets in another target group, then use `content based routing` to route traffic to each target group

<br>

#### 6. Invoking Lambda Functions via HTTP(S)

- Elastic Load Balancing supports invoking `Lambda functions` for serving HTTP(S) requests
  - Users can access `serverless applications` from HTTP clients including web browsers
- You can register Lambda functions as targets and leverage support for Application Load Balancer's content-based routing rules to route requests to different Lambda functions
- You can use `Application Load Balancer` as a **common HTTP endpoint** for applications that use either server or serverless approaches
- You can build entire websites using Lambda functions or combine EC2 instances, containers, on-premises servers, and Lambda functions to create applications

<br><br>

### Amazon Elastic Load Balancing Features

<br>

1. #### High Availability

   : ELB automatically distributes traffic across multiple targets (Amazon EC2 instances, containers, IP addresses) in a single availability zone or across multiple availability zones

2. #### Health Checks

   : ELB can detect unhealthy targets, stop sending traffic to them, and distribute the load to the remaining healthy targets

3. #### Security Features

   - Using Amazon Virtual Private Cloud (VPC), you can create and manage security groups associated with the Load Balancer to provide additional networking and security options
   - You can also create internal Load Balancers without using the internet

4. #### `TLS (Transport Layer Security)` Termination

   : ELB supports integrated certificate management and `SSL (Secure Socket Layer)` and `TLS` decryption, allowing you to flexibly manage SSL settings centrally on the Load Balancer and reduce CPU-intensive tasks for the application

5. #### **Layer 4** or **Layer 7** Load Balancing

   : You can load balance HTTP/HTTPS applications for Layer 7-specific features or use strict Layer 4 balancing for applications utilizing `TCP (Transmission Control Protocol)` or `UDP (User Datagram Protocol)`

6. #### Monitoring

   : ELB provides **Amazon CloudWatch** metrics and request tracing integration to enable real-time monitoring of application performance

<br>

<br>

### ELB Products

> You can choose the appropriate Load Balancer based on application requirements

- #### `Application Load Balancer`

  : When flexible application management is needed

  - Operating at the request level (Layer 7), Application Load Balancer routes traffic to targets such as EC2 instances, containers, IP addresses, and Lambda functions based on the content of the request

  - Ideal for advanced load balancing of HTTP and HTTPS traffic, Application Load Balancer provides advanced request routing capabilities for delivering modern application architectures including **microservices** and **container-based applications**

    - Application Load Balancer supports HTTPS termination between the client and the load balancer
    - SSL certificate management is also provided through predefined security policies from AWS Identity and Access Management (IAM) and AWS Certificate Manager

  - Application Load Balancer simplifies and improves application security by ensuring the latest **SSL/TLS ciphers** and protocols are always used

  - **SNI (Server Name Indication)**

    - SNI is an extension to the TLS protocol where the client indicates the hostname it wants to connect to at the start of the TLS handshake
    - The Load Balancer can present multiple certificates through the same secure listener, enabling a single secure listener to support multiple secure websites
    - Application Load Balancer supports **smart certificate selection algorithm** using SNI
    - When the hostname indicated by the client matches multiple certificates, the Load Balancer determines the *optimal certificate* to use based on multiple factors including the client's capabilities

  - Using IP addresses as targets

    - You can load balance applications hosted on AWS or on-premises by using the IP address of the application backend as a target
      - => You can load balance to application backends hosted on any IP address and interface of an instance
    - Each application hosted on the same instance can have its own associated security group and use the same port
    - You can load balance applications hosted on-premises (via Direct Connect or VPN), in peered VPCs, and in EC2-Classic (using ClassicLink) by using IP addresses as targets
    - The ability to load balance across AWS and on-premises resources helps with migrating to the cloud, cloud bursting, or failing over to the cloud

  - Using Lambda functions as targets

    - You can invoke Lambda functions that handle HTTP requests from Application Load Balancer to provide user access to serverless applications from any HTTP client including web browsers
    - You can register Lambda functions as targets for the Load Balancer and route requests to different Lambda functions through support for content-based routing rules
    - You can use Application Load Balancer as a common HTTP endpoint for applications that use both server and serverless computing

    <br>

- #### `Network Load Balancer`

  : When the application requires excellent performance and static IP

  - Operating at the connection level (Layer 4), Network Load Balancer routes connections to targets within Amazon Virtual Private Cloud (VPC) based on IP protocol data
  - Ideal for load balancing both TCP and UDP traffic, Network Load Balancer can handle millions of requests per second while maintaining **very low latency**
  - Network Load Balancer is *optimized for handling sudden and volatile traffic patterns* while using one static IP address per availability zone
  - Integrates with other AWS services such as `Auto Scaling`, `Amazon EC2 Container Service (ECS)`, `Amazon CloudFormation`, and `AWS Certificate Manager (ACM)`
  - High Availability
    - The Load Balancer monitors the health of registered targets and routes traffic only to healthy targets
  - High Throughput
    - Network Load Balancer is designed to handle increasing traffic and can load balance millions of requests per second
    - It can also handle sudden and volatile traffic patterns
  - Low Latency
  - Source IP Address Preservation
    - Preserves the client-side source IP, allowing backends to see the client's IP address
    - Applications can then use this for additional processing
  - Static IP Support
    - Automatically provides a static IP per availability zone (subnet) that applications can use as the frontend IP for the load balancer
  - Elastic IP Support
    - Provides the option to assign an Elastic IP per availability zone (subnet) to provide your own fixed IP
  - TLS (Transport Layer Security) Offload
    - Supports TLS termination between the client and the Load Balancer
    - Even when TLS is terminated at the Network Load Balancer, the original IP continues to be preserved for the backend application
  - Health Checks
    - Supports health checks for both network and application targets
    - Full visibility into health checks and reasons for failures are provided through 'reason codes' in the Network Load Balancer API and Amazon CloudWatch metrics linked to target health checks for quick diagnostics and robust debugging
  - DNS Failover
    - If there are no healthy registered targets in a Network Load Balancer or the **Network Load Balancer node** in that zone is unhealthy, `Amazon Route 53` sends traffic to Load Balancer nodes in other availability zones
  - Integration with Amazon Route 53
    - If the Network Load Balancer is unresponsive, integration with Route 53 removes unavailable Load Balancer IP addresses from the server and sends traffic to an alternate Load Balancer in another region
  - Integration with AWS services
  - Long-lived TCP connections
    - Network Load Balancer supports long-lived TCP connections suitable for WebSocket-type applications

<br>

- #### `Classic Load Balancer`

  : When the existing application is built within the EC2-Classic Network

  - Classic Load Balancer provides basic load balancing across multiple Amazon EC2 instances and operates at both the request level and connection level
  - For applications built within the EC2-Classic Network
  - When using Virtual Private Cloud (VPC)
    - Layer 7 - Application Load Balancer
    - Layer 4 - Network Load Balancer
  - High Availability
    - Automatically adjusts request handling capacity in response to incoming application traffic
  - Health Checks (Monitoring)
    - Classic Load Balancer can detect the health of Amazon EC2 instances
    - When unhealthy EC2 instances are detected, it no longer routes traffic to those instances and distributes the load across all healthy instances
  - Security Features
    - When using Amazon Virtual Private Cloud (VPC), you can create and manage security groups associated with the Classic Load Balancer to provide additional networking and security options
    - You can create a Classic Load Balancer without a **public IP address** to use as an internal Load Balancer not connected to the internet
  - SSL (Secure Socket Layer) Offload
    - SSL decryption offload
    - Centralized SSL certificate management
    - Backend instance encryption using public key authentication
    - Flexible cipher support allows you to control the ciphers and protocols the load balancer presents to clients
  - Sticky Sessions
    - Supports the ability to pin user sessions to specific EC2 instances using cookies
    - While the user accesses the application, traffic is routed to the same instance
  - IPv6 Support
    - Classic Load Balancer supports both Internet Protocol version 4 and 6 in the EC2-Classic Network
  - Layer 4 & Layer 7 Load Balancing
    - You can load balance HTTP/HTTPS applications and use Layer 7-specific features such as `X-Forwarded` and sticky sessions
    - You can use strict Layer 4 load balancing for applications that use only the TCP protocol
  - Operational Monitoring
  - Logging
    - The access log feature records all requests sent to the load balancer and stores the logs in Amazon S3 for later analysis
    - Logs are useful for diagnosing application failures and analyzing web traffic
    - You can use `AWS CloudTrail` to log Classic Load Balancer API calls for your user account and deliver log files
    - API call records can be used to perform security analysis, resource change tracking, and compliance auditing

<br>

<br>

### ELB Services

> Elastic Load Balancing improves application availability and scalability through the following services

<br>

#### 1. Amazon EC2

: Virtual servers that run applications in the cloud

- You can configure a Load Balancer to route EC2 instance traffic

<br>

#### 2. Amazon EC2 Auto Scaling

: Ensures that you have the desired number of instances running even if an instance fails, and automatically increases or decreases the number of instances when demand changes

- When enabling Auto Scaling together with ELB,
  - Instances launched by Auto Scaling are automatically registered with the load balancer
  - Instances terminated by Auto Scaling are automatically deregistered from the load balancer

<br>

#### 3. AWS Certificate Manager

: When creating an HTTP listener, you can specify a certificate provided by ACM

- The Load Balancer uses the certificate to terminate connections and decrypt client requests

<br>

#### 4. Amazon CloudWatch

: Enables you to monitor the Load Balancer and take action as needed

<br>

#### 5. Amazon EC2

- You can run, stop, and manage `Docker containers` on EC2 instance clusters
- You can configure a Load Balancer to route traffic to containers

<br>

#### 6. Route 53

- Converts **domain names** (e.g., <www.example.com) into> numeric IP addresses (e.g., 192.0.2.1) that computers use to connect to each other, routing visitors to websites reliably and cost-effectively
- AWS assigns URLs to user's AWS resources such as load balancers

<br>

#### 7. AWS WAF

: You can use `AWS WAF` together with Application Load Balancer to allow or block requests based on rules in the `Web ACL (Access Control List)`

<br><br>

## Amazon Auto Scaling

- Amazon EC2 Auto Scaling allows you to ensure that you have the exact number of Amazon EC2 instances needed to handle your application's load
- You create a collection of EC2 instances called an `Auto Scaling Group`
- You can specify the minimum and maximum number of instances for each Auto Scaling Group
- If you specify the desired capacity, Amazon EC2 Auto Scaling ensures that the group always has that many instances after the group is created
- If you specify scaling policies, Amazon EC2 Auto Scaling can launch or terminate instances as application demand increases or decreases

<br>

### Amazon Auto Scaling Core Components

<br>

#### 1. Group

- EC2 instances are organized into groups so they can be treated as a logical unit for scaling and management purposes
- When creating a group, you can specify the minimum and maximum number of instances and the desired number of instances

<br>

#### 2. Configuration and Template

- Groups use a launch template or launch configuration as a configuration template for EC2 instances
- You can specify information such as the AMI (Amazon Machine Image) ID, instance type, key pair, security group, and block device mapping for instances

<br>

#### 3. Scaling Options

- e.g., You can configure the group to scale based on the occurrence of specified conditions (dynamic scaling) or on a schedule

 <br><br>

### Building ELB and Auto Scaling

<br>

![Image result for elb autoscaling](https://jayendrapatil.com/wp-content/uploads/2016/06/Screen-Shot-2016-06-07-at-4.13.10-PM.png)

<br>

1. Build VPC
2. Create ELB Target Group
3. Create Auto Scaling Launch Configuration
4. Create Auto Scaling Group
5. Create ELB

<br>

<br>

<br>

#### Summary

: The three load balancers provided by Amazon ELB (Elastic Load Balancing) — `Application Load Balancer`, `Network Load Balancer`, and `Classic Load Balancer` — are all equipped with **high availability**, **automatic scaling**, and **robust security** required for application fault tolerance.
