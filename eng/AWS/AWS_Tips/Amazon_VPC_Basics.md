# Getting Started with Amazon VPC

> Dissecting VPC!
>
> References: [Amazon VPC docs](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html), [44bits.io](https://www.44bits.io/ko/post/understanding_aws_vpc)

<br>

## What is Amazon VPC?

> Virtual Private Cloud defined by users

- VPC has important features that differentiate it from traditional server hosting
  - With VPC, you can **directly design** your network environment
- In VPC, you can use both IPv4 and IPv6 to access resources and applications safely and easily

- VPC **provisions logically isolated spaces**
  - VPC is a function that creates an isolated network exclusively for resources created within one account!!
    - When using VPC, resources of specific users are created in logically isolated networks, making it impossible for others to access or even see them!
  - EC2-Classic network environment is a public space shared with other users
    - In the past, you could choose between EC2-Classic and EC2-VPC network environments!! (I see..)
    - Currently, when AWS creates an AWS account, it creates a **default VPC** for each region
      - Using the default VPC allows you to easily use services provided by AWS without being too conscious of Amazon VPC, just like using EC2-Classic network
      - Even when using the default VPC, you can enjoy the advantages of an isolated network environment unlike EC2-Classic!

<br>

<br>

## VPC Components

<br>

### 1. VPC

- The most fundamental resource for creating a private cloud

- A resource that configures a logically independent network

  - Must have a name and IPv4 CIDR block
    - **CIDR (Classless Inter-Domain Routing) block**
      - A method for specifying IP ranges
      - Configuration
        - IP address
        - Netmask number following `/`
          - Represents IP range
            - If this number is 32, it points to exactly one IP described in front
            - ex) `192.168.0.0/32` points to `192.168.0.0`
            - Range is `2^(32-n)` IPs from the specified IP
              - ex) If the trailing number is 24, then `2^(32-24)=256` IP addresses
              - ex) `192.168.0.0/24` is IPs from `192.168.0.0` to `192.168.1.255`

- Resources created in the cloud are basically created on specific networks and have private IPs to access them

  - These resources are created on specific VPCs!
    - They get allocated appropriate IPs within the VPC's CIDR range
    - ex) An EC2 instance created in a VPC with CIDR block `192.168.0.0/24` can be allocated IP `192.168.0.127`
  - When all allocatable IPs within the VPC range are allocated, no more resources can be created
    - You need to create a VPC of appropriate size!!
      - Maximum VPC size is 16 (`netmask`)
        - 2^(32-16)=65536 IPs available

- Another thing to consider when creating a VPC!

  - While there are no special constraints on specifying CIDR ranges, problems can occur if connected to the internet

    - ex) Just for reference!

      > For example, consider the case where `52.12.0.0/16` is specified as the CIDR block. In this VPC, traffic accessing `52.12.0.0/16` is routed inside the VPC. However, IPs in this range are IPs that can be used on the internet. Therefore, in this VPC, it is fundamentally impossible to access internet IPs belonging to `52.12.0.0/16`. If internet connection is needed, you must use private network ranges, and even if internet connection is not needed, it is recommended to use private network ranges when possible. Private network ranges are `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`.

  - Since VPC is configured as an independent network environment, it is possible to create VPCs even if CIDRs are the same or overlapping

    - When using multiple VPCs together later, problems can occur if IP ranges overlap
      - **Creating a VPC is easy, but once created, changing existing CIDR is impossible**
        - Cannot change, but can add new CIDR
      - Since it would be difficult to move VPC internal resources if problems arise
        - When building a production environment, it's good to fully understand VPC constraints and decide on CIDR!!!!!
          - Default VPC's CIDR block is `172.31.0.0/16`

<br>

<br>

### 2. Subnet

- You can't do anything with just a VPC
  - VPC is divided again into units that have CIDR blocks
- Subnets are connected to the physical space where resources are actually created, called `Availability Zone (AZ)`
  - If VPC represents a logical range,
  - Subnet is a network within VPC where resources can actually be created
    - When creating resources for other services, you never specify only VPC!
      - Either specify both VPC and Subnet or
      - If you specify Subnet, VPC can be automatically inferred!
