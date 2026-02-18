# Router

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

## 1. What is Router?

- A `Router` is the representative device among various network devices operating at **Layer 3**, and as its name suggests, it is a device that **designates routes**
- The `Router` checks the **destination IP address** of incoming packets and uses its route (`Route`) information to **forward** packets through the **optimal path**
- The `Router` is an essential network device for connecting to **remote networks** and is a core device for network configuration
  - A `router` is absolutely necessary for communication between different networks!

<br>

### Router vs L3 Switch

- `Switches` are representative Layer 2 devices, but `L3 Switches` that operate at Layer 3 like routers are also widely used
- Previously, Routers were implemented in software and switches in hardware, or distinguished by feature-rich routers versus switches optimized for fast packet delivery
  - Recently, with technological advances, it is difficult to distinguish between `Router` and `L3 switch`
    - The content in this document is explained using routers, but everything applies equally to L3 switches!

<br>

<br>

## 2. How Does a Router Work?

- A `Router` collects **various route information**, stores the **optimal routes** in its `routing table`,
  - When a `packet` arrives at the router, it compares the destination IP address with the routing table and sends it through the best route
- Opposite to a Switch, a router **drops packets** whose **destination address** is not in the routing table
- The Router **removes existing Layer 2 header information** during the packet forwarding process and creates **new Layer 2 headers**
- The above router operation is called `Route designation`, `Broadcast control`, and `Protocol conversion`

<br>

### 2-1. Route Designation

- The Router's most important role is **route designation**
  - It gathers route information to build a `routing table` and **forwards** `packets`
    - IP addresses are designed based on a hierarchical structure divided into `network address` and `host address`, enabling distinction between local and remote networks, and allowing routes to be found based on network addresses
    - The Router checks these IP addresses and forwards packets to appropriate routes for remote destinations
- The Router separates its role of designating routes and forwarding packets into two functions:
  1. The role of obtaining route information, and
  2. The role of checking obtained route information and forwarding packets
- The Router **only forwards packets whose routes are included in its obtained route information**, so obtaining accurate destination routes is very important

<br>

#### How Routers Obtain Route Information

- Naturally obtaining adjacent network information when entering IP addresses
- Administrators directly entering route information
- Routers automatically exchanging route information with each other

<br>

<br>

### 2-2. Broadcast Control

- `Switches` **flood** packets to all ports when the packet's **destination information** is unknown, for communication with devices that may exist somewhere
  - While flooding to the entire LAN network under the assumption that a destination may exist somewhere might seem like it could strain overall network performance with useless packets,
    - LANs are small in size so **the impact of flooding is small**,
    - And since the destination network interface card (NIC) **discards packets when its address doesn't match** the packet's destination address, such flooding **does not significantly burden the network**
- In contrast, `Routers` were developed with the goal of **sending packets to remote locations**, operating at **Layer 3**, and only allowing communication with **clear destination information**
  - Internet connections mostly rent specific bandwidth, so efforts are made to minimize **useless communications occupying the network**
    - If, like switches in LANs,
      - Packets without destinations or
      - With unclear destinations were flooded,
    - The Internet would be filled with useless packets, reaching a **communication-impossible** state
- `Routers` **cannot forward packets** without route acquisition configuration beyond **directly connected network information**
  - The Router's default behavior does not acquire `multicast information` and does not forward `broadcast packets`
    - Using this Router function, **broadcast propagation to other networks** can be prevented
      - This function is called `Broadcast / Multicast Control`
  - When much broadcast occurs on a network, separating networks with a router can divide the broadcast network and improve network **performance**

<br>

<br>

### 2-3. Protocol Conversion

- Another role of the `Router` is **connecting** networks configured with **different protocols**
- Since modern networks have converged on `Ethernet`, the role of protocol conversion has diminished, but in the past, the protocols used in LAN and WAN were completely different, separate spaces
  - LAN focused on multiple computers communicating with each other, while WAN focused on long-distance communication
  - LAN technology had to be **converted** to WAN technology for communication with **remote networks like the Internet**, and `Routers` handled this role
- The `Router` is a device operating at Layer 3, so it checks Layer 3 address information and operates based on it
  - When a packet enters the Router, it **strips** the `Layer 2 header information`, **checks** the `Layer 3 address`, then **creates** new `Layer 2 header information` and sends it out
    - This is why the Layer 2 header information of a packet entering the router differs from when it leaves
    - Using this function, conversion between completely different technologies is possible!

<br>

<br>

## 3. Route Designation - Routing/Switching

- When a Router processes packets, it performs two main tasks:
  1. Obtaining route information and **organizing route information**
  2. Based on organized route information, **forwarding packets**
- Since a Router drops packets with destinations it doesn't clearly know, **route information must be sufficiently collected** before packets arrive for the router to operate normally
  - The Router must obtain complex and numerous route information to appropriately maintain the **optimal route information** in its `routing table`
- A Router can obtain diverse and numerous route information, but cases where it does not exactly match the desired destination information are more common
  - The Router acquires routing information in **subnet units** and performs `summary work` to **bundle** multiple subnet information together for **optimized** routing information transmission
    - So even if the packet's destination address entering the router does not **exactly match** the routing table information (not exact match), the **closest information** to the destination must be found among numerous entries to forward the packet

