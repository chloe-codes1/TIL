# STP

> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

- In IT environments, various efforts are made to avoid failures caused by `SPoF (Single Point of Failure)`
  - `SPoF` refers to an element where a **failure** in a **single** system or component causes the **entire system** to stop working
  - In networking as well, `redundancy` and `multi-pathing` are designed and configured to prevent the entire network from being paralyzed by a single device failure
- When a network is configured with a single switch and that **switch fails**, the **entire network fails**
  - To avoid this `SPoF`, the network is designed with **two or more switches**,
    - But designing with two or more switches can cause **packets to continuously transmit** through the network, potentially **paralyzing** it
      - This situation is called a `Network Loop`
  - A separate **mechanism** is needed to prevent `Loops`

<br>

<br>

## 1. What is a Network Loop?

- A `Loop` literally describes a situation where the **network connection shape** forms a **ring that comes back around**
  - When a loop situation occurs, the network becomes paralyzed and communication fails
- `Various Loop structures`
  1. **Redundant connections** between two devices
  2. Devices connected in a **single ring** formation
  3. Devices connected in an **overlapping ring** formation

<br>

### 1-1. Broadcast Storm

- When a terminal generates a **Broadcast** in a network connected with a loop structure, the switch **floods** the packet to all ports except the one it came in on
  - The **flooded** packet is also sent to **other switches**, and switches receiving this packet again **flood** it to all ports except the incoming port
    - In a `Loop` structure, **this packet continues to circulate**, which is called a `Broadcast Storm`
- The `Layer 3 header` has **TTL (Time to Live)** which gives packets a lifespan, but the `Layer 2 header` that **switches** examine has no **lifetime mechanism** like Layer 3's TTL, so when a loop occurs, packets don't die and keep surviving, potentially allowing a single packet to consume the entire network bandwidth
  - Such `broadcast storms` **consume the entire bandwidth** of the network, and with all terminals connected to the network using **system resources** to process broadcasts, communication between the switch and terminals becomes nearly impossible
- When a `Broadcast storm` occurs:
  1. **Terminal speeds slow down** on the network
     - CPU usage increases due to processing many Broadcasts
  2. **Network access speed slows down**
     - Nearly impossible to communicate
  3. All LEDs on switches installed on the network blink simultaneously at a fast speed
- Once a `Network Loop` is created, the network remains in a paralyzed-like state until the cable is removed

<br>

### 1-2. Switch MAC Learning Duplication Problem

- In a loop structure, not only `broadcast` but also `unicast` causes problems
  - The same packet circulates the loop and causes duplicate reception confusion on the destination side, and **intermediate switches** also experience `MAC Learning problems`
    - Switches **learn source MAC addresses**, but since the **directly delivered packet** and the **packet that went around through switches** arrive on different ports, the MAC address cannot be learned normally
    - Since the Switch MAC Address Table can only **learn one port** for **one MAC address**, when the **same MAC address is learned on multiple ports**, the MAC table is **repeatedly updated** and does not function normally
      - This phenomenon is called `MAC Address Flapping`
- To prevent `MAC Address Flapping`, depending on switch settings, warning messages are sent to administrators or automatic measures prevent learning from frequent flapping

<br>

- When a Loop occurs in the network, the above problems prevent normal network operation, so measures must be taken in advance to prevent loops
  - Even if just one of the ports in the loop configuration is **shutdown**, loops can be prevented
    - However, having designed the network with two or more switches to prevent `SPoF` and then manually finding and forcibly disabling loops is not desirable
      - First, finding loops through complex cable connections in the network is difficult
      - Even after finding and forcibly disabling a port, if a network failure occurs, the port must be manually re-enabled
    - Networks cannot adequately respond to failures with such active user intervention
      - For these reasons, `Spanning Tree Protocol` was developed to **automatically detect loops**, **block ports**, and when there is no alternate route due to failure, **reopen blocked ports** for the switch

<br><br>

## 2. What is STP?

- `STP (Spanning Tree Protocol)` is a mechanism that **detects loops** and appropriately **disables ports** to **prevent loops**
  - As the term suggests, the purpose of Spanning Tree Protocol is to **maintain a loop-free structure** like a well-branched tree **from root to branches**
