# Encapsulation and Decapsulation

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

- `상위 계층`에서 `하위 계층`으로 data를 보내면 Physical Layer에서 **전기 신호** 형태로 network를 통해 신호를 보낸다
- 받는 쪽에서는 다시 `하위 계층`에서 `상위 계층`으로 data를 보낸다
  - 이렇게 data를 보내는 과정을 **Encapsulation**, 받는 과정을 **Decapsulation**이라고 부른다

![encapsulation and de-encapsulation in tcp/ip model](https://www.computernetworkingnotes.org/images/cisco/ccna-study-guide/csg25-03-tcp-ip-encapsulation.png)

<br>

- 현대 network는 대부분 `packet`기반 network이다
  - `packet network`는 data를 packet이라는 작은 단위로 쪼개 보내는데,
    - 이런 기법으로 하나의 통신이 **회선 전체를 점유**하지 않고 동시에 **여러 단말이 통신**하도록 해준다
  - data를 packet으로 **쪼개고** network를 이용해 목적지로 보내고, 받는 쪽에서는 다시 큰 data 형태로 **결합**해 사용한다

<br>

<br>

### Encapsulation

- application에서 data를 **Data Flow Layer (1~4층)**로 내려보내면서 packet에 data를 넣을 수 있도록 분할하는데, 이 과정을 **Encapsulation**이라고 한다
- network 상황을 고려해 적절한 크기로 data를 쪼개고, 위의 그림처럼 4계층 (Transport Layer)부터 **네트워크 전송을 위한 정보**를 `header`에 붙여 넣는다
  - **header 정보**는 `4계층`, `3계층`, `2계층`에서 각각 자신이 필요한 정보를 추가하는데 이 정보는 미리 정의된 **bit 단위** (0또는 1)로 쓴다
    - 4계층에서 header를 추가하고 `3계층`으로 내려보내면 `3계층`에서 필요한 header를 추가하고 `2계층`으로 내려보낸다
    - `2계층`에서도 필요한 정보를 header에 추가한 후 **전기 신호**로 변환해 수신자에게 전송한다
- data를 전송하는 작업은 생각보다 복잡해서 data flow layer (1~4계층) 에서만 **3개의 header 정보**가 추가된다

<br><br>

### Decapsulation

- data를 받는 쪽에서는 **Decapsulation** 과정을 수행한다
- 받은 **전기 신호**를 **data 형태**로 만들어 `2계층`으로 올려보낸다
- `2계층`에서는 송신자가 작성한 2계층 header에 포함된 정보를 확인한다
  - 만약 `2계층`에 적힌 정보 중 **목적지**가 자신이 아니라면 자신에게 온 **packet**이 아니므로 버린다
    - 이 역할은 **LAN Card**가 담당한다
  - `2계층`에 적힌 정보의 목적지가 자신이 맞다면, `3계층`으로 정보를 보내준다
    - data를 상위 계층으로 올려보낼 때 **2계층의 header 정보**는 더 이상 필요없으므로 **벗겨내고 올려보낸다**
    - `3계층`과 `4계층`에서도 똑같이 각 계층의 정보를 확인하고, 자신에게 온 것이 맞는지 확인 후 맞으면 상위 계층으로 올려보낸다

<br>

<br>

이러한 작업은 아래의 2가지 정보 흐름으로 설명할 수 있다

1. `Encapsulation`, `Decapsulation` 과정을 통해 **data가 전송되는 과정**
2. 각 계층 `header`를 이용해 송신자 계층과 수신자 계층 간의 **논리적 통신 과정**

<br>

- 실제로  data는 상위 계층(Upper Layer)에서 하위 계층(Lower Layer)로 상위 계층에서 **packet** 형태로 하나씩 **encapsulation**되면서 내려오고, 2계층의 **LAN card**에서 **전기 형태**로 변환되어 목적지로 전달된다
- 해당 전기 신호를 받은 목적지에서는 **data 형태**로 변환해 상위 계층으로 올려주고, **packet**들을 조합해 **data 형태**로 만들게 된다
- 즉, 실제 data는 `상위 계층`에서 `하위 계층`, `하위 계층`에서 `상위 계층`으로 전달되고 **header 정보**는 각 계층끼리 전달된다

<br>

<br>

### Header 정보

Data를 **encapsulation**하는 과정에서 **header**에 넣는 정보는 다양한데, 이런 복잡한 정보들에서도 규칙이 있으며 아래의 두 가지 정보는 반드시 포함되어야 한다

1. 현재 계층에서 정의하는 정보
2. 상위 protocol 지시자

<br>

#### 1. 현재 계층에서 정의하는 정보

- OSI 7계층의 각 계층에서의 목적에 맞는 정보들이 포함된다
- `4계층`의 목적은 큰 data를 잘 **분할**하고 받는 쪽에서는 잘 **조립**하는 것이기 때문에 data에 **순서**를 정하고 받은 `packet`의 순서가 맞는지 **점검**하는 역할이 중요하며 이 정보를 `header`에 적어 넣게 된다
  - `TCP/IP`의 4계층 protocol인 **TCP**에서는 **Sequence number**, **ACK number** field로 이 data를 표현한다
- `3계층 hearder`에는 3계층에서 정의하는 **논리적 주소**인 **출발지, 도착지 IP 주소**를 header에 적어넣는다
- 2계층은 **MAC 주소**를 정의하는데, 3계층처럼 2계층도 **출발지, 도착지 MAC 주소**를 header에 넣는다

<br>

#### 2. 상위 protocol 지시자

- **protocol stack**은 상위 계층으로 올라갈수록 종류가 많아진다
  - 3게층 protocol인 `IP`는 4계층에서는 `TCP`와 `UDP`로 나뉘고, 그보다 더 상위 계층에서는 `FTP`, `HTTP`, `SMTP`, `POP3`등 더 다양한 prtocol로 다시 나뉜다
- **Encapsulation** 과정에서는 상위 Protocol이 많아도 문제가 없지만, **decapsulation** 하는 목적지 쪽에서는 header에 아무 정보가 없으면 **어떤 상위 protocol**로 올려보내 주어야 할지 결정할 수 없다
  - ex) 3계층에서 목적지 `IP주소`를 확인하고 4계층으로 data를 올려보낼 때 header에 상위 protocol 정보가 없다면 `TCP`로 보내야 할지 `UDP`로 보내야 할지 구분할 수 없다
