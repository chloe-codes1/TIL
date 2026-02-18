# TCP / UDP

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

- Layers 2 and 3 were aimed at **providing addresses** to accurately find the destination, but protocols operating at Layer 4 were created with a slightly different purpose than Layers 2 and 3
  - Among multiple application processes running inside the destination terminal, they accurately find the **destination process to communicate with**,
  - Properly **assemble** packets so their order is not mixed up,
  - And fulfill the role of properly reconstructing the **original data**

<br>

## 1. Layer 4 Protocol (TCP, UDP) and Service Port

- During the Encapsulation and Decapsulation process of sending and receiving data, headers are added at each layer with various information
  - Among the diverse information, the two most important pieces are:
    1. Information defined at each layer
       - Information for use by the same layer on the receiving side
    2. Upper protocol indicator information
       - Used for the purpose of accurately finding the upper layer protocol or process during the Decapsulation process
- In the `TCP/IP Protocol Stack`, Layer 4 is handled by TCP and UDP
  - Layer 4's purpose is to accurately find the process used by the application, properly split data into `packets`, send them well, and assemble them well
  - **Sequence Numbers** and **ACK Numbers** are used to split and assemble packets

- In the `TCP/IP Protocol Stack`, the upper protocol indicator is the **port** number
  - The Layer 4 protocol indicator, the port number, must be **processed by distinguishing source and destination**

<br>

#### Well Known Port

- Ports like HTTP TCP 80, HTTPS TCP 443, SMTP TCP 25 are called **Well Known** ports
- These ports are already registered with the Internet address allocation agency **IANA (Internet Assigned Numbers Authority)** and use port numbers **1023** and below
- To allocate port numbers to various applications, the **Registered Port** range is used
  - The range is `1024 ~ 49151`, and applying for a port number registers it with **IANA** for management
    - However, official and unofficial numbers are mixed, and they may be used as private port numbers
- The range for **dynamic**, **private**, **temporary** ports is `49152 ~ 65535`
  - Port numbers in this range are not registered with IANA
  - These port numbers are automatically allocated, assigned for private use, or used as temporary port numbers for clients!
- [Check IANA-managed Ports](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)

<br>

<br>

## 2. TCP

- TCP includes most of the characteristics of Layer 4
- TCP protocol ensures **lossless** communication even on unreliable public networks by
  - Safely establishing sessions,
  - Splitting data,
  - And having the ability to check whether split packets were transmitted successfully
- It assigns numbers (`Sequence Number`) to packets and responds (`Acknowledge Number`) regarding successful transmission
  - It also considers the transmission size (`Window Size`) to determine **how much to send at once** so the receiver can properly receive and process it
    - Thanks to TCP's role, networks can be used easily and safely without seriously considering network conditions

<br>

### 2-1. Packet Order and ACK Number

- In TCP, packets are given **sequence numbers** to properly split and allow the receiver to assemble them, along with **response numbers**
- Assigning **sequence** to Packets is called `Sequence Number`, and assigning **response numbers** is called `ACK Number`
  - These two numbers interact to detect when **order is mixed up** or packets are **lost** in transit

<br>

#### Basic Operation of `Sequence Number` and `ACK Number`

- The sender **assigns numbers** to packets and the receiver **checks whether the order is correct**

- If the received packet number is correct, a response is given requesting the next numbered packet
  - This number is called the `ACK Number`

- If the sender sends packet 1 and the receiver receives it successfully, it gives `ACK Number` 2 indicating "I received 1 well, please send 2 next"

ex)

1. The source sends `Sequence Number` as 0 (SEQ = 0)

2. The receiver responds with 1 in the response number (`ACK Number`) indicating packet 0 was well received

   At this time, since it is the first packet the receiver sends, it assigns `Sequence Number` 0 to its own packet

3. The sender that received this packet sets `Sequence Number` to 1 (because the receiver requested packet 1 via `ACK Number`!!)

   Sets `ACK Number` to 1 meaning it successfully received the other party's Sequence 0, and transmits again with Sequence Number 1!

<br>

### 2-2. Window Size & Sliding Window

- TCP does not unilaterally send packets but **checks ACK numbers** to see how well the other party **received** them and then **sends the next packet**
  - Receiving a separate packet to check if transmission was successful itself **increases communication time**, and if the sender and receiver are far apart, **Round Trip Time (RTT)** increases, making the **wait time for responses even longer**
    - If only one small packet could be sent and a response had to be received before sending another, it would take a very long time to transmit all data
    - So when sending data, not just one packet but **many packets are sent at once** and **only one response** is received
- While sending as many packets as possible at once is more efficient, if network conditions are poor, the possibility of **packet loss** increases, so an **appropriate transmission rate** must be determined
  - The amount of data that can be received at once is called `Window Size`,
  - Adjusting this window size based on network conditions is called `Sliding Window`
- The maximum size expressible in the TCP Header window size is **2^16**
  - In practice, the window size can be up to 64K, but this is too small for modern networks with **improved line stability** and **higher speeds**
    - So communication occurs with a **greatly increased** window size beyond 64K, but since **TCP headers cannot be changed**, the window size is increased by **ignoring the trailing digits** without increasing the header size
      - Using this method, the window becomes 10x, 100x larger than the original!
