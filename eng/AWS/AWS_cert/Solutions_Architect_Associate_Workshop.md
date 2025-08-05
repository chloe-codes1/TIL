# AWS Solutions Architect - Associate Prep Workshop

<br>

#### Question Distribution

1. Designing resilient architectures
2. Defining solutions that meet performance criteria
3. Specifying secure applications and architectures
4. Designing cost-optimized architectures
5. Defining operationally excellent architectures

<br>

<br>

## Overview

<br>

### EC2 Instance Store

- Temporary supported volume
- Only specific EC2 instances
- Fixed capacity
- Disk type and capacity determined by EC2 instance type
- Application-level durability
- Fast I/O

<br>

### Elastic Block Store (EBS)

- Various types
- Encryption
- Snapshots
- Provisioned capacity
- Independent lifecycle from EC2 instances
- Multiple volumes can be striped to create large volumes

<br>

![image-20200309134828549](../../../kor/images/image-20200309134828549.png)

> Answer: B

<br><br>

### Amazon S3

- Object Storage
- Consistency
- Storage classes and durability - Standard, Standard-IA
- Encryption
  - Data at rest
  - Data in transit
- Versioning
- Access control
- Multi-part upload
- Internet / API access available
- Virtually unlimited capacity
- Regional availability
- Exceptional durability - 99.999999999% (nine elevens)

<br>

<br>

### Amazon Glacier

- Data backup and archive storage
- Retrieval
- Encryption
- Regional availability

<br><br>

#### Decoupling from Component State

![image-20200309135329574](../../../kor/images/image-20200309135329574.png)

- Load Balancer or SQS improves message delivery rate

<br>

<br>

#### Decoupling for Scalability

![image-20200309135522472](../../../kor/images/image-20200309135522472.png)

<br>

<br>

#### Decoupling from Component ID

![image-20200309135708110](../../../kor/images/image-20200309135708110.png)

<br><br>

![image-20200309135953183](../../../kor/images/image-20200309135953183.png)

> Answer: B, D

<br><br>

### Fault Tolerance

: Everything can fail -> Preparation is needed!

![image-20200309140033872](../../../kor/images/image-20200309140033872.png)

<br>

![image-20200309140344479](../../../kor/images/image-20200309140344479.png)

> Answer: C

- High availability requires multiple availability zones!
  - If single availability zone is mentioned, it's not the answer
- High availability doesn't need SLA (Service Level Agreement)
  - `SLA`: A service-level agreement (SLA) defines the level of service you expect from a vendor

<br>

![image-20200309140439634](../../../kor/images/image-20200309140439634.png)

> Answer: D

- Fault tolerance must have SLA

<br>

<br>

### CloudFormation

- Declarative language for deploying AWS services

![image-20200309140534063](../../../kor/images/image-20200309140534063.png)

<br>

![image-20200309140757315](../../../kor/images/image-20200309140757315.png)

> Answer: B

<br><br>

### AWS Lambda

- Fully managed compute service that runs stateless code (Node.js, Python, etc.) in response to events or time-based intervals
- Can run code without managing infrastructure like Amazon EC2 instances and Auto Scaling groups

<br>

![image-20200309141006364](../../../kor/images/image-20200309141006364.png)

> Answer: C

<br>

![image-20200309141202930](../../../kor/images/image-20200309141202930.png)

> Answer: B

- RTO (Recovery Time Objective): Minimum time for disaster recovery
- RPO (Recovery Point Objective): Target recovery point

<br>

![image-20200309141335170](../../../kor/images/image-20200309141335170.png)

<br><br>

### Designing High-Performance Architecture

1. Design high-performance storage and databases
2. Improve performance by applying caching
3. Design solutions with elasticity and scalability - `Auto Scaling`, `CloudWatch`

<br>

![image-20200309142239841](../../../kor/images/image-20200309142239841.png)

- Hard disks are not just low performance!
  - Optimized for throughput
- If SSD for general purpose => General Purpose
- If need fast per-volume max throughput/random data access => Provisioned IOPS

<br>

<br>

### AWS S3 Bucket

![image-20200309142747237](../../../kor/images/image-20200309142747237.png)

<br>

<br>

### Amazon S3: Billing Model

![image-20200309142831070](../../../kor/images/image-20200309142831070.png)

<br>

<br>

### Amazon S3: Storage Classes

