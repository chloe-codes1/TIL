# Network Lines

> Let's learn about network lines
>
> Reference: [Book] Network Introduction for IT Engineers

<br>

<br>

- To connect to a remote network, you need to use a **WAN**
  - Various types of network lines and technologies have been used in WAN to connect **telecommunications carriers** and **users**, but currently **LAN**-identical `Ethernet` is primarily used
- In addition to regular `Ethernet`, different technologies are used for special purposes such as **low-speed line technologies** based on **voice circuits** and **high-speed communication** between telecommunications carriers, or for subscriber identification/distinction

<br>

<br>

### 1. Internet Lines

- The lines connecting to `telecommunications carriers` for **Internet access** are called internet lines
- Simply connecting a cable to a telecommunications carrier does not enable connectivity; you must use a **line connected to the Internet sold by the telecommunications carrier** to access the Internet
- The technology used to connect homes to the Internet is slightly different from the `leased line` technology described later
  - The structure is not a direct connection between **subscriber** and **telecommunications carrier**, but uses **shared transmission line technology**
    - ex)
      - Although apartment optical LAN appears to be like a dedicated Internet line with direct internal wiring,
        - The line connecting from the apartment to the telecommunications carrier is **shared** among apartment subscribers
  - Since **transmission lines are shared**, the speed of general Internet lines is the maximum possible speed and is not guaranteed
    - In other words, speeds may slow down depending on surrounding usage

<br>

#### Types of General Internet Lines

- Optical LAN (Ethernet)
  - Giga ~ 100Mbps
- FTTH
  - Giga ~ 100Mbps
- Coaxial Cable Internet
  - Hundreds ~ Tens of Mbps
- xDSL (ADSL, VDSL, etc.)
  - Tens ~ Single Mbps

<br>

- The above Internet access technologies use existing telephone lines or are **shared** from a certain point onward
- Since not everyone is always using the Internet at maximum capacity, it is common to build **shared sections** in a way that **does not guarantee maximum speed for each user**

<br>

<br>

### 2. Leased Line

- Services that **guarantee bandwidth** between the `subscriber` and `telecommunications carrier` are generally called **leased lines**
- The `subscriber` and `telecommunications carrier` are connected by a **dedicated cable**, and inside the carrier, technology like **TDM (Time Division Multiplexing)** is used to guarantee communication quality **as if directly connected**
- Non-Internet `dedicated leased lines` are primarily used for **headquarters-branch connections**

<br>

Leased lines can be classified into **low-speed lines** based on **voice transmission** and **high-speed lines** called **Metro Ethernet** based on the `transmission technology` connecting with the `subscriber`

<br>

#### 2-1. Low-speed Lines Based on Voice Transmission Technology

- Low-speed voice transmission technology is divided and used in **64kbps** units
- It is a technology that has been used for a long time, developed by **bundling** **small basic units** to **increase line access speed**
- It was typically used when **high speeds were not needed** or when **high reliability was required**, but
  - Currently, Ethernet-based optical transmission technology has developed to a reliable level, so usage frequency is declining
    - However, low-speed lines are still often used for **VAN (Value Added Network)** for transmitting payment approvals such as `Clear Text transmission` and **external connections**
- To use low-speed voice transmission technology, a `Router` capable of **converting to remote transmission technology** is needed

<br>

#### 2-2. Metro Ethernet High-speed Lines

- High-speed connections mostly use **optical cable-based** `Ethernet`
- The technology between subscriber and carrier is `Ethernet`, and **inside the carrier**, other high-speed communication technologies are used to bundle individual subscribers for communication
  - The reason communication techniques differ between subscriber and carrier internally is that carriers need to **distinguish multiple subscribers** and **transmit** subscriber **traffic** at **high speed**
  - Additionally, technology is used to **unify** various subscriber access technologies into a single technology
    - Why?
      - To carry low-speed communication lines, Ethernet, and voice on a single line!

<br>

`+`

#### LLCF (Link Loss Carry Forward)

- LLCF is a feature that **detects** when one side's link goes down and **brings down** the opposite side's link as well
- When configuring a leased line with `Ethernet`, if the carrier does not configure `LLCF`, even if the leased line goes down at one site, the other site will appear to still have the line alive
  - After line provisioning, you should verify whether `LLCF` is configured!
- However, low-speed lines have a function to check **Layer 2 protocol** communication status, so `Routers` can detect when the other party's link is disconnected, making `LLCF` configuration unnecessary!

<br>

<br>

### 3. Internet Leased Line

- A product that **guarantees** communication **bandwidth** for Internet connection lines is called an `Internet leased line`
  - The `subscriber` connects to the `telecommunications carrier`, which then connects to the Internet
- Unlike the access technology used by subscribers in regular homes, Internet leased lines do not **compete with other subscribers** and **guarantee connection quality** between the `telecommunications carrier` and `subscriber`
- The most common recent Internet leased line technology is `Ethernet`
  - This technology called `Metro Ethernet` is based on recent Ethernet technology that can transmit several to tens of kilometers

<br>

<br>

### 4. VPN (Virtual Private Network)

- VPN is a network technology that **creates the effect of a virtual connection** even though it is not physically dedicated
- There are various VPN technologies, and technologies from the `subscriber perspective` and `carrier perspective` have developed separately

<br>

#### 4-1. Carrier VPN

- `Leased lines` **increase in cost as the connection distance grows**
  - In-city leased line connections are not expensive, but cross-city or international leased lines are very expensive
  - Although available bandwidth is guaranteed, since subscribers do not always use 100% of the contracted bandwidth, **wasted** costs can be significant
- To reduce this cost waste, **carriers directly distinguish subscribers** using VPN technology to lower costs
  - The most representative VPN technology is **MPLS VPN**
    - **MPLS VPN**
      - Although multiple subscribers connect to a single MPLS network, technology to **distinguish subscribers** is applied so it can be used **like a leased line**
      - Using this technology, **multiple subscribers** access and communicate over **a single network**, sharing public lines and **lowering costs**
      - Leased line costs are affected by `distance` and `speed`, but MPLS VPN lines are primarily affected by `speed`,
        - So **as distance increases**, using **public network technology** like MPLS helps lower costs
      - Connections between `headquarters-branches` or `branch-branch` are mostly connected using MPLS VPN technology
        - From the user's perspective, there is nothing technically special to consider, so the same access technology as **regular leased lines** is used

<br>

#### 4-2. Subscriber VPN

- If a general user uses VPN, it is mostly subscriber VPN technology
- Users can build their own **virtual private network** using regular Internet connections
- Connecting remote areas or overseas via leased lines is very expensive, and MPLS VPN lines are also more expensive than regular Internet connections
  - So **VPN over regular Internet connections** is used to lower costs

<br>

<br>

### 5. DWDM (Dense Wavelength Division Multiplex)

- `Wavelength division multiplexing` technology was developed to overcome the problem of **high cable installation costs** and **difficulty in management** when communicating over **long distances**

- Before **WDM** technology, only **one communication per optical cable** was possible

  - `WDM`
    - A device that divides the wavelength of the signal (light) used

- Telecommunications carriers needed to **distinguish** many subscribers and provide **high bandwidth** communication, so **multiple cables** had to be installed, and there were difficulties in installing such physical cables

  - With `WDM` and `DWDM` technology, **different wavelengths of light** on a **single optical cable** create **multiple channels** while simultaneously transmitting **large amounts of data**

- `DWDM` transmission technology uses more channels than conventional `WDM`

  - This technology is primarily used **within telecommunications carriers** for **long-distance communication**, but recently it is also being used for **gigabit Internet** in regular households
