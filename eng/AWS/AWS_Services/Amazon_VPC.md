# Amazon VPC

> AWS VPC that you must know before moving forward!
>
> Reference: [Inflearn] DevOps : Infrastructure as Code with Terraform and AWS course by Song Ju-young, [medium.com/harrythegreat](https://medium.com/harrythegreat/aws-%EA%B0%80%EC%9E%A5%EC%89%BD%EA%B2%8C-vpc-%EA%B0%9C%EB%85%90%EC%9E%A1%EA%B8%B0-71eef95a7098)

<br>

<br>

## What is Amazon VPC?

- A **private** network service provided by Amazon
  - A service that creates a dedicated network for AWS accounts
- When VPC is applied:
  - You can configure networks for each VPC
  - You can set different network configurations for each VPC
- Each VPC operates as a completely independent network

<br>

<br>

## Core Components of VPC

<br>

### Virtual Private Cloud (VPC)

![image-20201011020530093](../../../kor/images/image-20201011020530093.png)

- A virtual network dedicated to your AWS account
  - To build a VPC, you must configure the IP range according to **private IP ranges** called `RFC1918`
    - **Private IP ranges used in VPC**
      - 10.0.0.0 ~ 10.255.255.255(10/8 prefix)
      - 172.16.0.0 ~ 172.31.255.255(182.16/12 prefix)
      - 192.168.0.0 ~ 192.168.255.255(192.168/16 prefix)
  - Once set, the IP range cannot be modified
  - Each VPC belongs to one Region
  - Since each VPC is completely independent, if you want communication between VPCs, you can consider the `VPC Peering Service`

<br>

### Subnet

> A network group belonging to a specific Availability Zone, an independent network area divided within the VPC

![image-20201011020622952](../../../kor/images/image-20201011020622952.png)

- VPC's IP address range
  - About how far to divide the IP address range within that VPC
    - The process of breaking down VPC into smaller pieces
  - The reason for dividing subnets is to create more network segments
  - Each subnet exists within an Availability Zone (AZ), and you can place resources like `RDS` and `EC2` within the subnet
- Public Subnet vs Private Subnet
  - **Public Subnet**
    - If a machine like EC2 has a `public IP` attached, it can usually be considered an EC2 instance located in a Public subnet
  - **Private Subnet**
    - A subnet that doesn't have a `public IP` but can access the internet through a `NAT Gateway` is called a Private Subnet
      - In other words, subnets connected to the internet are called **Public Subnets**, and subnets not connected to the internet are called **Private Subnets**

<br>

### Routing Table

![image-20201011021121247](../../../kor/images/image-20201011021121247.png)

- A **set of rules** called **routing** used to determine **where to forward** `network traffic`
  - About where **outbound** traffic from a machine (ex. EC2) goes
    - A table that sets rules about whether to go internally or externally
  - When a network request occurs, data first goes to the **router**
    - Network requests operate according to each defined **routing table**
      - In the above figure,
        - **Subnet A routing table** is set to find `172.31.0.0/16`, i.e., network requests with network ranges within the VPC, locally
          - However, it cannot handle traffic going outside
            - This is when Internet Gateway is used

<br>

### Internet Gateway

![image-20201011021532969](../../../kor/images/image-20201011021532969.png)

- A **gateway** that connects to VPC to enable communication between VPC **resources** and the **internet**
  - A service needed to connect to the internet
    - A gateway that connects VPC and the internet
      - In the above figure,
        - Looking at **Subnet B routing table**, it's defined as `0.0.0.0/0`
          - This means to direct all traffic **to IGA (Internet Gateway) A**
            - The **Routing table** first checks if the destination address matches `172.31.0.0/16`,
              - If it doesn't match, it sends traffic to **IGA A**
  - If the service going out to the internet in the routing table goes through `Internet Gateway`, it's called a **Public Subnet**

<br>

### NAT Gateway

![image-20201011022745821](../../../kor/images/image-20201011022745821.png)

- A gateway that connects **Private subnets** to the **internet** or **other AWS services** through `Network Address Translation`
  - If the service going out to the internet in the routing table goes through `NAT Gateway`, it's called a **Private Subnet**
- An **outbound instance** for **Private Subnets** to communicate with the internet
  - NAT Gateway operating on Public receives outbound traffic requested from private subnet to the outside and connects with `Internet Gateway`

<br>

### Security Group

![image-20201011022121617](../../../kor/images/image-20201011022121617.png)

- A set of rules that acts as a **virtual firewall** controlling `Inbound` and `Outbound` traffic for **instances**
  - What rules to allow Inbound traffic through
  - What rules to allow Outbound traffic through
- Network ACL and Security Groups act like **firewalls** and can set **Inbound traffic** and **Outbound traffic** security policies
  - **Security Group vs Network ACL**
    - `Security Groups` work in a **stateful** manner,
      - Operating security groups are configured by default to block all permissions
        - So you need to allow necessary settings
      - Unlike Network ACLs, security groups can set separate traffic,
        - Can be applied to Subnets but also to individual EC2 instances
    - `Network ACL` operates **statelessly**,
      - Since all traffic is set as default
        - You need to block unnecessary traffic
          - Applied at the Subnet level, cannot be set per resource
    - If Network ACL and Security Groups conflict, Security Groups have higher priority!

<br>

### VPC Endpoint

- An AWS service that allows direct use of AWS services between various AWS services inside VPC without going through **Internet Gateway** or **NAT Gateway**
  - You can privately connect VPC to `PrivateLink`-powered AWS services and VPC Endpoint services without requiring `Internet gateway`, `NAT device`, `VPC connection`, or AWS Direct Connect connection
  - **VPC Instances** do not require **Public IP** to communicate with **service resources**!
  - Traffic between VPC and other services does not leave the Amazon Network 
