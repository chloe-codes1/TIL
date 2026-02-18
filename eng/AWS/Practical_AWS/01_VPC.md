# VPC

> A deep dive into VPC - Practical ver.

<br>

<br>

### What is VPC?

- AWS introduced the Virtual Private Cloud to abstract and explain networking
- You can create multiple VPCs in a single account!

<br>

<br>

### Default VPC

- When you create an account, one **default VPC** is created per region
  - The Default VPC is assigned IPv4 CIDR `172.31.0.0/16`
  - Default subnets within the Default VPC are assigned `/20` net blocks within the VPC CIDR range
- If you build your infrastructure on the default VPC as-is
  - The question is whether the person configuring the infrastructure **is allowed to use that network range**
    - For larger companies, each branch/office may have different network ranges
      - This means some connections may work while others may not
        - So you need to be aware of each network range to check for conflicts, which is inconvenient

<br>

<br>

### Designing CIDR Blocks Properly

- The range of assignable IP addresses in an AWS VPC network is reduced by more than just the usual `Network address` and `Broadcast address`
  - A total of 5 are reserved
    - `Network address`
    - `Broadcast address`
    - `Reserved by AWS for VPC router`
    - `Reserved by AWS`
    - `Reserved by AWS for future use`
- Load balancers also consume IPs from your VPC, so this must be considered
  - ALB, NLB, and CLB each take at least 2 IPs for redundancy and HA configuration, and more if traffic is high

<br>

#### CIDR Configuration in a Public Cloud Environment

- Set CIDR to 16
  - Don't think too conservatively
    - You may need to expand later
    - In the cloud, 16 bits is appropriate!

<br>

<br>

#### Private IPv4 addresses

| RFC1918 name |       IP address range        | Number of addresses | Largest [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) block (subnet mask) | Host ID size | Mask bits | *[Classful](https://en.wikipedia.org/wiki/Classful_network)* description[[Note 1\]](https://en.wikipedia.org/wiki/Private_network#cite_note-4) |
| :----------: | :---------------------------: | :-----------------: | :----------------------------------------------------------: | :----------: | :-------: | :----------------------------------------------------------: |
| 24-bit block |   10.0.0.0 – 10.255.255.255   |      16777216       |                    10.0.0.0/8 (255.0.0.0)                    |   24 bits    |  8 bits   |                  **single class A network**                  |
| 20-bit block |  172.16.0.0 – 172.31.255.255  |       1048576       |                 172.16.0.0/12 (255.240.0.0)                  |   20 bits    |  12 bits  |              **16 contiguous class B networks**              |
| 16-bit block | 192.168.0.0 – 192.168.255.255 |        65536        |                 192.168.0.0/16 (255.255.0.0)                 |   16 bits    |  16 bits  |             **256 contiguous class C networks**              |

- AWS allows you to use any private IP range
- There are no conflicts with the AWS management network (thanks to AWS's virtual networking technology)

<br>

<br>

### Why You Should Enable DNS hostnames and DNS resolution

![dns](../../../kor/images/dns.png)

- `DNS hostnames`

  - When enabled, **DNS lookup** is possible through the AWS domain

- `DNS resolution`

  - If disabled

    - Issues may arise when connecting to EKS
    - Alias connections via Route 53 become unavailable
