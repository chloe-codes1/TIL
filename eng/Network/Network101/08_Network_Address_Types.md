# Network Address Types

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

The **communication methods** used when transmitting data from source to destination in a Network include `Unicast`, `Broadcast`, `Multicast`, and `Anycast`

<br>

### 1. Unicast

- A **1:1** communication method where the source and destination are **clearly defined as one each**
- **Most communications** actually used are `Unicast`

<br>

### 2. Broadcast

- A **1:all** communication method where the destination address is marked as **all**
- Before communicating via `Unicast`, it is mainly used to find the **exact location** of the other party
- `Broadcast` can be classified in various ways depending on the address system, but the basic operation is used when **all hosts in the Local network** need to receive the packet

<br>

### 3. Multicast

- A **1:group** communication method for transmitting packets to **multiple hosts belonging to a group** using a **Multicast group address**
  - Here, group refers to a multicast subscription host group
- The `multicast` communication method is used when watching real-time broadcasts like IPTV
- It is used when **one-directional** **simultaneous delivery of the same content** to **multiple parties** is needed, such as company broadcasts or stock price transmissions

<br>

### 4. Anycast

- A communication method that communicates with the host that is **closest or most efficient** to service among hosts with the same Anycast **address**
  - A **1:1** communication method where the destination is 1 host within the same group
- Using the **gateway** property of `Anycast`, it is used to **find the closest DNS server** or for `anycast gateway` functions to find the **closest gateway**
- **Final communication** is 1:1 making `unicast` and `anycast` identical, but the **candidates for communication** are different
  - `Unicast` has one source and one destination,
  - `Anycast` has servers with the **same destination address** as multiple **possible communication candidates**

<br>

### Communication Methods Summary

| Type          | Communication Target | Scope                  | IPv4 | IPv6 | Example |
| ------------- | -------------------- | ---------------------- | ---- | ---- | ------- |
| **Unicast**   | 1 : 1                | Entire network         | O    | O    | HTTP    |
| **Broadcast** | 1 : All              | Subnet (local network) | O    | X    | ARP     |
| **Multicast** | 1 : Group            | Defined scope          | O    | O    | Broadcast |
| **Anycast**   | 1 : 1                | Entire network         | △    | O    | DNS     |

- The currently predominantly used network address system is **IPv4-based**
  - Some mobile networks and large-scale data centers are adopting the new **IPv6**-based address system
  - In **IPv6**, `Broadcast` does not exist and is replaced by **link local multicast**
- When distinguishing communication methods, the important thing is that they are **classified based on the destination address**, not the actual source that delivers the data

<br>

<br>

`+`

### BUM Traffic

- BUM in BUM Traffic stands for **B (Broadcast)**, **U (Unknown Unicast)**, **M (Multicast)**
  - B, U, and M are different types of traffic, but their **behavior in the network is similar**
- `Unknown Unicast` is unicast, so the **destination address is clearly specified**, but the **behavior in the network** is the same as `Broadcast`
  - When a `Switch` has not learned the **destination address** (unknown from the switch's perspective), it **floods** the packet to all ports -- this unicast is called `unknown unicast`
- BUM Traffic is important because although it is `unicast`, its actual visible behavior is closer to `broadcast`
  - Of course, since it is `unicast`, **all receiving terminal NICs (Network Interface Cards)** will **check the destination address** and **discard the packet** since they are not the intended destination
  - However, from the network's perspective, it **unnecessarily uses network resources**, so if **unnecessary BUM Traffic** increases in the network, **performance may degrade**!
- In `Ethernet` environments, **ARP Broadcast** is sent first before communication begins, so BUM Traffic does not occur frequently
