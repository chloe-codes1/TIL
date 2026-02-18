# IP Address

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

- The layers in the OSI 7 layers that have addresses are **Layer 2** and **Layer 3**
  - Layer 2 uses the **physical address**, the **MAC address**,
  - Layer 3 uses the **logical address**, the **IP address**
- Since most networks operate on `TCP/IP`, understanding the IP address system is important
- The **Layer 3 address** of the IP address and other protocol stacks has the following characteristics
  1. It is a **logical address** that users can **change**
  2. The address has **levels**
     - Divided into a `network address` representing the **Group** and a `host address`

<br>

<br>

## 1. IP Address System

- The IP addresses we commonly use are **32-bit** **IPv4** addresses
  - IP has two systems in use: **v4** and **v6**, with **IPv6** addresses being **128 bits**
- When expressing IPv4 addresses, they are divided into 4 **8-bit units** called **octets**, and each octet is separated by **"."**
  - `IPv4 address`: 8 bits x 4 = 32 bits
- Unlike Layer 2 `MAC addresses` expressed in **hexadecimal**, `IP addresses` are expressed in **decimal**, so an **8-bit octet** can have values from **0 to 255**
- While Layer 2's `MAC address` is divided into the manufacturer code **OUI** and manufacturer-specific serial number **UAA** for different purposes,
  - Layer 3's `IP address` is also divided into a **network address** and a **host address**
    - **Network address**
      - An address that refers to the network that groups hosts
      - Networks with the same Network address are called **Local Network**
    - **Host address**
      - An address to distinguish hosts within a single network
- `MAC addresses` are split evenly at 24 bits each, but the **boundary between** the `IP address`'s **network address** and **host address** is **not fixed**
  - This is the most distinguishing feature of the IP address system from other address systems
  - The IP address system introduced the `Class concept` to **allocate different network sizes** based on the required **number of host IPs**
- If the **separator** dividing network and host addresses is **fixed**, all networks would be the **same size** since they could have the same number of `host IP addresses`,
  - But since the **separator can be moved**, network sizes can vary
- The **class concept** introduced by `IP addresses` has the advantage of being able to **conserve addresses** compared to other fixed network address systems
  - If all networks were the same size,
    - Organizations needing large networks would face difficulty in **securing multiple networks** and receiving **contiguous networks**
    - Organizations needing small networks would take **too many IPs**, resulting in **IP waste**
- A, B, and C Classes can be distinguished just by looking at the first octet's address

<br>

### Classful Network

<br>

#### A Class

- Has the largest address space
- Can have approximately 16 million IP addresses
- The **separator** between network and host addresses is at the **first octet**
  - This separator is called the `subnet mask`!
- Since there is 1 octet for the `network address` and 3 octets for the `host address`,
  - It has **2^8 (256)** networks and
  - **2^24 (16,666,216)** host addresses per network
- A, B, and C classes can be distinguished just by looking at the first octet address; if the octet address is in the range `0 ~ 127`, it is A Class
  - In binary, addresses where the first octet is `0 0000000 ~ 0 1111111` are A Class
  - Only `127` is an exception, used as the **Loopback address** representing itself, so the addresses actually usable as A Class are `1.0.0.0 ~ 126.255.255.255`

<br>

<br>

#### B Class

- Has approximately 65,000 IP addresses
- The **separator** is at the **second octet**
- Since there are 2 octets for the `network address` and 2 octets for the `host address`,
  - It has **2^16 (65,536)** networks and
  - **2^16 (65,536)** host addresses per network
- Addresses where the **first digit is 1** and the **second digit is 0** in binary representation of the first octet are B class
  - Binary first octet is `10 000000 ~ 10 111111`,
  - In decimal, addresses from 128 to 191 are B Class

<br>

<br>

#### C Class

- The **separator** is at the **third octet**
- Since there are 3 octets for the `network address` and 1 octet for the `host address`,
  - It has **2^24 (16,777,216)** networks and
  - **2^8 (256)** hosts per network
- Addresses where the **first and second digits are 1** and the **third digit is 0** in binary representation of the first octet are C Class
  - Binary first octet is `110 00000 ~ 110 11111`,
  - In decimal, IPs from 192 to 223 are C class

<br>

The class-based network division technique is a **concept used in the past**, and networks are no longer divided based on classes

To more precisely allocate network addresses, a method of **detailed division** in **1-bit units** is used to match the **required network size**

<br>

`+`

### Determining the Number of Usable Hosts in a Network

- In IP networks, since **network sizes change**, it is important to determine the `number of hosts` and `valid IP range` **usable in a single network**
  - When networks are divided by Class, they are expressed in easily recognizable decimal form making it straightforward to understand, but for `Classless Networks`, determining the valid IP range is very important
