# Amazon Security Group

> Let's learn about Amazon Security Groups
>
> References: [Book] AWS Discovery Book

<br>

### What is Amazon Security Group?

- A Security Group acts as a `virtual firewall` that controls **inbound** and **outbound** network traffic to instances
- When starting an EC2 instance, you can assign up to **5 security groups** per instance
- The configured security group functions similarly to firewall policies used in existing **on-premise** environments.
  - However, security groups can only **allow** network traffic but cannot **deny** it!
    - why?
      - Because security groups are rules applied at the EC2 level!
        - To apply **blocking functionality**, you can control network flow at the **subnet** level through `Network ACL`, one of the features of `VPC`

<br>

<br>

### Key Features of Amazon Security Groups

<br>

#### 1. Security Groups Have Limits on the **Number** of Security Groups That Can Be Created and **Rules**

- The number of security groups that can be created per VPC is limited to **500** by default
- The number of rules that can be added per security group is limited to **50**
- 5 security groups can be applied per network interface
  - However, if needed, you can request a limit increase through `AWS Support`

<br>

#### 2. There Are `Allow` Policies for Network Traffic but No `Deny` Policies

- General firewalls have both allow and deny policies to control network flow
  - However, security groups have allow policies but no deny policies
    - To apply deny policies, you must use the **Network ACL** feature of **VPC**

<br>

#### 3. You Can Control `Inbound Traffic` and `Outbound Traffic` Separately

<br>

#### 4. Initial Security Group Configuration Has No Inbound Security Rules

- When you first create an EC2 instance and want to communicate with other EC2 instances,
  - You must add **inbound rules** for communication with that EC2 to enable EC2-to-EC2 communication 
