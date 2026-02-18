# VLAN

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

## 1. What is VLAN?

- A technology that **logically divides and configures** a LAN regardless of physical placement
  - A single `Switch` can be divided into multiple `VLANs`
    - They operate as separate switches
- As departments in companies need network separation and numerous terminals like smartphones and PCs connect to networks, **network segmentation** is important
  - **Why network segmentation is needed**
    1. **Performance degradation** of terminals due to **excessive broadcast**
    2. For security enhancement and blocking purposes
    3. Applying policies based on service characteristics
- When `VLANs` are separated, since a single device is **logically divided into different networks**, not only `Unicast` but also `Broadcast` **cannot communicate between VLANs**
  - If communication between `VLANs` is needed, it requires the help of Layer 3 devices since it is communication between different networks
- Using `VLANs`, networks can be separated **regardless of physical configuration**, and terminals on physically different floors can be **grouped into the same network** using a single `VLAN`
  - Communication between separated terminals occurs through `Layer 3 devices`

<br>

<br>

## 2. Types of VLANs

There are **port-based** VLANs and **MAC address-based** VLANs for `VLAN` assignment methods

<br>

### Port Based VLAN

- When VLANs were first introduced, switches were expensive and played the role of bundling multiple hubs, so using the switch for multiple networks by dividing it was the purpose of applying VLAN functionality
  - Using the switch's ports in a **logically divided** manner is called `Port Based VLAN`
    - Most VLANs we generally refer to are `Port Based VLANs`
  - Regardless of which terminal connects, assigning a **VLAN to a specific port** on the switch causes it to belong to that assigned VLAN

- In a switch configured with `Port Based VLAN`, the **VLAN assignment criterion is the Switch's port**
  - ex)
    - If PC AA connects to port 1, it belongs to VLAN 10; if connected to port 4, it belongs to VLAN 20

<br>

### MAC Based VLAN

- As user mobility increased, `MAC Based VLAN` based on **MAC Addresses** was developed
  - Using `MAC Based VLAN`, wired users remain in the same VLAN even when they move
- Rather than assigning VLANs to **fixed ports** on the Switch, it assigns VLANs based on the **terminal's MAC Address** connecting to the switch
- When a terminal connects, the switch recognizes the terminal's MAC Address and changes the port to the designated VLAN
  - Since VLAN information can change based on the terminal, it is also called `Dynamic VLAN`

- The **VLAN assignment criterion** for `MAC Based VLAN` is the **PC's MAC address**
  - ex)
    - PC AA is assigned the **same VLAN** regardless of **which switch or which port** it connects to

<br>

<br>

## 3. How VLAN Works (Trunk/Access)

- In `Port Based VLAN`, each **Switch port** is configured with a **VLAN to use**, and even if connected to a single switch, **ports with different VLANs cannot communicate**
  - Different `VLANs` mean being connected to **separate, isolated switches**, so inter-VLAN communication is impossible
    - Communication between different VLANs requires Layer 3 devices like `routers`
      - In networks segmented by `VLANs`, the broadcast **ARP Request** cannot be delivered to other VLANs, so communication must occur through Layer 3 devices
- **Separating networks by configuring VLANs** on switch ports allows more **efficient** use of equipment compared to physically separating switches
  - VLAN separation creates the effect of **multiple logical switches**
- When switches need to be interconnected in a situation with multiple VLANs, communicating between each VLAN requires **as many ports as VLANs**
  - A switch with divided VLANs is **treated as physically separate switches**
  - ex)
    - If one switch has 3 VLANs configured, **3 ports** are needed for each VLAN to communicate between switches
      - In medium/large networks using more VLANs, connecting by VLAN **wastes many ports** just for device interconnections
  - The `VLAN Tag feature` was created to solve this problem!

<br>

### Tagged Port (Trunk Port)

- The Tag feature allows **multiple VLANs to be transmitted together through a single port**
  - This port is called a `Tagged port` or `Trunk port`
- The `Tagged port` that must transmit multiple VLANs simultaneously inserts a **VLAN Field** in the middle of the **Ethernet Frame** during communication
  - When sending packets through the `Tagged Port`, a **VLAN ID** is **attached**, and the receiving side **removes** the **VLAN ID** and sends the packet to the corresponding VLAN
- Using `Tagged Ports` allows bundling the multiple ports previously needed for each VLAN's communication into one, enabling flexible network **design without port waste**
- With the `Tagged Port` feature added to switches, the **MAC Address Table** used for packet transmission also changed
  - A **field specifying VLAN** was added to the **MAC Address Table** to prevent communication between different VLANs!
    - When a network is separated using VLANs on a single switch, it operates as if **MAC Address Tables exist per VLAN**

- `Tagged Ports` are used to deliver multiple VLANs, meaning **multiple networks**, through **a single physical port**
- `Tagged Ports` are generally used for connections between switches that have **multiple networks configured simultaneously**
- When packets enter through a `Tagged Port`, they are **transmitted to the tagged VLAN side while stripping off the Tag**

<br>

### Untagged Port (Access Port)

- Regular ports are called `Untagged Port` or `Access Port`
- `Untagged Ports` are used only when belonging to **a single VLAN**
  - So typically, servers belonging to a single network are configured as `Untagged`

- When packets enter through an `Untagged Port`, they are transmitted only to the same VLAN

<br>

<br>

### Virtualized Servers

- Even server-connected ports, not just switch-to-switch connections, may need to communicate with **multiple VLANs** when connected to **virtualized servers**
  - In this case, even server-connected ports are configured as `Tagged` rather than `Untagged`
    - Since it is in Tagged state, the interface on the virtualized server side must also be configured in tagged state
  - Since a **virtual switch** exists inside the virtualized server, it is easier to understand when viewed as a **switch-to-switch connection**

<br>

<br>

### Inter-VLAN Communication

- VLANs prevent `unicast`, `multicast`, and `broadcast` from crossing VLAN boundaries due to the switch communication segmentation function
- Generally, different VLANs mean being **divided into separate networks**, so **different networks** with **different IP address assignments** is typical
  - If communication between different networks is needed, the help of **Layer 3 devices** like `routers` is required
