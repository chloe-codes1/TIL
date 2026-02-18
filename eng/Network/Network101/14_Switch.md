# Switch

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

## Before Getting Started

<br>

### What is a Switch?

- The **Switch**, the most critical device in a network, operates based on the Layer 2 address, `MAC address`
- The Switch sits in the middle of the network and serves as a **mediator** that receives `packets` and **sends them only where needed**
  - The Switch can perform its basic operation of **forwarding packets** based on `MAC addresses` without any configuration when connected to the network
- Beyond the basic operation of recognizing `MAC addresses` and forwarding packets, the Switch also has
  - `VLAN functionality` that can **logically separate networks** on a single device,
  - Functions like `STP (Spanning Tree Protocol)` that **prevent Network Loops** built in by default

<br>

<br>

## Switch Device Operation

- The Switch is a device that **mediates communication** in a network
- In old `Ethernet Networks` without switches, devices would **compete** when sending **packets**, causing significant **network performance degradation**
  - The device that helps **multiple devices communicate simultaneously without interference** is the `Switch`
    - Using a Switch eliminates the need to **wait to communicate or wait due to collisions**, and the **overall network communication efficiency improves**
- The Switch's core role is to **identify who is at which location** and, when actual communication begins, **accurately transmit packets** to the location it knows
  - This is possible because the Switch **understands Layer 2 addresses**
    - And has a **MAC Address Table** that maps the terminal's `MAC address` to the `Interface information` where the terminal is located
- The Switch checks the **Layer 2 destination address in the header** of the packet it wants to forward, finds **which port that address is on** in the MAC Address Table, and **sends the packet only to that port**
  - To perform this role, the Switch needs a **MAC Address Table** with `MAC addresses` and `ports` mapped
    - If a packet enters the switch with a destination address not in the Table,
      - The Switch **sends the packet to all ports**
    - If the packet's destination address is in the Table,
      - It **sends the packet only to the mapped port** and does not send it to other ports
  - The Switch's operation can be summarized in these 3 actions:
    1. Flooding
    2. Address Learning
    3. Forwarding/Filtering

<br>

### 1. Flooding

- When a Switch boots, it has **no network-related information**
  - At this time, the switch cannot fulfill its role of **mediating network communication** and operates like a **hub**
    - A `Hub` **forwards packets to all ports** except the incoming port
      - The Switch's operation of **flooding packets to all ports** like a hub is called `Flooding`
- When a packet enters the Switch, it **checks the destination MAC address** and looks for that MAC address in its MAC Address Table
  - If there is no matching destination MAC address information in the MAC Address Table, it **sends the same packet to all ports**
    - Since the Switch operates in a `LAN`, it performs this action **under the assumption** that a device **may exist somewhere** even without its own information
- Flooding is a normal Switch operation, but if it happens too often, the Switch cannot perform its proper role
  - When a packet enters the switch, it **reads the MAC address** from the packet information and **learns** it to build the **MAC Address Table**, then uses it to forward packets

<br>

#### Abnormal Flooding

- A Switch flooding packets means the **switch is not functioning properly**
  - In `Ethernet - TCP/IP` networks, **ARP Broadcast** is exchanged beforehand, so **when actually sending and receiving data, the switch does not flood packets**
- Using a Switch allows **forwarding packets only where needed**, making it difficult to **maliciously intercept** surrounding communications, which is more secure than a `hub` that floods all packets
  - Attack techniques exist to neutralize this Switch function and monitor surrounding communications
    - ex)
      - Making the Switch learn wrong MAC addresses, or
      - Filling the Switch's MAC Address Table to capacity to **force flooding behavior**
  - If the switch is flooding packets for no reason,
    - The Switch may not be operating normally, or
    - An attack may be being carried out nearby
- Additionally, `ARP poisoning` techniques may be used to make the attacker's MAC address appear as the MAC address of the IP to be monitored, receiving the desired communications, so caution is needed

<br>

### 2. Address Learning

- For the Switch to properly perform its operation of checking the destination MAC address and **forwarding to the desired port**, it must build and maintain a **MAC Address Table**
  - The `MAC Address Table` is a **temporary table** that stores information about which device (MAC address) is connected to which location (port)
    - The process of **building and maintaining this MAC Address Table** is called `Address Learning`
- `Address Learning` uses the packet's **source MAC address information**
  - When a packet enters a specific port, the switch records the **source MAC address** and **port number** in the MAC Address Table
    - If a packet entering port 1 has source MAC address AAAA, it can be inferred that a device with MAC address AAAA is connected to port 1, and this is how information is acquired
- `Address Learning` uses MAC address information, so it cannot learn broadcast or multicast MAC addresses
  - Both are only used in the **destination MAC address field**!

<br>

#### Pre-defined MAC Address Table

- In addition to learning surrounding devices' MAC addresses through `MAC address learning`, the Switch also has **pre-defined MAC address information**
  - These pre-defined addresses are not for processing packets but are mostly **addresses used for inter-switch communication**
  - These types of addresses can also be found in the `MAC Address Table`, but since **addresses processed internally by the switch** are not sent to specific ports but processed within the switch,
    - Adjacent port information may be absent, or
    - Expressed with terms indicating CPU or management module

<br><br>

### 3. Forwarding/Filtering

- Switch operation is very simple: when a packet enters the switch,
  - It checks the **destination MAC address**
  - Compares it with its **MAC Address Table**, and if matching information exists, **forwards the packet to the matching port**
    - At this time, the packet is not sent to other ports, and this operation is called `filtering`
- The Switch **ensures packets are delivered only to the destination** through `forwarding` and `filtering`
- In a Switch, `forwarding` and `filtering` can be **performed simultaneously on multiple ports**
  - Since communication does not affect other ports, other ports can **operate independently** from existing communication

- The Switch performs `forwarding` and `filtering` only for **regular Unicast**
  - **BUM Traffic** -- Broadcast, Unknown Unicast, Multicast -- operates slightly differently
    - Since neither broadcast nor multicast are used as source MAC addresses, these types of traffic are **all flooded** without forwarding or filtering
    - Unknown Unicast also has an **address not in the MAC Table**, so it is flooded just like broadcast

<br>

#### ARP in LAN - Switch Operation

- In `Ethernet - TCP/IP` networks, switches rarely flood unicast
  - Before creating a packet, `ARP Broadcast` must be performed first to discover the MAC address of the terminal to communicate with, so ARP Broadcast reaches the network before Unicast
    - During this ARP-based MAC address acquisition process, the switch can already **learn** the MAC addresses of both communicating source and destination, and when actual unicast communication begins, it `forwards` and `filters` packets using the already created MAC Address Table
- ARP and MAC Tables are not deleted for a certain period, and this time is called **aging time**
  - Generally, the MAC Table's aging time is longer than the terminal's ARP aging time, allowing Ethernet networks to operate efficiently without flooding
