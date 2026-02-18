# ARP (Address Resolution Protocol)

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

- Layers 2 and 3 of the OSI 7 Layers have **addresses** that allow finding the **destination** during communication, but there is no relationship between the Layer 2 `MAC address` and Layer 3 `IP address`
  - Layer 2 `MAC addresses` are addresses arbitrarily assigned by hardware manufacturers,
  - Layer 3 `IP addresses` are **directly assigned** or **automatically assigned** using **DHCP**
- Actual communication occurs based on `IP addresses`, and the `MAC address` of the other party is automatically discovered for communication
  - The protocol used to discover the other party's MAC address is **ARP (Address Resolution Protocol)**

<br>

## 1. What is ARP?

- Two addresses are used for data communication: the Layer 2 physical `MAC address` and the Layer 3 logical `IP address`
  - Since the IP address system is completely unrelated to physical MAC addresses, a **mechanism** to **link the two addresses** is needed
    - The protocol used for this is **ARP**
- The `ARP protocol` does not only work for TCP/IP protocols
  - In protocols like TCP-Ethernet where there is **no relationship** between Layer 3's **logical address** and Layer 2's **physical address**, mechanisms like the ARP protocol are used to **link** physical and logical addresses
- When a Host has had no communication and **attempts communication for the first time**, it cannot immediately `encapsulate (Encapsulation)` the packet
  - When attempting communication, the source and destination IP addresses are known and can be encapsulated without problems, but **the other party's MAC address is unknown**, so Layer 2 encapsulation cannot be performed
    - To find out the other party's address, `ARP Broadcast` must be used to **query the entire network for the other party's MAC address**
- The destination that receives the `ARP Broadcast` uses `ARP protocol` to **respond with its own MAC address**
  - Once this process is complete, both source and destination **learn each other's MAC address**,
  - And subsequent packets can be normally encapsulated and delivered to the other party
- In `Packet Networks`, since **large data** is **split and transmitted**, **multiple packets** must be sent
  - Performing `ARP Broadcast` with every packet would greatly **degrade** network communication **efficiency**, so the information is **stored in memory** and **reused**
    - While maintaining the `ARP Table` for a long time is good for performance, since logical addresses (IP) can change at any time, this table is **deleted if there is no communication for a certain period**

<br>

<br>

## 2. ARP Operation

- Among various fields in the ARP Packet, the following 4 fields used in ARP data are important
  1. Sender hardware MAC address
  2. Sender IP Protocol address
  3. Target MAC address
  4. Target IP Protocol address
- ARP operates using the above 4 fields as follows
  - ex) Server A (`1.1.1.1`) -------- Server B (`1.1.1.2`)
    - When Server A tries to ping Server B, Server A can encapsulate up to the Layer 3 IP address, but cannot create the packet normally because the destination MAC address is unknown
    - Server A **broadcasts** an ARP request to the network to find Server B's MAC address
      - When broadcasting the ARP packet to the network, the Layer 2 MAC address source is filled with its own MAC address, the destination is filled with broadcast (FF-FF-FF-FF-FF-FF),
      - The ARP protocol fields are filled with its own MAC and IP as sender, target IP address as `10.1.1.2`, and target MAC address as `00-00-00-00-00-00`, then broadcast to the network
    - Since the Layer 2 destination address is the broadcast address, this ARP packet is sent to **all terminals** in the **same network** and all terminals check the ARP protocol contents
      - They check whether the target IP in the ARP protocol is theirs, and **discard** the ARP packet **if it is not**
    - Server B **processes the ARP request** because the target IP address is its own IP, and sends a **response**
      - At this point, the sender and target positions are swapped
    - Unlike Server A which initially sent the ARP request, Server B already knows Server A's IP and MAC addresses from receiving the ARP request, so it can **fill all ARP fields for the response**
      - Using Server A's information from the ARP request, it fills the target MAC and IP addresses and puts its own MAC and IP as sender MAC and IP addresses
        - The initial ARP **request** is **broadcast** (Layer 2 destination MAC address is broadcast),
        - While the ARP **response** is **unicast** with source and destination MAC addresses specified
    - Server A receives the ARP response from Server B and **updates** its **ARP cache table**
      - This ARP cache table is maintained until there is **no communication with Server B** for the defined time
        - If communication occurs again within that time, the timer **resets**
    - After the ARP cache table is **updated**, since the **other party's MAC address** is known, the destination MAC address field can be completed and the **ping packet** can be sent

<br>

<br>

## 3. GARP

