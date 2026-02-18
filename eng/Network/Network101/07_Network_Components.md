# Network Components

> Let's learn about the components needed to build and use a network
>
> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

## 1. Network Interface Card (NIC)

- The official name for what is commonly called a `LAN card` is **Network Interface Card (NIC)**
  - Besides NIC, it is also called `Network Card` or `Network Interface Controller`
- NIC is a **hardware device** for connecting a **computer** to a **network**

<br>

### Main Roles of NIC

- **Serialization**
  - The Network Interface Card **converts** **electrical signals** to **data signal form** or **data signal form** to **electrical signal form**
  - On the external cable of the NIC, data is transmitted in **electrical signal** form, and this **mutual conversion** process is called `serialization`
- **MAC Address**
  - The Network Interface Card has a MAC address
  - If the **destination address of a received packet** is not its own MAC address, it **discards** the packet; if it is its own address, it **forwards** it so it can be processed within the system
- **Flow Control**
  - In `Packet`-based networks, various communications use **a single channel**, so new data may not be received because of ongoing data processing
    - To prevent **data loss** in such situations, when **data cannot be received**, a **request to stop communication** can be sent to the other party, and this process is called `flow control`

<br>

### Multifunction NIC

- `Ethernet` is not the only network transmission technology used
  - The **Fibre Channel** standard exists for `SAN (Storage Area Network)` configurations connecting **Storage** and **servers**,
  - The **iSCSI protocol** exists for configuring storage networks over `Ethernet`
  - **InfiniBand** technology is also used in **HPC (High Performance Computing)** networks that implement high-performance clustering by linking multiple servers, like `supercomputers`
- Recently, these various protocols have been transitioning to `Ethernet`-based,
  - But these various protocols are still used in some networks
  - Network cards that support and accelerate these special networks are also being used

<br>

<br>

## 2. Cable and Connector

- While the use of **wireless** connections from laptops, smartphones, and tablets for Internet access is increasing, **wired** connections are still used when **high-reliability communication** is needed, such as connecting to company networks or connecting servers to the network
  - The first network connection point to consider for such connections is the **cable**
- **Cables** come in 3 types: `Twisted Pair`, `Coaxial cable`, and `Fiber-optic cable`
  - To correctly select the right cable for the desired environment, you need to know the **basic elements** and **standards** that make up the cable

<br>

### 2-1. Ethernet Network Standards

- Currently popular Ethernet standards are **Gigabit Ethernet** and **10 Gigabit Ethernet**
  - General terminals like PCs use Gigabit Ethernet, while terminals like data center servers primarily use Gigabit or 10 Gigabit Ethernet
  - When connecting servers and switches with 10 Gigabit Ethernet, switches use **40 Gigabit** or **100 Gigabit** Ethernet to secure **uplink bandwidth** for connections with upstream switches
- Ethernet is further subdivided into multiple standards by **cable type**, **encoder type**, etc., but 3 standards are most commonly used
  1. **1,000BASE-T/10GBASE-T**
     - Gigabit Ethernet standard using `Twisted pair cable`
  2. **1,000BASE-SX/10GBASE-SR**
     - Uses `Multi-mode optical cable` and can transmit over **relatively short distances**
  3. **1,000BASE-LX/10GBASE-LR**
     - Uses `Single-mode optical cable` and can transmit over **relatively long distances**

<br>

Explaining the meaning of each nomenclature using **1,000BASE-T**, one of the Gigabit Ethernet standards,

- The number 1,000 at the front indicates **speed**
  - If the front number is 1,000, it is a network that can communicate at **1,000Mbps speed**
- The middle characters refer to the **type of channel**
  - `BASE` indicates **single-channel communication**,
  - `BROAD` indicates **multi-channel communication**
- The last characters indicate the **cable type**
  - The `T` character indicates **Twisted Pair cable**
  - The optical signal and transceiver type change based on the last character

<br>

### 2-2. Cable and Connector Structure

- Cables are physically divided into several elements like `cable body`, `connector`, and `transceiver`
  - The cable body is divided into **Twisted Pair**, **coaxial**, and **optical cables**
  - The **connector** and **transceiver** types also change depending on the cable body type
- For `Twisted Pair Cable`, the connector and body are configured as one, and there is often no separate transceiver
- `Optical cables` need to support various speeds and distances, so the transceiver, connector, and cable are often separated

<br>

### 2-3. Cable - Twisted Pair Cable

