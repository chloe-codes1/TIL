# Layers of OSI Model

> 영어로 된 부분은 처음에 공부한 내용 & 한글로 된 부분은 책보며 다시 공부한 내용
>
> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

### Before getting started

- 과거에는 통신용 규약이 표준화되지 않아서 호환되지 않는 system이나 application이 많았고 통신이 불가능 했음
  - 이것을 하나의 **규약**으로 **통합** 하려는 노력이 현재의 `OSI 7 Layers` 로 남아있다!
- `OSI 7 Layers`가 network 동작을 나누어 이해하고 개발하는데 도움이 되므로 main network reference model로 활용되고 있지만, 
  - 현재 대부분의 protocol은 **TCP/IP protocol stack** 기반으로 되어 있다 

<br>

<br>

## What is OSI 7 Layers?

<br>

### OSI 7 Layers

- OSI (= Open Systems Interconnection) is a **7 layer** architecture with each layer having specific functionality to perform.
- All these 7 layers work *collaboratively* to **transmit the data** from one person to another across the globe.

![OSI 7 Layers](../images/The_7_Layers_of_OSI.png)

<br>

OSI 7 Layers는 계층의 **역할**과 **목표**에 따라 두 가지 계층으로 나눌 수 있다.

#### 1~4 계층

- `Lower Layer`
- `Data Flow Layer`
  - data를 상대방에게 잘 **전달**하는 역할을 갖고 있다

#### 5~7 계층

- `Upper Layer`
- `Application Layer`
  - data를 **만드는** 역할을 하는 부분이다

<br>

- **application 개발자**
  - data flow layer를 고려하지 않고 data를 **표현**하는 데 초점을 맞춘다
  - `Top-down` 형식으로 network를 바라본다
- **network engineer**
  - application layer는 application 개발자들이 고려해야 할 영역이므로 network engineer는 이 부분에 대해 일반적으로 심각하게 고민하지 않는다
  - `Bottom-up` 형식으로 network를 바라본다



<br>

<br>

## Details

<br>

### 1. Physical Layer (Layer 1) 

- The lowest layer of the OSI reference model is the physical layer. 
- It is responsible for the actual physical connection between the devices. 
- The physical layer contains information in the form of **bits.** 
  - It is responsible for transmitting individual bits from one node to the next. 
  - When receiving data, this layer will get the signal received and convert it into 0s and 1s and send them to the Data Link layer, which will put the frame back together.