- One VPC can have N subnets
  - `Maximum subnet size` == `VPC size`
  - It's possible to create only one subnet the same size as VPC
  - You can choose not to create subnets, but in this case, you can't do anything with VPC
  - Generally, considering available AZs, you create and use subnets of appropriate size equal to the number of AZs
    - **Creating subnets equal to N AZs and distributing resources is advantageous for disaster response!!**
      - `ap-northeast-2` (Asia Pacific Seoul) has 4 AZs! - 07.17.2020  
        - AZs located in AWS regions consist of **one or more individual data centers** with separate facilities with backup power equipment, networking, and internet connectivity
- Subnet netmask range can use 16 (65535) to 28 (6)
- You can specify CIDR blocks belonging to the VPC CIDR block range
  - One subnet is connected to one AZ
    - 1 subnet - 1 AZ
  - The number of available AZs differs by region
    - Usually 2 or more
    - Our Seoul has 4! Clap clap clap!
  - When dividing subnets by AZ for disaster response, you need to check the number of available availability zones in a specific region in advance
    - Even if you don't use all AZs, it's common to use 2 or more AZs
      - That's why interview assignments have 2 AZs (subnets)
  - In default VPC, subnets with `Netmask` 20 are automatically created equal to the number of AZs

<br>

`+`

#### Reason for Creating 2 Subnets

- It's possible to create EC2 instances with just one subnet connected to one availability zone!
  - However, many AWS services including EC2 support the concept of multi-AZ
  - A function that simultaneously deploys similar resources to one or more availability zones

- The reason for doing this is related to **fault tolerance**!
  - One region has multiple availability zones
  - These availability zones are not just virtually separated, but also physically separated!
    - By placing similar resources in multiple availability zones, it's possible to design so that services don't fail even if one availability zone has problems
  - AWS provides 2 or more availability zones per region and recommends designing networks based on 2 or more availability zones (subnets)!

<br>

<br>

### 3. Route Table

> Resource connected to Subnet

- When using networks in subnets, `Route table` is used to find destinations

  - Route table is connected to Subnet but is created when VPC is created and is also connected to VPC
  - Route table is used as the default route table when creating subnets belonging to VPC

- **One route table can be used by multiple subnets belonging to VPC**

- Automatically created Route table has only one rule defined

  - A rule where the target is `local` when the destination is VPC's CIDR block

    - ex) When VPC's CIDR Block is `127.31.0.0/16`, if looking for resources in the network whose destination is in the `192.31.0.0/16` range, it looks inside the VPC

    - This rule cannot be deleted!!!!!

      - To connect to the internet or communicate with other VPCs, you must additionally define Route rules in the Route table!

<br>

<br>

### 4. Internet Gateway

- VPC is basically an isolated network environment
  - Resources created in VPC basically cannot use the internet
    - Internet Gateway is needed to connect to the internet!
- Adding appropriate **rules** pointing to Internet Gateway in the routing table connects specific subnets to the internet
  - However, just connecting `Subnet` and `Internet Gateway` is not enough to use the internet!
    - Resources that want to use the internet must have a Public IP

<br>

`+`

#### NAT Gateway

: Allows outbound traffic from private subnets to the internet (for IPv4)

<br>

<br>

### 5. DHCP Option Set

> DHCP standard for delivering configuration information to hosts on TCP/IP networks

- Using DHCP, you can configure information such as:
  - Domain Name Server
  - Domain Name
  - NTP (Network Time Protocol) Server
  - NetBIOS Server
- Generally, use the **DHCP Option set** created when VPC is created as is

<br>

<br>

### 6. Network ACL (Access Control List)

> Virtual firewall that controls outbound and inbound traffic

- One Network ACL can be reused by multiple subnets
- Plays a role in controlling traffic at the subnet level

<br>

<br>

### 7. Security Group

> Virtual firewall that controls traffic at the instance level

- Even if passing through Network ACL rules, if not passing through Security Group rules, it may not be able to communicate with instances

<br>

*Through Network ACL and Security Group, you can build a secure network environment*!

<br> 
