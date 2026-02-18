# Encapsulation and Decapsulation

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

- When data is sent from the `upper layers` to the `lower layers`, the Physical Layer transmits signals through the network in the form of **electrical signals**
- On the receiving side, data is sent back from the `lower layers` to the `upper layers`
  - The process of sending data is called **Encapsulation**, and the receiving process is called **Decapsulation**

![encapsulation and de-encapsulation in tcp/ip model](https://www.computernetworkingnotes.org/images/cisco/ccna-study-guide/csg25-03-tcp-ip-encapsulation.png)

<br>

- Modern networks are mostly `packet`-based networks
  - `Packet networks` split data into small units called packets for transmission,
    - This technique allows **multiple terminals to communicate simultaneously** rather than having one communication **monopolize the entire line**
  - Data is **split** into packets, sent to the destination through the network, and on the receiving side, they are **reassembled** into the original large data form

<br>

<br>

### Encapsulation

- When an application sends data down to the **Data Flow Layer (Layers 1~4)**, the data is divided so it can fit into packets, and this process is called **Encapsulation**
- The data is split into appropriate sizes considering network conditions, and as shown in the figure above, **information needed for network transmission** is added to the `header` starting from Layer 4 (Transport Layer)
  - **Header information** is added at `Layer 4`, `Layer 3`, and `Layer 2` respectively, with each adding the information it needs in predefined **bit units** (0 or 1)
    - After Layer 4 adds its header and sends it down to `Layer 3`, `Layer 3` adds its required header and sends it down to `Layer 2`
    - `Layer 2` also adds necessary information to the header and then converts it to **electrical signals** for transmission to the receiver
- The task of transmitting data is more complex than expected, with **3 header layers** being added just in the data flow layer (Layers 1~4)

<br><br>

### Decapsulation

- On the receiving side, the **Decapsulation** process is performed
- The received **electrical signals** are converted into **data form** and sent up to `Layer 2`
- `Layer 2` checks the information contained in the Layer 2 header written by the sender
  - If the **destination** in the `Layer 2` information is not itself, the **packet** was not intended for it, so it is discarded
    - This role is handled by the **LAN Card**
  - If the destination in the `Layer 2` information is indeed itself, the information is sent up to `Layer 3`
    - When sending data to the upper layer, the **Layer 2 header information** is no longer needed, so it is **stripped off and sent up**
    - At `Layer 3` and `Layer 4`, the same process occurs: checking each layer's information, confirming whether it is intended for itself, and if so, sending it to the upper layer

<br>

<br>

These operations can be explained by the following 2 information flows

1. The process of **data being transmitted** through `Encapsulation` and `Decapsulation`
2. The **logical communication process** between sender and receiver layers using each layer's `header`

<br>

- In reality, data comes down from the Upper Layer to the Lower Layer, being **encapsulated** into **packets** one by one, and at the Layer 2 **LAN card**, it is converted to **electrical form** and delivered to the destination
- The destination that receives the electrical signal converts it to **data form** and sends it up to the upper layers, assembling the **packets** into **data form**
- In other words, actual data is transferred from `upper layers` to `lower layers` and from `lower layers` to `upper layers`, while **header information** is transferred between respective layers

<br>

<br>

### Header Information

During the process of **encapsulating** data, various information is put into the **header**, but even among this complex information, there are rules, and the following two pieces of information must be included

1. Information defined at the current layer
2. Upper protocol indicator

<br>

#### 1. Information defined at the current layer

- Information appropriate to the purpose of each layer of the OSI 7 layers is included
- The purpose of `Layer 4` is to properly **split** large data and **assemble** it correctly on the receiving side, so the role of **ordering** data and **checking** whether the order of received `packets` is correct is important, and this information is written into the `header`
  - In **TCP**, the Layer 4 protocol of `TCP/IP`, this data is represented by the **Sequence number** and **ACK number** fields
- The `Layer 3 header` contains the **logical addresses** defined at Layer 3: the **source and destination IP addresses**
- Layer 2 defines **MAC addresses**, and like Layer 3, Layer 2 also includes the **source and destination MAC addresses** in the header

<br>

#### 2. Upper protocol indicator

- The **protocol stack** has more types as you go up to higher layers
  - The Layer 3 protocol `IP` branches into `TCP` and `UDP` at Layer 4, and at even higher layers, it branches into even more diverse protocols like `FTP`, `HTTP`, `SMTP`, `POP3`, etc.
- During the **Encapsulation** process, having many upper protocols is not a problem, but on the destination side performing **decapsulation**, if there is no information in the header, it cannot determine **which upper protocol** to forward the data to
  - ex) When Layer 3 checks the destination `IP address` and sends data up to Layer 4, if there is no upper protocol information in the header, it cannot distinguish whether to send it to `TCP` or `UDP`
- To prevent this problem, the encapsulating side must include **upper protocol indicator information** in the `header`

<br>

<br>

### Upper Protocol Indicators

- Each layer has an upper protocol indicator, but the name differs for each layer
  - Layer 4 uses port number
  - Layer 3 uses protocol number
  - Layer 2 uses Ether Type
- An important point to note here is that while the port number is information written in the Layer 4 header, it indicates the protocol type at the application layer
  - That is, when **decapsulating**, since upper protocol information must be used to determine which upper protocol to send to, the information for one layer above the operating layer is written

<br>

#### Port Number - Layer 4

| Port Number       | Service                                   |
| ----------------- | ----------------------------------------- |
| TCP 20, 21        | FTP (File Transfer Protocol)              |
| TCP 22            | SSH (Secure Shell)                        |
| TCP 23            | TELNET (Telnet Terminal)                  |
| TCP 25            | SMTP (Simple Mail Transport Protocol)     |
| UDP 49            | TACACS                                    |
| TCP 53 / UDP 53   | DNS (Domain Name Service)                 |
| UDP 67, 68        | BOOTP (Bootstrap Protocol)                |
| TCP 80 / UDP 80   | HTTP (HyperText Transfer Protocol)        |
| UDP 123           | NTP (Network Time Protocol)               |
| UDP 161, 162      | SNMP (Simple Network Management Protocol) |
| TCP 443           | HTTPS                                     |
| TCP 445 / UDP 445 | Microsoft-DS                              |

<br>

#### Protocol Number - Layer 3

| Protocol Number | Protocol                         |
| ------------- | -------------------------------- |
| 1             | ICMP (Internet Control Message)  |
| 2             | IGMP (Internet Group Management) |
| 6             | TCP (Transmission Control)       |
| 17            | UDP (User Datagram)              |
| 50            | ESP (Encap Security Payload)     |
| 51            | AH (Authentication Header)       |
| 58            | ICMP for IPv6                    |
| 133           | FC (Fibre Channel)               |

<br>

#### Ether Type

| Ether Type                       | Protocol                             |
| -------------------------------- | ------------------------------------ |
| 0x0800                           | IPv4 (Internet Protocol version 4)   |
| 0x0806                           | ARP (Address Resolution Protocol)    |
| 0x22F3                           | IETF TRILL Protocol                  |
| 0x8035                           | RARP (Reserve ARP)                   |
| 0x8100                           | VLAN-tagged frame (802.1Q)           |
| Shortest Path Bridging (802.1aq) | AH (Authentication Header)           |
| 0x86DD                           | IPv6 (Internet Protocol version 6)   |
| 0x88CC                           | LLDP (Link Layer Discovery Protocol) |
| 0x8906                           | FCoE (Fibre Channel over Ethernet)   |
| 0x8915                           | RoCE (RDMA over Coverged Ethernet)   |