![img](https://media.geeksforgeeks.org/wp-content/uploads/computer-network-osi-model-layers-bits.png)

- **물리적 연결**과 관련된 정보를 정의
- 주로 **전기 신호** 를 **전달**하는데 초점이 맞추어져 있음
  - 들어온 전기 신호를 **그대로 잘 전달**하는 것이 목적이므로 전기 신호가 `1계층 장비` 에 들어오면 이 전기 신호를 **재생성**하여 내보낸다
- 1계층 장비는 **주소의 개념이 없다**!
  - 신호가 들어온 port를 제외하고 **모든 port**에 **같은 전기 신호**를 전송한다
    - 즉, 출발지와 목적지를 구분 할 수 없다

<br>



### 2. Data Link Layer (DLL) (Layer 2) 

- The data link layer is responsible for the node to node delivery of the message. 
- The main function of this layer is to make sure data transfer is error-free from one node to another, over the physical layer. 
- When a `packet` arrives in a network, it is the responsibility of DLL to transmit it to the Host using its `MAC address`.
- Data Link Layer is divided into two sub layers :
  1. `Logical Link Control (LLC)`
  2. `Media Access Control (MAC)`

- The packet received from Network layer is further divided into frames depending on the frame size of `NIC(Network Interface Card)`. 
- DLL encapsulates Sender and Receiver’s MAC address in the header.
- The Receiver’s MAC address is obtained by placing an `ARP(Address Resolution Protocol)` request onto the wire asking *“Who has that IP address?”* and the destination host will reply with its MAC address.
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/computer-network-osi-model-layers-framing.png" alt="img" style="zoom:110%; " />

- 전기 신호를 모아 우리가 알아볼 수 있는 data 형태로 처리한다
- 1계층과는 다르게 전기 신호를 정확히 **전달**하기 보다는 `주소 정보`를 **정의**하고 `정확한 주소`로 **통신**하는데 초점이 맞추어져 있다
- `출발지` 와 `도착지` 주소를 확인하고 내게 보낸 것이 맞는지 or 내가 처리해야 하는지에 대해 **검사**한 후에 **data 처리**를 수행한다

- 2계층에서는 `주소 체계` 가 생기면서 여러 통신이 한꺼번에 이루어지는 것을 **구분**하기 위한 기능이 주로 정의된다
- `전기 신호`를 모아 data 형태로 처리하므로 data에 대한 **error**를 **탐지**하거나 **고치는** 역할을 수행할 수 있다
  - Ethernet 기반 network의 2계층에서는 error를 탐지하는 역할만 수행한다
- 주소 체계가 생긴다는 것은 한 명과 통신하는 것이 아니라 동시에 **여러 명**과 **통신**할 수 있다는 것이므로 무작정 data를 던지는 것이 아니라 **받는 사람이 현재 data를 받을 수 있는지 확인** 하는 작업부터 해야 한다
  - 이 역할을  `Flow Control` 이라고 부른다
    - **Flow Control**
      1. 서버에서 스위치로 data 전송
      2. 스위치 혼잡 상황 발생. 스위치는 서버로 Pause frame 전송
      3. 서버는 Pause frame 수신 수 대기
- 2계층의 network 구성 요소는 `Network Interface Card`와 `Switch`이다
- 2계층의 가장 중요한 특징은 **MAC 주소**라는 주소 체계가 있다는 것이다
  - 2계층에서 동작하는 `Network Interface Card`와 `Switch` 모두 **MAC 주소**를 이해할 수 있고, `Switch`는 MAC 주소를 보고 통신해야 할 port를 지정해 내보내는 능력이 있다
    - **Network Interface Card 동작 방식**
      1. 전기 신호를 data 형태로 만든다
      2. 목적지 MAC 주소와 출발지 MAC 주소를 확인한다
      3. Network Interface Card의 MAC 주소를 확인한다
      4. 목적지 MAC 주소와 Network Interface Card가 갖고 있는 MAC 주소가 **맞으면** data를 **처리**하고, **다르면** data를 **폐기**한다  
    - **Switch 동작 방식**
      - Swtich는 단말이 어떤 MAC 주소인지, 연결된 port는 어느 것인지 **주소 습득 (Address learning)** 과정에서 알 수 있다
        - 이 data를 기반으로 단말들이 통신할 때 port를 적절히 **filtering** 하고, 정확한 port로 **forwarding** 해준다
      - Switch의 적절한 filtering과 forwarding 기능으로 통신이 필요한 port만 사용하고, network 전체에 불필요한 처리가 감소하면서
        - Ethernet network 효율성이 크게 향상되었고,
        - Ethernet 기반 network가 급증하는 계기가 되었다!

 <br>

### 3. Network Layer (Layer 3) 

- Network layer works for the transmission of data from one host to the other located in different networks. 
- It also takes care of `packet routing` i.e. selection of the shortest path to transmit the packet, from the number of routes available. 
- The sender & receiver’s IP address are placed in the header by the network layer.
- The functions of the Network layer are :
  1. **Routing** 
     - The network layer protocols determine which route is suitable from source to destination. 
     - This function of network layer is known as routing.
  2. **Logical Addressing** 
     - In order to identify each device on internetwork uniquely, network layer defines an addressing scheme. 
     - The sender & receiver’s IP address are placed in the header by network layer. 
     - Such an address distinguishes each device uniquely and universally.

- Segment in Network layer is referred as **Packet**.
  ![img](https://media.geeksforgeeks.org/wp-content/uploads/computer-network-osi-model-layers-packet.png)
- Network layer is implemented by networking devices such as routers

<br>

### 4. Transport Layer (Layer 4) 

- Transport layer provides services to application layer and takes services from network layer.
- The data in the transport layer is referred to as *`Segments`*. 
- It is responsible for the End to End Delivery of the complete message. 
- The transport layer also provides the acknowledgement of the successful data transmission and re-transmits the data if an error is found.
- Data in the Transport Layer is called as  `Segment`.
- Transport layer is operated by the `Operating System`. 
- It is a part of the OS and communicates with the Application Layer by making system calls.
- Transport Layer is called as **Heart of OSI** model.
  

<br>

### 5. Session Layer (Layer 5)

- The Session layer is responsible for establishment of connection, maintenance of sessions, authentication and also ensures security.
- The functions of the session layer are :
  1. **Session establishment, maintenance and termination** 
     -  The layer allows the two processes to establish, use and terminate a connection.
  2. **Synchronization ** 
     -  This layer allows a process to add checkpoints which are considered as `synchronization points` into the data. 
     - These synchronization point help to identify the error so that the data is re-synchronized properly, and ends of the messages are not cut prematurely and data loss is avoided.
  3. **Dialog Controller ** 
     - The session layer allows two systems to start communication with each other in half-duplex or full-duplex.

<br>

### 6. Presentation Layer (Layer 6) 

- Presentation layer is also called the **Translation layer**.
- The data from the application layer is extracted here and manipulated as per the required format to transmit over the network.
- The functions of the presentation layer are :
  1. **Translation**
     - For example, ASCII to EBCDIC.
  2. **Encryption/ Decryption** 
     - Data encryption translates the data into another form or code. 
  3. **Compression** 
     - Reduces the number of bits that need to be transmitted on the network.

<br>

### 7. Application Layer (Layer 7) 

- At the very top of the OSI Reference Model stack of layers, we find Application layer which is implemented by the network applications. 
- These applications produce the data, which has to be transferred over the network. 
- This layer also serves as a window for the application services to access the network and for displaying the received information to the user.
  - Ex: Application – Browsers, Skype Messenger etc.

- Application Layer is also called as Desktop Layer.

<br>

<br>

## Summary

<br>

![undefined](https://www.cloudflare.com/img/learning/ddos/what-is-a-ddos-attack/osi-model-7-layers.svg)