![image-20200309143130329](../../../kor/images/image-20200309143130329.png)

- Data that needs to be stored long-term should be stored in `Infrequent Access`

<br>

#### S3 Lifecycle Policy

: Amazon S3 lifecycle policies allow you to change storage class/delete objects based on period after creation

![image-20200309143358722](../../../kor/images/image-20200309143358722.png)

<br>

![image-20200309143504975](../../../kor/images/image-20200309143504975.png)

> Answer: D

- You can copy to multiple regions using cross-region replication

<br>

![image-20200309143709015](../../../kor/images/image-20200309143709015.png)

> Answer: A, C

<br>

<br>

### When to Use Amazon RDS

![image-20200309143810190](../../../kor/images/image-20200309143810190.png)

<br>

<br>

### RDS Read Replicas

: Replicas for SELECT queries only

![image-20200309144129531](../../../kor/images/image-20200309144129531.png)

<br>

<br>

### DynamoDB: Provisioned Throughput Capacity

> AWS's representative NoSQL

![image-20200309144250727](../../../kor/images/image-20200309144250727.png)

<br>

<br>

### Caching in CloudFront

![image-20200309144742870](../../../kor/images/image-20200309144742870.png)

<br>

<br>

### Comparison of Memcached and Redis

![image-20200309144934818](../../../kor/images/image-20200309144934818.png)

<br>

![image-20200309145317660](../../../kor/images/image-20200309145317660.png)

<br><br>

### AWS CloudFront

![image-20200309145420860](../../../kor/images/image-20200309145420860.png)

<br><br>

### Scalable Design

![image-20200309145459007](../../../kor/images/image-20200309145459007.png)

<br>

<br>

### Auto Scaling

![image-20200309145612245](../../../kor/images/image-20200309145612245.png)

<br>

<br>

#### CloudWatch Alarms that Trigger Auto Scaling

![image-20200309145744500](../../../kor/images/image-20200309145744500.png)

<br>

![image-20200309145821604](../../../kor/images/image-20200309145821604.png)

<br>

![image-20200309145940096](../../../kor/images/image-20200309145940096.png)

<br>

<br>

### Auto Scaling Components

![image-20200309150011191](../../../kor/images/image-20200309150011191.png)

<br><br>

### Traffic Distribution by Elastic Load Balancing (ELB)

<br>

![image-20200309150747880](../../../kor/images/image-20200309150747880.png)

> Answer: C

<br>

![image-20200309151127936](../../../kor/images/image-20200309151127936.png)

> Answer: B, E, F

<br>

![image-20200309151309160](../../../kor/images/image-20200309151309160.png)

> Answer: B, D

<br>

<br>

![image-20200309151343847](../../../kor/images/image-20200309151343847.png)

<br><br>

### AWS IAM

![image-20200309152454364](../../../kor/images/image-20200309152454364.png)

<br>

#### Credentials Used in AWS

![image-20200309152540848](../../../kor/images/image-20200309152540848.png)

<br>

![image-20200309152900595](../../../kor/images/image-20200309152900595.png)

> Answer: A, C, E

<br>

<br>

### Computing/Network Architecture

![image-20200309152949240](../../../kor/images/image-20200309152949240.png)

<br>

#### Virtual Private Cloud (VPC)

![image-20200309153030216](../../../kor/images/image-20200309153030216.png)

<br>

<br>

### How to Use Subnets

![image-20200309153120772](../../../kor/images/image-20200309153120772.png)

<br>

<br>

### Comparison of Security Groups and Network ACLs

![image-20200309153402116](../../../kor/images/image-20200309153402116.png)

<br><br>

### Security Groups

: Use security groups to control traffic sent to and from resources

![image-20200309153602501](../../../kor/images/image-20200309153602501.png)

<br>

<br>

### VPC Connections

![image-20200309153745540](../../../kor/images/image-20200309153745540.png)

<br><br>

### Outbound Traffic for Private Instances

<br>

ex 1)

![image-20200309153856056](../../../kor/images/image-20200309153856056.png)

<br>

ex 2)

![image-20200309153943668](../../../kor/images/image-20200309153943668.png)

- NAT Gateway is better for performance scalability

<br>

![image-20200309154239509](../../../kor/images/image-20200309154239509.png)

> Answer: A, C, E

- Option E is optional because Network ACLs always allow inbound access on port 80 unless separately modified...
  - But it's not wrong, so it's an answer!