- To prevent loops using STP, the **entire switch** connectivity must be known
  - To understand the overall switch connectivity, a method of **exchanging information between switches** is needed
    - For this, switches exchange information through a protocol called `BPDU (Bridge Protocol Data Unit)`, and using the collected information, the **entire network tree** is built to **identify loop sections**
      - `BPDU` contains unique values like the **switch's ID**, and as this information is **exchanged between switches**, **loop identification** becomes possible
      - The identified loop points are then **blocked from data traffic passage** to **prevent loops**

<br>

### 2-1. Switch Port States and Transition Process

- In switches where Spanning Tree Protocol is operating, to prevent loops:
  - When a new switch is connected to a switch port, **traffic is immediately blocked**
  - Then to verify whether **traffic should flow** on that port:
    - `BPDU` is waited for and learned,
    - The structure is analyzed,
    - Traffic is either allowed or the blocked state is maintained if it is a loop structure

<br>

#### Port Status from Blocked State to Traffic Flow

- `Blocking`
  - A state where packet data is blocked, waiting for **BPDU (Bridge Protocol Data Unit)** from the other party
  - If BPDU is not received from the other switch during the total 20-second **Max Age** period, or if a lower-priority BPDU is received, the port changes to **listening status**
  - The default BPDU exchange interval is **2 seconds**, waiting for 10 BPDUs
- `Listening`
  - A stage for **deciding** and **preparing** for the port to **transition to forwarding status**
    - From this state, it begins transmitting its own BPDU information to the other party
  - Waits for a total of **15 seconds**
- `Learning`
  - Having already **decided to forward on this port**, this is the stage of **learning MAC Addresses** so the switch can operate immediately when actual packet forwarding occurs
  - Waits for a total of **15 seconds**
- `Forwarding`
  - The stage of forwarding packets
    - Normal communication is possible at this stage!

<br>

### 2-2. STP Operation Method

- STP configures the topology **like a tree branching from root to branches** to eliminate loops
  - The **highest switch** in the network is elected as the root, and all BPDUs are exchanged through this switch, called the `Root Switch`
    - All switches initially recognize themselves as the root switch
      - Every 2 seconds, they advertise via BPDU that they are the root switch; when a new switch joins, the **bridge ID values** in the exchanged BPDUs are compared
      - The switch with the **lower Bridge ID value** is selected as the root switch, and the selected root switch sends BPDUs toward other switches

<br>

#### STP Operation to Prevent Loops

1. Select one `Root Switch`

   - One root switch is selected for the entire network
   - It sends `BPDU` declaring itself as the representative switch of the entire network to the adjacent switch

2. Select `Root Port` from non-Root switches

   - The port with the **shortest path** to the `Root Switch (Bridge)` is called the `Root Port`
   - The `Root Port` receives BPDUs sent from the `Root Bridge`

3. Select one `Designated Port` per **segment**

   - A **Designated Port** is selected for the connection between switches

   - In switch-to-switch connections:

     1. If one side is already selected as a root port, the opposite side is selected as the designated port, and both sides become **forwarding status**

     2. If neither side is a root port, one side becomes the **designated port** and the other becomes an **alternate port (Non-designated)** entering `blocking status`

   - The Designated Port is the **port through which BPDU is delivered**

<br>

#### STP Alternative - Port Fast

- When a new cable is connected to a port, instead of immediately transitioning to **forwarding status**, it assumes the other party could be a switch and **monitors** whether **BPDUs arrive**
  - However, this mechanism causes a **delay in terminal network connection time**, so if the connecting device is a regular PC or server rather than a switch, this mechanism should be removed or the transition to **forwarding status** should happen faster
    - In such cases, configuring the port as `Port Fast` allows using the port in **forwarding status immediately** without BPDU **waiting** and **learning** processes
    - If a switch connects to a `Port Fast` port, a loop can form, so separate technology like **BPDU Guard** that blocks the port as soon as BPDU arrives must be used together

<br>

<br>

### 2-3. Enhanced STP - RSTP, MST

