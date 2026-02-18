# Protocol

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

### Before getting started

- The term **protocol** is used when referring to rules/conventions
- In networking, the term protocol is also used to refer to **communication rules**

<br>

<br>

### Protocol

- **Physical aspect**
  - Data transmission media, signal conventions, line specifications, etc.
  - `Ethernet` is widely used
- **Logical aspect**
  - Protocol specifications for devices to communicate with each other
  - `TCP/IP` is widely used

<br>

#### Bit-based protocol

- `Protocols` were mostly developed based on **binary bits** to use small amounts of data efficiently
  - Strict agreements were made to transmit content with the minimum number of bits, and communication was only possible when these agreements were strictly followed

<br>

#### Application level protocol

- `Application level protocols` widely use character-based protocols rather than bit-based ones
  - **HTTP** and **SMTP** are representative protocols
  - Instead of transmitting messages in bits, they use characters to represent and transmit **headers**, **header values**, and **data**
  - While less efficient than bit-based protocols, they are defined in characters, allowing free header definition and **extensibility**

<br>

#### Protocol stack

- Generally, `TCP/IP` is called a **protocol stack** rather than a protocol

  - **TCP** and **IP** are protocols that operate on separate layers, but since they are used together, such a bundle of protocols is called a protocol stack
  - The **TCP/IP** protocol stack includes not only TCP and IP but also a wide variety of **application layer protocols** such as `UTP`, `ICMP`, `ARP`, `HTTP`, `SMTP`, and `FTP`

- The TCP/IP protocol stack is divided into the following 4 parts

  - **Physical layer**

    - Ethernet

  - **Network layer**

    - Helps data find its way to the destination

  - **Transport layer**

    - Helps properly assemble split `packets` into data form

  - **Application layer**