- 이러한 문제가 발생하지 않도록 **Encapsulation**하는 쪽에서는 `header`에 **상위 protocol 지시자 정보**를 포함해야 한다

<br>

<br>

### 상위 프로토콜 지시자

- 각 계층마다 상위 protocol 지시자를 가지고 있지만 계층마다 이름이 다르다
  - 4계층은 port 번호
  - 3계층은 protocol 번호
  - 2계층은 Either type이라고 부른다
- 여기서 주의해야 할 점은 port 번호는 4계층 header에 적힌 정보이지만 application layer에서 protocol 종류라는 것이다
  - 즉, **decapsulation** 할 때 상위 protocol 정보를 이용해 어느 상위 protocol로 보내야 할지 구분해야 하므로 동작하는 계층보다 한 계층 위의 정보가 적혀있게 된다

<br>

#### port 번호 - 4계층

| Port 번호         | Service                                   |
| ----------------- | ----------------------------------------- |
| TCP 20, 21        | FTP (File Transfer Protocol)              |
| TCP 22            | SSH (Secure Shell)                        |
| TCP 23            | TELNET (Telnet Terminal)                  |
| TCP 25            | SMTP (Simple Mail Transport Protocol)     |
| UDP 49            | TACACS                                    |
| TCP 53 / UDP 53   | DNS (Domain Name Service)                 |
| UDP 67, 68        | BOOTP (Bootstrap Protocol)                |
| TCP 80 / UDP 80   | HTTP (HyperText Transfer Protocol)        |
| UDP 123           | NTP (Network Time Protocol)               |
| UDP 161, 162      | SNMP (Simple Network Management Protocol) |
| TCP 443           | HTTPS                                     |
| TCP 445 / UDP 445 | Microsoft-DS                              |

<br>

#### protocol 번호 - 3계층

| Protocol 번호 | Protocol                         |
| ------------- | -------------------------------- |
| 1             | ICMP (Internet Control Message)  |
| 2             | IGMP (Internet Group Management) |
| 6             | TCP (Transmission Control)       |
| 17            | UDP (User Datagram)              |
| 50            | ESP (Encap Security Payload)     |
| 51            | AH (Authentication Header)       |
| 58            | IPv6용 ICMP                      |
| 133           | FC (Fibre Channel)               |

<br>

#### Ether Type

| Ether Type                       | Protocol                             |
| -------------------------------- | ------------------------------------ |
| 0x0800                           | IPv4 (Internet Protocol version 4)   |
| 0x0806                           | ARP (Address Resolution Protocol)    |
| 0x22F3                           | IETF TRILL Protocol                  |
| 0x8035                           | RARP (Reserve ARP)                   |
| 0x8100                           | VLAN-tagged frame (802.1Q)           |
| Shortest Path Bridging (802.1aq) | AH (Authentication Header)           |
| 0x86DD                           | IPv6 (Internet Protocol version 6)   |
| 0x88CC                           | LLDP (Link Layer Discovery Protocol) |
| 0x8906                           | FCoE (Fibre Channel over Ethernet)   |
| 0x8915                           | RoCE (RDMA over Coverged Ethernet)   |