- Generally, the total count of all expressible numbers can be calculated as **base^digits**
  - ex) The total numbers a 4-digit decimal number can represent is 10^4
    - 10,000 numbers from 0000 to 9999
- Since IP uses binary, the number of expressible IPs can be calculated as **2^digits**
  - One octet is 8 binary digits, so A Class has 2^24, B Class has 2^16, and C Class has 2^8 IPs
  - However, in the IP system, the **first number** is used as the `network address` and the **last number** as the `broadcast address`, so the actually usable IPs are **A Class** `2^24 - 2`, **B Class** `2^16 - 2`, **C Class** `2^8 - 2`

<br>

<br>

## 2. Classful and Classless Network

- When the IP address system was first created, introducing the Class concept was a good choice that could provide **scalability** and minimal address waste
  - In `Classful Networks`, there was no need for a separator (`Subnet mask`) to divide **network addresses** and **host addresses**
  - Simply looking at the first digit naturally told which class the address belonged to, and the address separator could be applied

<br>

### Classless Network

- As the Internet became commercialized, the number of hosts connected to the Internet increased explosively
  - The existing `Classful` address system was a good system capturing both **scalability** and **efficiency**, but it was far too insufficient to handle the exponentially growing IP address demand
    - Additionally, many IPs were **wasted** in the process of **hierarchizing** and **dividing** network addresses
- The 3 conservation and transition strategies created to solve IP address shortage and waste problems are as follows
  1. Short-term measure - `Classless`, `CIDR (Classless Inter-Domain Routing)` based address system
  2. Medium-term measure - `NAT` and `Private IP addresses`
  3. Long-term measure - Next-generation IP `IPv6`
- The biggest problem with `IPv4` was not just the shortage of addresses themselves, but the waste from organizations that received upper Classes (A Class) not properly using those addresses
  - In `Classful`, once a single class network was assigned to an organization, no matter how many addresses were unused, **IPs could not be divided for other organizations to use**
    - To solve this problem, the class concept itself was abandoned, and this is called `Classless network`
      - The address system we currently use is a **Classless-based address system** that does not apply the Class concept
- In `Classless Network`, a separate separator must be used to divide network and host addresses, and this separator is called the **Subnet Mask**
  - The `Subnet Mask` is used to distinguish between **IP addresses** and **Network addresses**, where binary 1 represents **Network address** and 0 represents **Host address**
    - Typically expressed in decimal as `255.0.0.0`, `255.255.0.0`, `255.255.255.0`
    - Since binary 11111111 in decimal is 255, 255 represents the **Network address** portion and 0 represents the **Host address** portion
      - ex) An IP of `103.9.32.146` with subnet mask `255.255.255.0` has
        - Network address of 103.9.32.0,
        - Host address of 0.0.0.146
  - In Classless-based IT Networks, the subnet mask is required to represent the Network, and it must be used when assigning IP addresses to servers or PCs

<br>

### Subnet Mask Notation Methods

- There are two methods for expressing Subnet masks: **bit-level notation** and **decimal notation**
  - **Bit-level notation** expresses the number of consecutive 1s in the Subnet Mask
    - Expressing A Class as a subnet mask: the first Octet is 1 and the remaining Octets are 0, so it is expressed as `/8`
    - B Class is `/16`,
    - C Class is expressed as `/24`
  - **Decimal notation**:
    - A Class is `255.0.0.0`,
    - B Class is `255.255.0.0`,
    - C Class is `255.255.255.0`

<br>

<br>

## 3. Subnetting

- Ignoring the originally assigned Class criteria and having the user define new **Network-Host criteria** to subdivide the network smaller than classful units is called **Subnetting**
  - It is called **subnetting** because the assigned address is re-divided, and this is the most significant feature of classless networks
  - Subnetting divided by Octet units is easy to understand and operate, but in practice, networks are divided more finely than Octet units, in 1-bit units of binary
- In practice, there are two situations where subnetting must be considered, and the factors and scope to consider differ depending on the situation
  1. When a **network designer** plans how to efficiently divide the network
     - Network scope design considering the required terminals within the network
  2. When a **network user** needs to distinguish between their own network and remote networks in an already divided network
     - Determining the usable IP range in the network
     - Verifying that the Default Gateway and Subnet Mask settings are correct

<br>

### 3-1. Network User's Subnetting

- Network users need to determine the **usable IP address range** in an already designed network
  - If an IP outside the given network range is assigned, or the Subnet mask is incorrectly entered,
    - Communication problems may occur with terminals in a specific range of the Local Network,
    - Or communication with the entire external Network may fail