<br>

<br>

### Data at Rest

> Data stored in S3 is private by default and requires AWS credentials to access

![image-20200309154502649](../../../kor/images/image-20200309154502649.png)

![image-20200309154523626](../../../kor/images/image-20200309154523626.png)

<br><br>

### Key Management

![image-20200309154613320](../../../kor/images/image-20200309154613320.png)

<br>

![image-20200309154826811](../../../kor/images/image-20200309154826811.png)

<br>

![image-20200309155010053](../../../kor/images/image-20200309155010053.png)

> Answer: B, D, E

<br>

![image-20200309155222445](../../../kor/images/image-20200309155222445.png)

> Answer: B

<br>

<br>

![image-20200309155306646](../../../kor/images/image-20200309155306646.png)

- Root user is the last resort
  - Creating access keys and security keys as root user is absolutely forbidden!
- Having applications perform role-based permissions through roles is good for security

<br>

<br>

### Amazon EC2 Pricing

![image-20200309160427703](../../../kor/images/image-20200309160427703.png)

- Elastic IP addresses
  : No cost when in use, but costs are incurred when holding onto IP addresses without using them
  - About $3 per IP address per month

<br>

#### EC2 Pricing Factors

- Instance family
- Tenancy
- Pricing options

<br>

#### EC2: Ways to Save Costs

![image-20200309160800242](../../../kor/images/image-20200309160800242.png)

<br>

![image-20200309161137491](../../../kor/images/image-20200309161137491.png)

<br>

<br>

### Amazon EBS Pricing

![image-20200309161333929](../../../kor/images/image-20200309161333929.png)

<br>

![image-20200309161511103](../../../kor/images/image-20200309161511103.png)

> Answer: A

<br>

<br>

![image-20200309161549562](../../../kor/images/image-20200309161549562.png)

<br>

<br>

### Caching Through CloudFront

![image-20200309161734120](../../../kor/images/image-20200309161734120.png)

<br>

<br>

![image-20200309161805190](../../../kor/images/image-20200309161805190.png)

<br><br>

### Defining Operationally Excellent Architecture

<br>

![image-20200309162004529](../../../kor/images/image-20200309162004529.png)

<br>

<br>

### AWS Services Supporting Operational Excellence

![image-20200309162236340](../../../kor/images/image-20200309162236340.png)

<br>

- `AWS CloudTrail`
  : Records who issued what commands when at the AWS API level

<br>

![image-20200309162620668](../../../kor/images/image-20200309162620668.png)

> Answer: C

<br>

![image-20200309162909909](../../../kor/images/image-20200309162909909.png)

> Answer: B

<br>

<br>

![image-20200309162947164](../../../kor/images/image-20200309162947164.png)

<br>

<br>

### Summary

![image-20200309163259775](../../../kor/images/image-20200309163259775.png)

<br>

![image-20200309163436032](../../../kor/images/image-20200309163436032.png)

<br>

<br>

<br>

### Q&A

Question:
So in the exam, should I assume that users preserve EBS volumes by default?

Answer:
If there's a statement that "EBS volumes are deleted when EC2 terminates", it would be false. More precisely, currently when creating EC2 and allocating EBS, the root volume is set to be deleted by default, while volumes other than the root volume are set not to be deleted by default (you can specify this directly in this process).

<br>

Question:
What is MFA?

Answer:
It refers to multi-factor authentication. For example, when logging in, you use additional authentication like OTP in addition to passwords. AWS also enables MFA for double security. You can use soft tokens like Authy or physical tokens like Yubico.

<br>

Question:
When is it appropriate to use NAT instance? Compared to NAT Gateway?

Answer:
NAT Gateway has limitations such as not providing features like port forwarding. When customers need to directly control features that NAT Gateway doesn't provide, there may be a need to directly configure and use NAT instances. Or it could be used to configure custom security elements. NAT Gateway is a managed service provided by AWS with built-in scalability and durability, making it easy to configure and use.

<br>

Question:
Are EC2 instance storage and EBS different?

Answer:
Yes, instance storage is storage built into the host with volatile characteristics. Instance storage is provided or not provided depending on the instance type. The provided capacity is also determined by the instance type. Volatile means that data is not preserved when the instance is stopped and restarted. Despite this characteristic, it has the advantage of superior performance compared to EBS which is mounted and used through the network. In contrast, EBS can store data permanently. 
