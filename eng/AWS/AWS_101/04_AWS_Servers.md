# AWS Servers

<br>

#### Contents

- Server Architecture
- AWS Server service
- Amazon EC2 (Elastic Compute Cloud)

<br>

#### Useful Information

1. Availability Zones (AZ) in AWS Server services consist of one or more data centers and are designed as independent failure domains
2. AWS regions include two or more AZs

<br>

<br>

## Server Architecture

<br>

### Web Server Architecture

![aws web server architecture 이미지 검색결과](https://tech.cloud.nongshim.co.kr/wp-content/uploads/2018/10/2-1-1-1024x688.png)

<br>

<br>

## AWS Server Service

<br>

### Availability Zone(AZ)

- AWS `data centers` are organized within `Availability Zones (AZ)`
- Each availability zone consists of one or more data centers
- A single data center cannot be included in two availability zones
- Each availability zone is designed as an independent failure domain
- Availability zones are physically isolated within a typical metropolitan region, and power is supplied through independent utilities' different grids in addition to separate uninterruptible power supplies and on-site backup generation facilities, reducing single points of failure
- Users must select the availability zone where their systems will reside
- Systems can be extended across multiple availability zones, and should be designed to overcome temporary or long-term availability zone failures in case of disasters
- Distributing applications across multiple availability zones maintains resilience in most failure situations including natural disasters or system failures

<br>

### Region

- Availability Zones are further grouped into regions
- Each AWS Region includes *two or more Availability Zones*
- When data is stored in a specific region, the data is replicated only within that region
- AWS does not move data *outside the region where users store data*
  -> If business needs require this, replicating data across multiple regions is the user's responsibility
- AWS provides information about the countries and regions where each region is located, and it is the user's responsibility to select the region to store data according to compliance and network latency requirements
- All communication between regions occurs through `Public Internet Infrastructure`, so it is necessary to use **encryption methods** to protect sensitive data
- Available AWS products and services vary by region, so users need to carefully check the services available in their region

<br>

### Edge Location

- A collection of cache servers for Amazon's CDN (Content Delivery Network) service, CloudFront
  - `CDN`
    - A service that copies contents (HTML, images, videos, other files) to cache servers located around the world so users can receive them quickly from servers physically close to them
- Since downloading from physically closer servers is much faster, CDN services build cache servers in major cities worldwide

<br>

### Virtual Private Cloud (VPC)

- *A virtual network dedicated to your AWS account*
- Logically isolated from other virtual networks in the AWS cloud
- A `cloud` and `network` environment where you can run AWS resources such as Amazon EC2 instances in your VPC
- A place to launch various resources, designed to provide excellent control over your environment and resource isolation
- Each VPC exists within a region, and resources within the VPC cannot exist outside that region
  - However, resources in different availability zones within the same region can exist in the same VPC
- You can connect privately to AWS services through VPC endpoints without using internet gateways, NAT, or firewall proxies
- Available services include S3, DynamoDB, Kinesis Streams, Service Catalog, EC2 Systems Manager (SSM), Elastic Load Balancing (ELB) API, Amazon Elastic Compute Cloud (EC2) API, and SNS!

<br>

### Subnet

- A range of IP addresses in your VPC
- You can launch AWS resources into a specified subnet
- Use a `public subnet` for resources that must be connected to the internet
- Use a `private subnet` for resources that won't be connected to the internet
  - For example, use private subnets for instances that you want to prevent direct access from the internet using Network Address Translation (NAT)
  - Instances in private subnets can access the internet through a NAT gateway in the public subnet by routing traffic outbound without exposing their private IP addresses

<br>

### Elastic Compute Cloud (EC2)

- The core of AWS services
- Provides scalable computing in the AWS cloud
- Using EC2 eliminates the need for hardware upfront investment, enabling faster application development and deployment
- Through EC2, you can build as many virtual servers as you want and manage security, networking configuration, and storage
- EC2 can scale up or down according to requirements or sudden traffic increases, reducing the need for traffic prediction
- Features provided by EC2:
  1. `Virtual Computing Environment`
     - Create instances suitable for purpose according to computer and memory capabilities
  2. `Amazon Machine Image (AMI)`: Templates provided with OS and various software properly configured for servers, enabling instance creation
     - Provides various configurations of CPU, memory, storage, and networking capacity for instances
  3. `Instance Store Volume`
     - Storage volume for saving temporary data - instance will be deleted when you shut down
  4. `Amazon Elastic Block Store (Amazon EBS)`
     - Ability to store data in permanent storage volumes using EBS volumes
  5. `Security Group`
     - Provides firewall functionality to specify protocols, ports, and source IP ranges that can connect to instances
  6. `Elastic IP (EIP)`
     - Fixed IPv4 addresses for dynamic cloud computing
  7. `Tag`
     - Metadata that users can create and assign to Amazon EC2 resources
  8. `Virtual Private Clouds (VPC)`
     - Virtual networks that are logically isolated in the AWS cloud but can easily connect to your network whenever desired

<br>

### Relational Database Service (RDS)

- A web service that supports easier setup, operation, and scaling of RDBMS in the cloud
  - Provides economical and resizable capacity for industry-standard relational databases and manages common database administration tasks
- With Amazon RDS, CPU, memory, storage, and IOPS (Input/Output Operations Per Second) are separately partitioned, so they can be scaled independently
- When you need more CPU, less IOPS, or more storage, allocation is easily possible
- RDS manages backup, software patches, automatic error detection & recovery
- You can use familiar database products including MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL Server, and MySQL-compatible `Amazon Aurora DB engine`
  - In addition to package security, you can control which users can access RDS databases by defining users and permissions using AWS Identity and Access Management (IAM)

<br>

### Elastic Load Balancing (ELB)

- Automatically distributes incoming application traffic across multiple targets such as Amazon EC2 instances, containers, and IP addresses
- Handles various application loads in single or multiple AZs (Availability Zones), improving fault tolerance and availability
- **3 Load Balancers in ELB**
  - ELB has three types of load balancers, all providing high availability, automatic scaling, and robust security features necessary for application fault tolerance
    1. `Application Load Balancer`
       - Operates at Layer 7 of the OSI 7-layer model
       - Routes traffic to targets within VPC based on request content
       - Load balances Layer 7 HTTP/HTTPS applications and improves application security by ensuring SSL/TLS ciphers and protocols are used
    2. `Network Load Balancer`
       - Operates at Layer 4 of the OSI 7-layer model
       - Routes connections to targets within VPC based on IP protocol data
       - Suitable for TCP traffic load balancing and handles sudden, highly volatile traffic using one static IP address per AZ
    3. `Classic Load Balancer` (General purpose)
       - Provides basic load balancing across multiple Amazon EC2 instances and operates at both Layer 4 and Layer 7
       - An earlier service than the previous two balancers, designed for applications built within the EC2-Classic network, but can also be used in VPC and is relatively simple to configure

<br><br>

### EC2 Storage

<br>

![Storage options for Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/architecture_storage.png)

<br>

#### 1. Amazon EBS (Elastic Block Storage)

> Persistent block-level storage volumes for EC2 instances with high reliability and low latency

- Charged based on size/usage duration
- Provides durable block-level storage volumes that can be attached to running instances
- Amazon EBS can be used as the primary storage device for data that requires frequent granular updates
- Recommended storage option when running databases within instances

<br>

#### 2. Amazon EC2 Instance Store

> Temporary block-level storage for your instance 