- Spanning Tree Protocol considers the time for BPDU to be delivered to all switches in the same network to prevent loops
  - Therefore, it takes 30 ~ 50 seconds for a **blocking port** to transition to **forwarding status**
    - Since TCP-based applications, the most commonly used for communication, cannot wait 30 seconds when the network is disconnected, communication **may be interrupted** when a failure occurs in an STP-based network
    - Also, if a switch has **multiple VLANs**, **overhead occurs** from calculating STP for each VLAN
- Enhanced STP is used to solve these problems

<br>

#### 3-1. RSTP (Rapid Spanning Tree Protocol)

- Spanning Tree Protocol takes 30 ~ 50 seconds to **activate the backup path** when the **normal path** among redundant switch paths has a problem
  - `RSTP (Rapid Spanning Tree Protocol)` was developed to solve the problem of taking too long to activate backup paths
- `RSTP` has a switchover time of 2 ~ 3 seconds, allowing typical **TCP-based applications** to **maintain their sessions**
- The basic operation is the same as STP, but the BPDU message format is more diverse, allowing various status messages to be exchanged
  - STP has only two messages related to general topology changes (TCN: Topology Change Notification, TCA: Topology Change Acknowledgement BPDU)
  - RSTP uses **all 8 bits** to exchange various information with surrounding switches
- In traditional STP, when topology changed, terminal switches would send **change reports** up to the root bridge, and the root bridge would complete its recalculation and then send **updated topology information** down to terminal switches
  - Additionally, **reserve time** had to be considered for this information to **propagate to all switches** in the network, so it took **a long time to extend the information**
- In `RSTP`, the **switch where the topology change occurred** can **directly propagate** the topology change to the entire network
  - Instead of reporting to the root bridge and propagating, the terminal switch **directly notifies** other bridges of the topology change
- `RSTP` can **detect and recover from topology changes** faster than regular STP through diverse BPDU messages, alternate port concepts, and changes in topology change delivery methods!
  - In practice, `RSTP` can recover from failures in just 2 ~ 3 seconds, so even when failures occur, **application sessions are not interrupted**, helping operate the network more **stably**!

<br>

#### 3-2. MST (Multiple Spanning Tree)

- Regular Spanning Tree Protocol is called `CST (Common Spanning Tree)`
  - Regardless of the number of VLANs, **only one spanning tree operates**
    - In this case, even with many VLANs, only one spanning tree needs to operate, so **switch management overhead** is low
      - However, CST activates only one port and line in a loop-causing topology, so **resources cannot be efficiently utilized**
    - Also, each VLAN may have different optimal paths, but with only one usable port, communication may need to **take a longer detour**
- To solve CST's problems, `PVST (Per VLAN Spanning Tree)` was developed
  - Different spanning tree processes operate per VLAN, enabling separate paths and trees per VLAN
    - This enabled **designing optimal paths** and **designating separate block ports per VLAN** to configure **network load sharing**
      - However, the spanning tree protocol itself **puts significant burden on switches (exchanging every 2 seconds)**, and PVST requires **maintaining separate spanning trees for every VLAN**, adding even more burden

- To complement the disadvantages of CST and PVST, `MST (Multiple Spanning Tree)` was developed
  - `MST`'s basic idea is to **group multiple VLANs together** and have **separate spanning trees operate** per group
    - In this case, far fewer spanning tree processes run than PVST, and PVST's advantage of **load sharing** can also be used
- Generally, the number of `MST` **spanning tree processes** is defined based on the number and purpose of **alternate paths**
  - MST introduces a **region concept**, allowing **multiple VLANs to be bundled into a single region**
    - region 1 == spanning tree 1
    - ex)
      - If there are VLANs 11~50 and 101~150,
        - Bundle 11~50 into one region
        - Bundle 101~150 into one region, then 100 VLANs can be managed with two spanning trees

<br>

<br>

#### Why Switches Have IP Addresses and Switch Architecture

- Switches are broadly divided into a management `Control Plane` and a `Data Plane` for packet forwarding
  - **STP** and switch remote management services like telnet, SSH, and web are performed in the `Control Plane`
- Switches are Layer 2 devices that can only **understand MAC addresses**
  - IP is not needed for switch operation, but switches operating in networks of a certain scale or larger are mostly assigned IP addresses for **management purposes**
