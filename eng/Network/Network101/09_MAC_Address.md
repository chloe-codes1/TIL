# MAC Address

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

### 1. MAC Address

- MAC address stands for Media Access Control and is a **unique identifier** assigned to NICs for communication at **Layer 2 (Data Link Layer)**
- MAC addresses are used as **Layer 2 addresses** in most **IEEE 802 network technologies** including `Ethernet` and `WiFi`
- Every device connecting to a Network must have a **physical address** called a `MAC address`, and devices **communicate** using this address

<br>

<br>

### 2. MAC Address System

- MAC addresses are fixed in hardware so they cannot be changed when shipped, so each network component has a different address
  - Each network device manufacturer has one or more **address pools**, and within those pools, each manufacturer **assigns** MAC addresses when devices are **shipped**
    - The allocation of address pools to network device manufacturers is called **Vendor Code**, and these addresses are **managed** by the international organization **IEEE**
- MAC addresses are expressed as **48-bit hexadecimal 12 digits**
  - The 48-bit MAC address is further divided into the first 24 bits and the last 24 bits
    - The first 24 bits are the aforementioned **Vendor Code**, called **OUI (Organizational Unique Identifier)**
    - The last 24 bits are called **UAA (Universally Administered Address)**, **independently assigned** by each manufacturer to distinguish each device in the network
- Since they are **determined in hardware at production**, MAC addresses are also called `BIA (Burned-In Address)`

<br>

#### 2-1. Non-unique MAC Addresses

- MAC addresses are commonly thought to be unique values, but **they may not be unique**
  - Network manufacturers assign the `UAA` value within their manufacturer code, but MAC addresses may be **duplicated** either by **mistake** or **intentionally**
- MAC addresses operate without issues **as long as they are not duplicated within the same network**
  - When communicating across networks using a `router`, the source and destination MAC addresses are **changed** when the `router` **forwards to another network**, so MAC addresses from the original source and destination are not maintained across networks

<br>

#### 2-2. Changing MAC Addresses

- MAC addresses are assigned to NICs in a **BIA (Burned-In Address)** state
- They are generally fixed in **ROM (Read Only Memory)** at shipment, so it is **difficult to change** the MAC address fixed on the NIC
- However, since MAC addresses are also loaded into memory for operation, the NIC can be operated with a changed MAC address using various methods
  - ex)
    - On Windows, if the **Driver details** provide MAC address change functionality, it can be easily changed
    - On Linux, MAC address changes are possible through **GNU MacChanger** or by **entering the MAC address** in each distro's **network configuration file**

<br>

<br>

### 3. MAC Address Operation

- NICs have their own MAC addresses, and when an electrical signal comes in, it is converted to **data form (packet)** at **Layer 2 (Data Link Layer)**, the contents are distinguished, and the **destination MAC address** is checked
  - If the destination MAC address is different from the NIC's own MAC address, the `packet` is **discarded**
  - If the packet's destination address is itself or a **group address** like `broadcast` or `multicast`, it recognizes it as an address to process and passes the packet information to the **upper layer**

<br>

#### 3-1. Promiscuous Mode

- By default, the NIC operation discards packets with destination addresses that do not match its own MAC address
  - When monitoring, debugging, or analyzing network status requires collecting and analyzing all packets across the network, the NIC's normal operation prevents analysis of packets destined for others
- When packets destined for others need to be **analyzed** or **collected**, the NIC is configured in **promiscuous mode**
  - Promiscuous mode allows packets **unrelated to its own MAC address** to be **loaded into memory for processing**
- A representative application using promiscuous mode is the **network packet analysis application** `Wireshark`

<br>

#### 3-2. Cases of Having Multiple MAC Addresses

- MAC addresses are **not tied to the terminal but to the NIC**
  - A terminal can have multiple NICs, so it can have multiple MAC addresses
- Complex network devices like `Multi-layer switches` and `routers` have multiple NICs and multiple assigned MAC addresses