- Most subnetting is done in **bit units**, and since the IP address system is processed by computers, it is in binary
  - If you are familiar with binary or subnetting is done in octet units, it is easy to determine the network size and IP range, but for 1-bit subnetting, determining the valid network range is difficult
    - Generally, the method to determine **the valid range of your own Network** is as follows
      1. Express your IP in binary
      2. Express the Subnet Mask in binary
      3. Use a binary AND operation to find the subnetted `Network address`
      4. Change all Host address bits to binary 1 to find the `Broadcast address`
      5. Determine the valid IP range
         - `Subnetted Network address + 1` is the smallest valid IP
      6. `Broadcast address - 1` is the largest valid IP
      7. Convert the binary results to decimal
    - It is not always possible to determine the Local Network range using the above method

<br>

#### Simple Subnetting Method

- ex) IP address: `103.9.32.146`, Subnet Mask: `255.255.255.192`
  1. Convert the Subnet Mask to binary
     - ex) `11111111.11111111.11111111.11000000`
  2. Determine the maximum number of IPs the current Subnet can have
     - ex) 2^6 = 64
  3. List multiples of 64 to identify the base Network addresses
     - The first Block starts from 0
     - The last address of each Network becomes the Broadcast address
       - This address is the next block's Network address - 1
     - ex) `0 ~ 63` / `64 ~ 127` / `128 ~ 191` / `192 ~ 255`
  4. Select the Network that contains Host address 146 from `103.9.32.146`
     - ex) `128 ~ 191`
  5. Organize the required addresses
     - **Network address**: `103.9.32.128` (first number)
     - **Broadcast address**: `103.9.32.191` (last number)
     - **Valid IP range**: `103.9.32.129` ~ `103.9.32.190` (between Network and Broadcast addresses)

<br>

The key to the above method is determining the Network size based on the Subnet Mask to find the subnetted Network size!

<br>

<br>

### 3-2. Network Designer's Subnetting

- When building a new Network, contrary to the network user, the designer is not given a Subnet Mask but must consider the **Network size** to **determine the Subnet Mask** and reflect it in the design
  - What a network designer must consider when designing IPs:
    1. How many IPs need to be allocated in a single subnetted Network?
    2. How many subnetted Networks are needed?

<br>

ex) Designing a Network for a company with 12 branches

1. 12 IPs must be allocated in a single subnetted Network
2. Networks grow in powers of 2, so they can be allocated in units of 4, 8, 16, 32, 64, 128, 256
   - The smallest Network that can accommodate 12 IPs is 16, so allocate a Network of 16
     - However, a Network of 16 must exclude 2 IPs for `Network address` and `Broadcast address`, so the actually usable IPs are 14
3. Secure 12 of the 16-unit Networks
   - List multiples of 16 starting from 0 to identify Network addresses
4. Allocate 12 Networks out of the total 16 to each branch

<br>

- When designing a Network, it is best to use private IP ranges to ensure **sufficient IP range**
- If public IPs are used with no margin for Network allocation, there will be **many different-sized Networks**
  - This makes management difficult for network administrators and makes it hard for general users to easily distinguish or recognize IPs
- It is advisable to allocate **same-sized** Networks as much as possible, and divide in **C class units** of **24 bits** that are easily understood even in decimal notation

<br>

<br>

## 4. Public IP and Private IP

- To access the Internet, an IP address is needed and this IP must be a globally unique identifier
  - Such an IP address is called a **Public IP** address
- If you configure a Network privately without connecting to the Internet, you can build a Network without being assigned a public IP address
  - The IP addresses used in this case are called **Private IP** addresses
- To access the Internet, you need to be assigned an IP address from a `telecommunications carrier` or obtain an **Autonomous System Number (ASN)** from an `IP allocation agency (KISA in Korea)` and then receive independent IPs, making the process complex
- If you do not access the Internet or use **NAT (Network Address Translation)** technology (using a home router or company firewall), **private IPs** can be used
  - These addresses are specified in the Internet standard document **RFC**
  - Using **Private IP** prevents direct Internet access, but after converting to **public IP** at the **NAT device**, Internet access becomes possible
- When building a Private Network within a company, even if connecting to the Internet via NAT, **IPs assigned to other users** should not be used as private IPs
  - If Public IPs used by other organizations are used internally, access to those IPs becomes impossible
- `Private IPs` can use **1 A Class**, **16 B Class**, and **256 C Class**
  - Large Enterprise networks mostly use the A Class size `10.0.0.0/8` network,
  - For smaller networks, C Class `192.168.x.0/24` is used
    - This is why the most common default IP for home routers is `192.168.0.1`