<br>

### 3-1. Routing Operation and Routing Table

- In modern networks, instead of being responsible for the entire path from terminal to destination, only the route to the **adjacent router** needs to be specified,
  - The adjacent router then finds the optimal route,
  - And forwards the packet to the next router
- This technique is called `Hop by Hop routing` since it jumps over the network one step at a time, and the adjacent router is called the `Next Hop`
  - The Router does not figure out the entire path to the destination but selects and sends to the optimal `next hop`

<br>

#### Methods for Specifying `Next Hop`

1. Specify the next router's IP (Next hop IP address)
2. Specify the Router's `outbound interface`
3. Simultaneously specify both the Router's `outbound interface` and next router's IP

<br>

- When specifying the next hop on a Router, the common method is to specify the `Interface IP address` of the **other router**
- Only in special cases can the router's `outbound interface` be specified; this can only be used when the other party's **MAC address information** can be discovered even without knowing the `next hop IP`
  - Special cases:
    1. When using protocols like `PPP (Point-to-Point)` or `HDLC (High Level Datalink Control)` in WAN dedicated line sections, where **the other party's MAC address doesn't need to be known**
    2. When proxy ARP is running on the other router, allowing the other party's MAC address to be known even without the exact IP address
       - What is ARP?
         - Address Resolution Protocol
         - A protocol used to discover the other party's MAC address
- When a Router selects which route to forward a packet, **it does not consider the source**
  - Regardless of the source, it compares the **destination address** with the **routing table** to decide which route to forward to
    - So when building the routing table:
      - Only **destination information is collected**,
      - When a packet arrives, the destination address is checked,
      - And the packet is **forwarded to the next hop**

<br>

#### Data Stored in the Routing Table

1. Destination address
2. Next hop IP address, local outbound interface (optional!)

- The `PBR (Policy-Based Routing)` feature can be used on a Router to route using the packet's source address, but this cannot be activated with the routing table that only collects destination addresses; separate configuration related to router policies is needed
  - Using PBR makes management difficult and problems hard to resolve, so it is only used for special purposes

<br>

#### Loop Free Layer 3: TTL (Time To Live)

- The Layer 3 IP header has a field called `TTL`
  - This field limits the time (Hops) a packet can live in the network!
- To prevent useless packets from wandering around the Internet and wasting bandwidth, routers **drop packets with unclear addresses**
- However, there can be cases where an operating site suddenly disappears, and while searching for alternative routes, the next hops of two facing routers may momentarily be configured as each other, causing packets to continuously bounce between the two routers
  - In this case, incorrect routing between the two routers creates an **L3 Loop**
- If packets never permanently disappear, identical packets would ping-pong between devices or ghost packets that never disappear would flood the Internet
  - Therefore, all packets have a lifespan value called **TTL**, and when this value reaches 0, the packet is dropped by the network device
- Here, `TTL` is not actual time like seconds, but refers to `hops`, and the TTL value decreases by 1 **with each hop**

<br>

<br>

### 3-2. Routing (How Routers Obtain Route Information)

Routers obtain route information through 3 main methods:

1. `Direct Connected`
2. `Static Routing`
3. `Dynamic Routing`

Route information is collected using the above 3 methods, and the **optimal route** for each destination is selected from the collected information to build the `Routing Table`

 <br>

#### 1. Direct Connected

- The **IP address** and **Subnet mask** used when entering an IP address can determine the **Network address information** that IP belongs to
  - Routers and PCs automatically create the Routing Table for that Network using this information
    - This route information is called `Direct Connected`
- Since the route information created by `Direct Connected` is **automatically generated** when an IP is configured on an Interface,
  - The information **cannot be forcibly deleted**,
  - And only **automatically disappears** when the Network configuration is deleted or the Network Interface is **deactivated**

<br>

#### 2. Static Routing

- When an administrator **directly specifies** the `destination Network` and `Next hop` on the router to **enter route information**, it is called `Static Routing`
  - `Static Routing` allows very **intuitive** configuration and management of routing information since the administrator directly specifies routes
- `Static Routing`, like `Direct Connected`, **automatically deletes associated Static Routing information** when the connected Network Interface information is deleted or deactivated
  - However, Logical Interfaces, unlike Physical Interfaces, may not be deactivated when the Physical Interface is deactivated, so they may not disappear from the Routing Table

<br>

#### 3. Dynamic Routing

- `Static Routing` is a good method for administrators to easily manage networks with few changes, but large networks are difficult to manage with `Static Routing` alone
  - Why?
    - Route changes due to **failures cannot be reflected** with `Static Routing`!
      - Because `Static Routing` **cannot assess the status of routers beyond the current router**, if a failure occurs in lines between routers or in a router itself, **it cannot detect the failure and send packets through alternate routes**!
- `Dynamic Routing` compensates for this weakness of `Static Routing` by having **routers exchange their known route information or link status information** to learn the entire network
  - Since route information is exchanged periodically or when status changes, when failures occur in lines connecting routers or in routers themselves, the situation is recognized and **packets can be forwarded through alternate routes**
- In `Dynamic Routing`, the **network to advertise must be declared**
