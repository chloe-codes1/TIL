# VPC Endpoints

> A deep dive into VPC Endpoints - Practical ver.

<br>

<br>

### Before Getting Started

#### What are Scopes?

- `Global Scope`
  - Literally a global scope
  - e.g.)
    - IAM
- `AZ Scope`
  - Resources that consume your VPC's IPs when created
  - e.g.)
    - ENI
    - ELB
    - ElastiCache
- `Region Scope`
  - Resources whose scope does not consume your VPC's IPs when created
    - Fully managed services
  - They communicate over the **Internet**
    - Why?
      - Because they're outside your VPC!
    - Therefore, you need to consider **outbound traffic**, **security/network configuration**, etc.
      - The service used for this is `VPC Endpoints`!!
  - e.g.)
    - SQS
    - Kinesis
    - S3
      - Shown as **Global** in the AWS Console
        - S3 has **triple replication** by default
          - This means that even when the Seoul Region only had two AZs (a and c zones), there was a **hidden AZ**!
          - That's how S3 could provide its triple-replication service

<br>

<br>

### What are VPC Endpoints?

- A service that creates a sort of pathway as if communicating within the VPC
  - If you create such a pathway, even an EC2 without external communication configuration can go out through the Endpoint!

<br>

<br>

### Endpoint Types

#### 1. Gateway Type

- Routes traffic to another destination
- Consumes your VPC IPs, but
  - Does not control access through firewalls like SGs
- Rules are only applied by these two:
  1. `Routing Table`
  2. `ACL`
     - ACL is not dependent on Subnets!
       - In other words, it is not affected by AZ
     - As long as the requester's destination matches, it sends traffic to the corresponding Endpoint
- Each VPC requires one per resource (e.g., S3)
- e.g.)
  - S3
  - DynamoDB
- **Advantages of Gateway Type**
  - Cost
    - It's economical because `internal communication` costs apply
  - Security
    - Since it's `internal communication`, there are fewer considerations compared to external communication

<br>

#### 2. Interface Type

- Interface refers to `Network Interface`
  - Think of it as a **Network Interface Card**
- Consumes your VPC's IPs
  - Access can be controlled through firewalls like SGs
    - `NAT Gateway` is also an Interface Type!
- Interface Type does not configure Routing Tables