- The most commonly used cable is the `Twisted Pair` cable
- Twisted Pair cables use **RJ-45** connectors that are attached to the cable body and **cannot be separated**
- Plugging it into a **LAN port** on a computer or server connects it to the network
- **Types of Twisted Pair cables**
  - **STP (Shielded Twisted Pair)** cable with mesh-type shield
  - **FTP (Foil Twisted Pair)** cable with foil-type shield
  - **UTP (Unshielded Twisted Pair)** cable without shield
- Cables with shields on each twisted pair and cables with an overall cable protection shield may use **STP/FTP** combinations
  - **STP/FTP** has each pair shielded with foil and an overall cable protection shield
    - This can effectively block both **internal interference** and **external interference**!
- **Twisted Pair cable grades**
  - Twisted Pair cables are graded by `category`
  - The most commonly used cable is the **category 5E** cable
    - It is a common cable supporting **1G** speeds and is **suitable** for connecting **general terminals** like desktops and laptops,
    - But **not suitable** when **high bandwidth** like data centers needs to be supported

<br>

### 2-4. Cable - Coaxial Cable

- `Coaxial cables` are the same type as the thick black cables used to connect cable TV
- In the past they were also used in **LAN sections**, but since they are **hard to handle and expensive**, they are rarely used and have only been used for cable TV and Internet connections
  - However, recently for **10G or higher** **high-speed connections**, `DAC (Direct Attach Copper)` cables with **integrated transceivers** are widely used, which are a type of **coaxial cable**

<br>

### 2-5. Cable - Optical Cable

- Optical cables generally have higher **reliability** than other copper wires (`UTP`, `coaxial`) and can communicate over **longer distances**, so they are primarily used for communication between network devices that require **high bandwidth** or need to communicate over **long distances**
- Cables need to be protected from **attenuation** caused by **resistance** and **interference** from **surrounding magnetic fields**, and optical cables based on `optical signals` are **relatively free from such attenuation and interference**
- Optical cables are divided into 2 types: `Single mode` and `Multi mode`
  - `Single mode`
    - The **cable thickness is very thin** to support **long-distance communication**, and **laser** is used as the light source
      - Lasers have the property of traveling straight without dispersing over long distances compared to other light
    - Called single mode because a single laser signal passes through a thin transmission path
    - Single mode with a **small reflection angle** can transmit over **much longer distances**
    - Single mode cables are **yellow**
  - `Multi mode`
    - Uses a **relatively thicker cable** compared to single mode and uses **LED** as the light source
      - LED light sources are easier to implement than lasers, so both multi mode cables and transceivers are cheaper than single mode
    - Called multi mode because **multiple light sources** are transmitted through a wide optical transmission path
    - Multi mode cables are **orange (1G)** and **sky blue (10G)**

<br>

### 2-6. Connector

- The connector is the end part of the cable that connects to **network devices** or **network cards**
- Twisted Pair cables use `RJ-45` connectors, but optical cables have various connectors
  - Optical cables primarily use **LC connectors**, and **SC connectors** are partially used
  - When using optical cables for servers, the connector type must be communicated to the network administrator when requesting network connections to ensure the appropriate cable is used

<br>

### 2-7. Transceiver

- Transceivers convert **external signals** into **electrical signals** inside the computer
- In the past when transceivers were not separately distinguished, different network devices or NICs had to be purchased to satisfy various `Ethernet standards` and cables
  - To solve the problem of having to replace network devices and NICs when cables changed, and to allow the **mixed use** of different **diverse network standards**, transceivers are used
- Among transceivers, **GBIC** is the name of the initially developed module, and subsequent **upper standards** like **SFP** and **SFP+** were released, but
  - Generally, all transceivers are collectively referred to as **GBIC**
- To be precise,
  - **GBIC (GigaBit Interface Converter)** is an interface that can connect **SC type** connectors
    - SC type connectors are mainly used for optical cables
  - **SFP (Small Form-Factor Pluggable)** can connect **LC type** connectors

- **Without Transceivers**, using dedicated interfaces would require purchasing different network devices or NICs for each length and speed, but
  - By **only changing the Transceiver**, **communication length** and **speed** can be adjusted, so most recently produced network devices and NICs support transceivers

<br>

<br>

## 3. Hub

- Hub is a device that operates at **Layer 1 (Physical Layer)**, the same as cable
- Hub **regenerates** electrical signals that weaken with distance, and as the term HUB implies, is used to **connect** multiple devices
- Hub simply **sends incoming signals to all ports**, causing all terminals connected to the network to **compete**, resulting in problems of reduced overall network performance
  - **Infinite packet loops** can occur, paralyzing the entire network, and various **failure causes** like loops mean that hubs are **rarely used** today

