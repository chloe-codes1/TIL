# Network Glossary

> Efforts to become a Network expert

<br>

<br>

### 1. STP (Spanning Tree Protocol)

- A protocol to prevent **looping** that occurs in **Switches** or **Bridges**
- In Switch or Bridge configurations, if there are **two or more** paths from source to destination, only one path is kept and the rest are **disconnected**; when a **problem occurs** with the active path, the disconnected paths are brought back one by one

<br>

### 2. Spine-leaf architecture

- Composed of 2 switching layers: **spine** and **leaf**
  - The `leaf` layer aggregates traffic from servers
  - Consists of `access switches` that connect directly to the **spine** or **network core**
  - `Spine switches` connect all **leaf switches**
  - `Leaf switches` are mounted in **racks** and are responsible for server communication within that rack
- Proposed to support recent traffic trends of increasing server-to-server communication

<br>

### 3. ToR (Top of Rack)

- A switch placed at the top of a server rack where servers are installed
- A switch deployed to **handle traffic** for the servers installed in that rack

<br>

### 4. packet

- A portmanteau of package and bucket; a **bundled unit** of data **cut for easy transmission** through a communication network
  - Represents the size of data to be transmitted at once
- A packet consists of a **header**, **data**, and **trailer**
  - The `header` contains the recipient's internet **address** and **sequence** information
  - The `trailer` contains **error information**

- Generally, the data unit at Layers 3~4 is defined as a **packet**, and the data unit at Layers 1~2 is called a **frame**

<br>

### 5. NIC (Network Interface Card)

- A **card** or **interface** that **connects** a PC or server to the **network**
- Terms used to refer to NIC include (quite diverse..):
  - `Network Interface Controller`
  - `Network Card`
  - `LAN Card`
    - In the past, Ethernet was only used in LANs (Local Area Networks), so the Network Interface Card came to be called a LAN Card!
  - `Physical Network Interface`
    - Emphasizes the meaning of a physical **intermediary point** **connecting** the inside and outside of a computer
    - Using this term can cause NIC to be mistaken as a Layer 1 (Physical Layer) component, but NIC is a Layer 2 (Data Link Layer) component!
  - `Ethernet Card`
    - Since most networks are made of Ethernet, NICs connecting to Ethernet are used for general network connections, hence the name Ethernet Card
  - `Network Adaptor`

<br>

### 6. Sequence Number

- When splitting packets at Layer 4, the sending order noted in the `packet header` is the **Sequence Number**
- Also called `seq` or `sequence number`

<br>

### 7. ACK (Acknowledgement) Number

- When splitting packets at Layer 4, the receiving order noted in the `packet header` is the **ACK Number**
- Also called `ack number` or `acknowledgement number`

<br>

### 8. MSS (Maximum Segment Size)

- When an application creates and sends data, the `data flow layer` properly splits the data to match network conditions and delivers it to the other party
  - The value that **reverse-calculates from the size the network can accommodate** to **induce data to be split into appropriate sizes** when it comes down to Layer 4 is called `MSS (Maximum Segment Size)`
- MSS is the **maximum data value** that can be held at `Layer 4`

<br>

### 9. MTU (Maximum Transmission Unit)

- The size of **data that can be sent at once** in a network is called `MTU (Maximum Transmission Unit)`

  - The typical size that regular Ethernet can accommodate is 1,500 bytes

- MTU is the **maximum data value** that can be held at `Layer 2`

  - At Layer 2, the size of data excluding **Layer 2 header sizes** is called the MTU size

- Since the standard header sizes of Layer 3's `IP header` and Layer 4's `TCP header` are each 20 bytes, regular Ethernet uses an MSS value of 1,460 bytes

  ```
  MTU (1,500 bytes) = IP header (20 bytes) + TCP header (20 bytes) + MSS (1,460 bytes)
  ```

<br>

### 10. PDU (Protocol Data Unit)

- The part combining **header and data** at each layer is called `PDU`
- The name for PDU differs by Layer
  - Layer 1 (`Physical Layer`): **Bits**
  - Layer 2 (`Data Link Layer`): **Frame**
  - Layer 3 (`Network Layer`): **Packet**
  - Layer 4 (`Transport Layer`): **Segment**
  - Layer 5 (`Session Layer`): **Data**
  - Layer 6 (`Presentation Layer`): **Data**
  - Layer 7 (`Application Layer`): **Data**

<br>

### 11. BPDU (Bridge Protocol Data Unit)

- Frame data for information exchange between Switches (Bridges)
  - Becomes the data for `STP (Spanning Tree Protocol)` to prevent **network loops** that can occur within a network
- Provides the information needed for STP to construct a **loop free leaf** topology
- When a Switch (Bridge) boots, it sends `BPDU` out of each port every 2 seconds, exchanging STP information with each other
  - In other words, Bridges exchange `BPDU` with each other to determine who is the root bridge, which port is the root port, and which port will be the designated port

<br>

### 12. SSL (Secure Socket Layer)

- A cryptographic protocol designed to provide communication security for Networks
- Applied to communications using TCP/IP networks such as the Internet
- Ensures **security** and **integrity** between Transport Layer (L4) endpoints during communication
- Protocols such as `HTTP`, `FTP`, `TELNET` are combined with security protocols like SSL to create `HTTPS`, `SFTP`, `SSH` and similar protocols

<br>

### 13. TLS (Transport Layer Security)

- An upgraded version of SSL
- HTTP using encrypted connections via TLS is called HTTPS (secure)
  - Uses port 443 instead of the default port 80
- **TLS and HTTPS**
- TLS
  - A protocol for various types of secure communication
  - Covers not only HTTP but also protocols like FTP and SMTP
- HTTPS
  - A protocol for secured HTTP communication by layering the HTTP protocol on top of TLS
  - Refers only to the combination of TLS and HTTP protocols

<br>

### 14. SSID (Service Set Identifier)

- An identifier under the IEEE 802.11 wireless networking standard that indicates the **service set** (Network) to connect to
  - Displayed when using the Internet through a WiFi module
  - Acts as an **ID** that distinguishes one wireless LAN from another
- Designed with unique names to distinguish among WiFi networks in a given area
- Creation rules
  - Maximum 32 characters (32 bytes)
  - Case-sensitive
  - Some special characters can be used
    - ?, ", $, [, \, ], and +.
  - The following characters cannot appear at the beginning
    - !, #, and ;