- In addition to regular ARP, there are protocols like `GARP` and `RARP` that use the same ARP protocol fields but with **modified content** for **purposes different from the original ARP protocol**
- `GARP` stands for Gratuitous ARP, where the **target IP field** is filled with **one's own IP address** for the ARP request
  - While ARP is used to discover the other party's MAC address, `GARP` is used for the purpose of **announcing one's own IP and MAC address**
    - Therefore, GARP's destination MAC address (Layer 2 destination MAC) uses the **broadcast MAC address**
- Looking at the `GARP` packet:
  - Sender MAC is one's own MAC address,
  - Sender IP address is one's own IP address,
  - Target MAC address is all **0s** as `00:00:00:00:00:00`,
  - Target IP address is also filled with one's own IP address and **broadcast** to the network

<br>

### 3-1. Other ARP Requests vs GARP

- Similarity
  - The target MAC address is filled with `00:00:00:00:00:00`
- Difference
  - The sender and target IP addresses are the same (both are one's own)

<br>

### 3-2. Why GARP is Used to Announce One's IP and MAC Address to the Same Network

#### 1. IP Address Conflict Detection

- IP addresses should be uniquely assigned, but for various reasons someone else may be using the IP assigned to you
  - To prevent communication failure due to IP conflicts, `GARP` is used to check whether the assigned IP is already in use on the network
- When a terminal connects to the network, `GARP` can be used to **check whether the currently configured IP address is being used on the network**
  - If a response to `GARP` is received, it means a terminal already using that IP exists on the network

#### 2. Updating the ARP Table of Other Parties (on the same subnet)

- Primarily used in **database HA (High Availability)** solutions that do not use `virtual MAC addresses`
  - **Database HA** typically has two database servers serving under a single virtual IP address
    - Only one of the two databases operates while the other stands by in an `Active-Standby` configuration
    - The `Active` server responds to **virtual IP address** requests for service, but uses the **actual MAC address** rather than a virtual address
  - If the responding `master device` A stops working, standby device B becomes `active` and responds to ARP requests for the virtual IP address
    - Terminals communicating with the newly active device B for the first time learn the changed active's MAC address and can communicate,
    - But terminals that were communicating with the former master device A still have A's MAC address in their **ARP Cache Table** and continue sending packets to A
    - Packets sent by terminals with stale information either cannot receive responses from the network, or are sent to A which is in `Standby` state, so normal service cannot be received
      - To prevent this phenomenon, when a `Standby` device becomes `Active`, it sends **GARP Packets** to the network to announce that the active device has **changed**
        - Subsequently, the **ARP tables** of local network terminals are updated with the virtual IP address mapped to the new MAC address
- In recent network devices, this form of HA is rarely used
  - Since techniques for **intercepting packets** using **GARP** are widely used, there may be terminals that do not update their ARP table even when receiving GARP for **security reasons**, so `HA solutions` using `virtual MACs` that avoid this problem are used

#### 3. Clustering for HA (High Availability), `VRRP (Virtual Router Redundancy Protocol)`, `HSRP (Hot Standby Router Protocol)`

- While the HA solution in #2 above is used for **device redundancy**, GARP is also used in `Clustering`, `VRRP`, `HSRP` and similar **FHRP (First Hop Redundancy Protocol)** that **do not use actual MAC addresses but use virtual MACs**
  - While the purpose of GARP usage in Database HA solutions was **ARP Table update**,
  - The purpose of `Clustering` and FHRP usage is to update the **MAC Table of switch devices** in the network
    - When `Clustering` uses a virtual MAC address, terminals learn ARP information with the virtual MAC address, so **there is no need to update terminal ARP Tables**
    - However, the **switch's MAC Table** in between must be **updated** when the master changes so that the **virtual MAC address location** is properly directed, so **MAC Table updates are needed when the master changes**
  - Therefore, when a Slave changes its role to master, it sends `GARP`, and the switch updates port information for the MAC address and refreshes the MAC table

<br>

<br>

## 4. RARP

- An abbreviation for Reverse ARP, it literally operates as a reverse ARP
  - Like `GARP`, the ARP Protocol structure is the same, but
    - The content in the fields is different
    - And it is used for purposes opposite to the original
  - **ARP vs RARP**
    - `ARP`
      - IP address -> `ARP` -> MAC address
    - `RARP`
      - MAC address -> `RARP` -> IP address
- `RARP` is used when a **terminal without a defined IP address** **requests IP assignment**
  - `ARP` is a protocol created to query for the MAC address using the other party's IP address when the other party's MAC address is unknown
  - Conversely, `RARP` is used when the terminal knows its own MAC address but has not yet been assigned an IP, to ask an **IP assignment server** **what IP address to use**
- RARP was used for network host address assignment in the past but has been replaced by `BOOTP` and `DHCP` due to limited functionality and is no longer used