<br>

<br>

## 4. Switch

- Switch, like Hub, is a **Layer 2 (Data Link Layer) device** that **connects multiple devices** and **mediates communication**
- Switch performs both the **role of a Hub** and **mediating communication**, so it is also called a **Switching Hub**
- Hub simply **regenerates electrical signals** and sends them to all ports except the source,
  - But Switch, unlike Hub, can **understand MAC addresses**, **identify the location of the destination MAC address**, and send electrical signals only to the port where the correct destination is connected
    - ex) When servers A, B, C, D exist and A needs to communicate with C,
      - `Hub` sends electrical signals to all ports B, C, D except the source port when A sends a signal,
      - `Switch` sends electrical signals only to C
        - B and D are completely unaffected by this communication and can **simultaneously** perform other communications
- `Hub` works like a **walkie-talkie** that cannot send and receive simultaneously and operates **in only one direction**,
- `Switch` works like a **telephone** that can send and receive **simultaneously**

<br>

<br>

## 5. Router

- As network sizes grew and the need to communicate with networks in **distant areas** increased, routers became necessary
- Router operates at **Layer 3 (Network Layer)** of the OSI 7 layers and converts to protocols that can communicate over **long distances**
- Router controls **broadcast** and **multicast** to prevent unnecessary packets from being transmitted to remote locations, and discards communications to **unclear addresses**
  - It designates **paths** so packets are transmitted in the **correct direction** and **forwards** packets through the **optimal path**
    - In other words, the router's role is to **verify the network address** and then **designate the path**
- Recently, it is difficult for general users to encounter Router devices, but `L3 Switches` and `home routers (shared routers)` that perform similar roles to routers can be easily found

<br>

<br>

## 6. Load Balancer

- Generally, Load Balancers operate at **Layer 4 (Transport Layer)** of the OSI 7 layers
- `Layer 7 Load Balancers` that understand and operate based on application protocol characteristics at the `application layer` are separately called **ADC (Application Delivery Controller)**
- Network devices called **L4 Switches** are also a type of load balancer, referring to devices that have **multiple ports** like a `switch` while performing the **load balancer role**
- Load Balancers can **check Layer 4 port addresses** while simultaneously **changing IP addresses**
- The service where Load Balancers are most commonly used is **Web**
  - When you want to **scale up** a web server, place a load balancer in front of the web servers and increase the number of web servers
    - The load balancer holds the **representative IP**, and the load balancer **changes** the **destination IP address of packets** to send them to each web server
  - Using this principle, multiple web servers operate simultaneously to **improve** service **performance**
  - Even if some web servers have problems, it helps **recover** service quickly
    - For these functions, load balancers have capabilities like **service health check** and **high-volume session processing** in addition to IP translation!

<br>

<br>

## 7. Security Devices (Firewall/IPS)

- While most network devices focus on **accurate information delivery**,
  - Security devices focus on properly **controlling** information and **defending against attacks**
- Various security devices are used according to the **defense purpose** and the **location where they are installed**
- Generally, the most well-known security device is the **Firewall**
  - `Firewalls` operate at **Layer 4 (Transport Layer)** of the OSI 7 layers, checking **Layer 3 and 4 information** of **packets** passing through,
  - And comparing packets against **policies** to either discard or forward them

<br>

<br>

## 8. Others (Modem/Home Router)

### 8-1. Home Router (Shared Router)

- The `home router` used in nearly every household or small business is a device that combines **Layer 2 switch**, **Layer 3 router**, and **Layer 4 NAT and firewall** functions in one place
- The inside of a home router is divided into `Switch section`, `Wireless section`, and `Router section` circuits
  - It looks like a single device on the outside, but internally it is a complex device broadly divided into **switch**, **wireless AP**, and **Router**

<br>

### 8-2. Modem

- A `Modem` is a device that **converts** between technologies because **short-distance communication technology** and **long-distance communication technology** are different
- Both the `LAN (Local Area Network)` port and `WAN (Wide Area Network)` port of a home router cannot send data farther than 100m over regular Ethernet, so a separate modem is needed to **convert** to **long-distance communication technology**
- Various types of modems are used depending on the carrier network type and technology
  - For `gigabit Internet`, mostly **FTTH (Fiber To The Home) modems** are used,
  - For `coaxial cable Internet`, **Cable modems**,
  - For `telephone lines`, **ADSL (Asymmetric Digital Subscriber Line) modems** or **VDSL (Very high bit-rate Digital Subscriber Line) modems** are used

<br>
