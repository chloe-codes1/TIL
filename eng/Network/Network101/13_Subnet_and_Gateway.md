# Subnet and Gateway

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

- Early networks were designed considering local networks (LANs) where all terminals existed in a single network, making the communication method very simple
  - With the development of Internet technology, small LAN networks were combined into one large network, and **communication with other LANs at distant locations** became important
- **Communication within the same network** and **communication between remote networks** differ in both operation methods and required network equipment
  - The equipment used for communication with remote networks is called a **Gateway**, and Layer 3 devices (`routers` and `switches`) can fulfill this role

<br>

<br>

## 1. Purpose of Subnet and Gateway

- In a Local network, `ARP Broadcast` can be used to learn the destination MAC address and communicate directly using that MAC address,
  - But remote network communication requires the help of network equipment because `broadcast` cannot be transmitted beyond the network
    - This equipment is called the **Gateway**,
    - And the configuration item for setting gateway information on PCs and network devices is called the **Default Gateway**
      - The **Default Gateway** is performed by a `Layer 3 device`,
      - And plays the role of **designating appropriate paths** while connecting with multiple networks
- Whether the source and destination are in the **same LAN** or **different networks** changes the communication method, so the source must verify whether the destination is **within its own network range**
  - The **Subnet mask** is used for this purpose
    - The method to find your own network is to perform an **AND operation** on `your IP address` and the `Subnet mask`
      - If the **destination belongs** to this computed **local network address**, it is `Local communication`; otherwise, it is `Remote communication`
  - In other words, the subnet mask is used to distinguish between communication within the same network and communication between different networks

<br>

### Proxy-ARP

- Proxy ARP is literally a feature that **acts as a proxy for ARP**
- `Remote communication` requires sending ARP requests to the **Default gateway** and sending packets toward the default gateway to communicate
  - However, if **Proxy ARP** is enabled on the Default gateway, even for remote communication, `ARP broadcast` can be sent to the local network for communication
- A `default gateway (router)` with **Proxy ARP** enabled will **respond to ARP on behalf** when an ARP broadcast comes in
  - In this case, the `packet` is sent toward the default gateway, so it can be forwarded to the remote path
- The **Proxy ARP** feature is enabled by default on routers and often operates without the user's knowledge
  - While it may seem convenient to operate automatically without user configuration, it often operates even when there are configuration errors in the network or essential settings are missing, making it a failure factor that prevents easy resolution during outages
    - ex) For remote communication,
      - If a `router` with Proxy ARP enabled is operating, it will accept and process even wrong ARP requests, so communication may work even if the Default gateway is incorrectly entered on the PC!

<br>

<br>

## 2. Layer 2 Communication vs Layer 3 Communication

- Layer 2 communication is **Local Network communication**, and Layer 3 communication is **Remote Network communication**
- Communication between terminals starts from the application layer and goes through **Encapsulation** and **Decapsulation**,
  - For direct communication in a Local Network (when source and destination are in the same network), communication is possible without the help of Layer 3 network devices like **routers**
    - Network devices connecting terminals only check information up to Layer 2 for communication, and `ARP requests` are sent using `broadcast` directly, so this is called **Layer 2 communication**
  - On the other hand, when communicating with a remote Network (when source and destination are in different networks), communication is impossible without the help of Layer 3 devices like **routers**
    - Network devices forwarding the `packet` must check up to Layer 3 information, and this is called **Layer 3 communication**
- The communication method changes based on whether the source and destination networks are **"the same"** or **"different"**, and this difference arises from the different `ARP operation methods` for Local and Remote communication
  - Communication between terminals in the same network occurs directly
    - `ARP Broadcast` is used to discover the other party's MAC address,
    - And as soon as the MAC address is discovered, packets are **encapsulated** and communication begins
  - When communication with an external network is needed,
    - The terminal determines that **the destination is at a location it cannot reach directly** and sends the ARP request to the Default gateway's IP address
    - After receiving the ARP response from the Gateway, the terminal writes the Default gateway's MAC address as the destination MAC address and starts communication
- In Local communication (L2 communication), the destination MAC address and destination IP address match,
  - In Remote communication (L3 communication), the destination MAC address and destination IP address differ
    - The destination IP address is the **actual destination** of the communication,
    - The destination MAC address is the **default gateway's MAC address**