- TCP **halves** the window size when **data loss** occurs and gradually increases it by one during normal communication
  - If **network contention** occurs and `packet drop` happens, the reduced window size may cause data communication speed to slow down, failing to properly utilize the line
    - To avoid contention:
      1. Increase the line speed, or
      2. Use **network devices with larger buffers** that can temporarily avoid contention, or
      3. Use **TCP optimization solutions** to solve these problems

<br>

### 2-3. 3-Way Handshake

- In TCP, **preliminary connection work** is done before communication starts to ensure **lossless, safe communication**

  - If data is unilaterally transmitted when the destination is not ready to receive, the destination cannot process the data normally and **data is discarded**
  - To prevent this, the TCP protocol performs a preliminary check to verify whether data can be safely sent and received!

- In `Packet Networks`, since **many parties communicate simultaneously**, it is important to **pre-secure resources** needed for communication before actual communication

  - In TCP, this is called `3-Way Handshake` because **3 packets** are exchanged to **mutually prepare for communication**

- In TCP, the **state** information is named differently depending on the progress of the `3-Way Handshake`

  - The Server waits in a **LISTEN** state ready to accept client connections for service
  - When the Client initiates communication, it sends a `Syn` packet; this state on the client side is called **SYN-SENT**
  - The server receiving the Client's `Syn` changes to **SYN-RECEIVED** state and responds with `Syn`, `Ack`
  - The client receiving the response changes to **ESTABLISHED** state and sends a response to the server
  - The server also changes to **ESTABLISHED** state after receiving the client's `Ack` response
    - **ESTABLISHED** state indicates that the connection between server and client has been successfully completed!

  ![3-Way-Handshake](../../kor/Network/images/3-Way-Handshake.jpg)

- Due to the `3-Way Handshake` process, **Flags** are placed in headers to distinguish which packets are new connection attempts and which are responses to existing ones
  - **TCP Flags**
    - `SYN`
      - Used to initiate a connection
      - When a connection starts, the SYN Flag is set to 1
    - `ACK`
      - Set to 1 when the ACK number is valid
      - All packets other than the initial SYN are responses to existing messages, so the ACK flag is set to 1
    - `FIN`
      - Set to 1 when terminating a connection
      - Used for **normal bidirectional termination** after data transmission is complete
    - `RST`
      - Set to 1 when terminating a connection
      - Used to **forcefully terminate** a connection **unilaterally**
    - `URG`
      - Set to 1 for urgent data
    - `PSH`
      - Used when the server has no data to send or to instruct that data should be immediately delivered to the application without buffering

<br>

<br>

## 3. UDP

- Unlike TCP, UDP has almost none of the characteristics that a Layer 4 protocol should have
  - At Layer 4, the following tasks were performed for **reliable communication**:
    - **Pre-establishing connections (3-Way Handshake)**
    - Assigning `packet numbers` to properly **split** and **assemble** data, and responding for received data
    - Sending data in specific units (`Window Size`) and maintaining it in memory, then removing data from memory only after receiving `ACK Numbers` and confirming successful communication
    - If **loss** occurs mid-transmission, detecting it by comparing `Sequence Number` and `ACK Number`, and **retransmitting** using data maintained in memory
      - This function allows correction even if data loss occurs or order is mixed up
  - UDP has none of the above TCP features
- The UDP header has almost no content compared to TCP
  - UDP lacks the content for **reliable communication** characteristic of Layer 4 (`Sequence Number`, `ACK Number`, `Flag`, `Window Size`)

- The core of data communication is the **reliability** of data transmission
  - The purpose of data communication is for applications to create and use data without worry,
  - But UDP is a **protocol that does not guarantee data delivery**, so it is used only for limited purposes
- UDP is primarily used for **time-sensitive** protocols or applications like voice data or real-time streaming, or for `multicast` used in company broadcasts or stock price data transmission where **one-directional** communication with **multiple terminals** makes receiving responses difficult
  - For services like video conferencing systems where continuing transmission on schedule is more important than **reliability**, even if some data is lost, UDP is used
    - UDP processes data in its lost state even if some data is lost mid-transmission!
- Unlike TCP, UDP does not have a pre-connection establishment procedure like `3-Way Handshake` before communication starts
  - Instead, the **first data** in UDP is used as an **Interrupt** for resource provisioning and is lost
    - So most applications using UDP protocol are aware of this situation and operate accordingly,
    - Or TCP protocol is used for connection establishment, and after all preparations are complete between applications, only the actual data uses UDP
- ex)
  - Connections for individual viewers that are **not time-sensitive**, like Netflix or YouTube, use TCP
  - Real-time video conferencing solutions where data transmission occurs bidirectionally and is **very time-sensitive** use UDP, because in a TCP environment, data loss may make users perceive poor network quality

<br>

### TCP vs UDP

| TCP                               | UDP                           |
| --------------------------------- | ----------------------------- |
| Connection Oriented               | Connectionless                |
| Error control: Yes                | Error control: No             |
| Flow control: Yes                 | Flow control: No              |
| Unicast                           | Unicast, Multicast, Broadcast |
| Full Duplex                       | Half Duplex                   |
| Data transmission                 | Real-time traffic transmission |

<br>

`+`

#### Communication channels in telecommunications

- Simplex communication
  - One-directional transmission
  - ex) TV, Radio
- Half-duplex communication
  - Bidirectional transmission is possible, but both sides cannot transmit simultaneously
  - ex) Walkie-talkie
- Full-duplex communication
  - Simultaneous bidirectional transmission is possible
  - ex) Telephone
