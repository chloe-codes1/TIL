# TCP / UDP

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

- 2계층과 3계층은 목적지를 정확히 찾아가기 위한 **주소 제공**이 목적이었지만, 4계층에서 동작하는 protocol은 만들어진 목적이 2, 3 계층과 조금 다르다
  - 목적지 단말 안에서 동작하는 여러 application process 중 **통신해야 할 목적지 process**를 정확히 찾아가고,
  - packet 순서가 바뀌지 않도록 잘 **조합**해
  - **원래 data**를 잘 만들어내기 위한 역할을 한다

<br>

## 1. Layer 4 Protocol (TCP, UDP) and Service Port

- Data를 보내고 받는 Encapsulation, Decapsulation 과정에 각 계층에서 정의하는 header가 추가되고, 여러가지 정보가 들어간다
  - 다양한 정보 중 가장 중요한 두 가지 정보는 아래와 같다
    1. 각 계층에서 정의하는 정보
       - 수신 측의 동일 계층에서 사용하기 위한 정보
    2. 상위 protocol 지시자 정보
       - Decapsulation 과정에서 상위 계층의 protocol이나 process를 정확히 찾아가기 위한 목적으로 사용
- `TCP/IP Protocol Stack`에서 4계층은 TCP와 UDP가 담당한다
  - 4계층의 목적은 application에서 사용하는 process를 정확히 찾아가고, data를 분할한 `packet`을 잘 쪼개 보내고 잘 조립하는 것이다
  - packet을 분할하고 조립하기 위해 **Sequence Number**와 **ACK Number**를 사용한다

- `TCP/IP Protocol Stack`에서 상위 protocol 지시자는 **port**번호이다
  - 4계층 protocol 지시자인 port 번호는 **출발지와 목적지를 구분해 처리**해야 한다

<br>

#### Well Known Port

- HTTP TCP 80, HTTPS TCP 443, SMTP TCP 25와 같이 잘 알려진 Port를  **Well known** port 라고 한다
- 이 port들은 이미 인터넷 주소 할당 기구인 **IANA (Internet Assgined Numbers Authority)**에 등록되고 **1023**번 이하의 port 번호를 사용한다
- 다양한 application에 port 번호를 할당하기 위해 **Registered Port** 범위를 사용한다
  - `1024 ~ 49151` 의 범위이며,port 번호를 할당받기 위해 신청하면 **IANA**에 등록되어 관리된다
    - but, 공식 번호와 비공식 번호가 혼재되어 있고, 사설 port 번호로 사용되기도 한다
- **동적**, **사설**, **임시** port 의 범위는 `49152 ~ 65535` 이다
  - 이 범위의 port 번호는 IANA에 등록되어 사용되지 않는다
  - 이 port 번호는 자동으로 할당되거나, 사설 용도로 할당되고, client의 임시 port 번호로 사용된다!
- [IANA가 관리하는 Port 확인하기](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)

<br>

<br>

## 2. TCP

- TCP는 Layer 4의 특징을 대부분 포함하고 있다
- TCP protocol은 신뢰할 수 없는 공용망에서도 **정보유실** 없는 통신을 보장하기 위해
  - session을 안전하게 연결하고
  - data를 분할하고
  - 분할된 packet이 잘 전송되었는지 확인하는 기능이 있다
- Packet 에 번호(`Sequence Number`)를 부여하고 잘 전송되었는지에 대해 응답(`Acknowledge Number`) 한다
  - 또한, **한꺼번에 얼마나 보내야** 수신자가 잘 받아 처리할 수 있는지 전송크기 (`Window Size`)까지 고려해 통신한다
    - 이러한 TCP의 역할 덕분에 network 상태를 심각하게 고려하지 않고 쉽고 안전하게 network를 사용할 수 있다

<br>

### 2-1. Packet 순서와 응답 번호 (ACK Number)

- TCP에서는 분할된 packet을 잘 분할하고 수신측이 잘 조합하도록 **packet에 순서**를 주고 **응답 번호**를 부여한다
- Packet에 **순서**를 부여하는 것을 `Sequence Number`, **응답 번호**를 부여하는 것을 `ACK Number` 라고 부른다
  - 두 번호가 상호작용해 **순서가 뒤바뀌거나** 중간에 packet이 **손실**된 것을 파악할 수 있다

<br>

#### `Sequence Number` 와 `ACK Number`의 기본 동작 방식

- 보내는 쪽에서 packet에 **번호를 부여**하고 받는 쪽은 이 번호의 **순서가 맞는지 확인**한다

- 받은 packet 번호가 맞으면 응답을 주는데, 이때 다음 번호의 packet을 요청한다
  - 이 숫자를 `ACK Number`라고 한다

- 송신 측이 1번 packet을 보냈는데 수신 측이 이 packet을 잘 받는다면 1번을 잘 받았으니 다음에는 2번을 달라는 표시로 `ACK Number` 2를 준다

ex)

1. 출발지에서 `Sequence Number` 를 0으로 보낸다 (SEQ = 0)

2. 수신 측에서는 0번 packet을 잘 받았다는 표시로 응답 번호 (`ACK Number` 에 1을 적어 응답한다

   이때 수신 측에서는 자신이 처음 보내는 packet이므로 자신의 packet에 `Sequence Number` 0을 부여한다

3. 이 packet을 받은 송신 측은 `Sequence Number`를1로,  (수신 측이 `ACK Number`로 1번 packet을 달라고 요청했으니까!!)

   `ACK Number`는 상대방의 0번 Sequence를 잘 받았따는 의미로 Sequence Number를 1로 부여해 다시 송신한다!

<br>

### 2-2. Window Size & Sliding Window

- TCP는 일방적으로 packet을 보내는 것이 아니라 상대방이 얼마나 **잘 받았는지 확인**하기 위해 **ACK 번호를 확인**하고 **다음 packet을 전송**한다
  - Packet이 잘 전송되었는지 확인하기 위해 별도 packet을 받는 것 자체가 **통신 시간**을 늘리지만, 송신자와 수신자가 먼 거리에 떨어져 있으면 **왕복 지연시간 (Round Trip Time, RTT)**이 늘어나므로 **응답을 기다리는 시간이 더 길어**진다
    - 만약 작은 packet을 하나 보내고 응답을 받아야만 하나를 더 보낼 수 있다면 모든 data를 전송하는 데 긴 시간이 걸릴 것이다
    - 그래서 data를 보낼 때 packet을 하나만 보내는 것이 아니라 **많은 packet을 한꺼번에** 보내고 **응답을 하나만** 받는다
- 가능하면 최대한 많은 packet을 한꺼번에 보내는 것이 효율적이지만, Network 상태가 안 좋으면 **packet 유실** 가능성이 커지므로 **적절한 송신량**을 결정해야 하는데,
  - 한 번에 data를 받을 수 있는 data의 크기를 `Window Size`라고 하고,
  - Network 상황에 따라 이 window size를 조절하는 것을 `Sliding Window`라고 한다
- TCP Header에서 window size로 표현할 수 있는 최대 크기는 **2^16** 이다
  - 실제로 64K만큼 window size를 가질 수 있지만 이 size는 **회선의 안정성**이 높아지고 **고속화**되는 현대 network에서는 너무 작은 숫자이다
    - 그래서 window size를 64K보다 **대폭 늘려 통신**하는데 **TCP header는 변경이 불가능**하므로 header size를 늘리지 않고 **뒤의 숫자를 무시**하는 방법으로 window size를 증가시켜 통신한다
      - 이 방법을 사용하면 기존 숫자의 10배, 100배로 window가 커진다!
- TCP는 **data 유실**이 발생하면 window size를 **절반**으로 떨어뜨리고 정상적인 통신이 되는 경우 서서히 하나씩 늘린다
  - 만약 **Network 경합**이 발생해 `packet drop`이 생기면 작아진 window size로 인해 data 통신 속도가 느려져 회선을 제대로 사용하지 못하는 상황이 발생할 수 있다
    - 이 경우 경합을 피하기 위해
      1. 회선 속도를 증가시키거나
      2. 경합을 임시로 피하게 할 수 있는 **buffer가 큰 network 장비**르ㄹ 사용하거나
      3. **TCP 최적화 solution**을 사용해 이런 문제들을 해결할 수 있다

<br>

### 2-3. 3-Way Handshake

- TCP에서는 **유실없는 안전한 통신**을 위해 통신 시작 전 **사전 연결작업**을 진행한다

  - 만약 목적지가 data를 받을 준비가 안 된 상황에서 data를 일방적으로 전송하면 목적지에서는 data를 정상적으로 처리할 수 없어 **data가 버려진다**
  - 이런 상황을 방지하기 위해 TCP protocol은 data를 안전하게 보내고 받을 수 있는지 미리 확인하는 작업을 거치는 것이다!

- `Packet Network`에서는 **동시에 많은 상대방과 통신**하므로 정확한 통신을 위해 통신 전 통신에 필요한 **resource를 미리 확보**하는 작업이 중요하다

  - TCP에서는 **3번의 packet**을 주고받으면서 **통신을 서로 준비**하므로 `3-Way Handshake`라고 부른다

- TCP에서는 이런 `3-Way Handshake` 진행 상황에 따라 **state** 정보를 부르는 이름이 다르다

  - Server에서는 service를 제공하기 위해 client의 접속을 받아들일 수 있는 **LISTEN** state로 대기한다
  - Client에서 통신을 시도할 때 `Syn` packet을 보내는데 client에서는 이 상태를 **SYN-SENT** state 라고 부른다
  - Client의 `Syn` 을 받은 server는 **SYN-RECEIVED** state로 변경되고, `Syn`, `Ack`로 응답한다
  - 응답을 받은 client는 **ESTABLISHED** state로 변경하고 그에 대한 응답을 server에 보낸다
  - Server에서도 client의 `Ack` 응답을 받고 **ESTABLISHED** state로 변경된다
    - **ESTABLISHED** state는 server와 client 간의 연결이 성공적으로 완료되었음을 나타낸다!

  ![3-Way-Handshake](../images/3-Way-Handshake.jpg)

- `3-Way Handshake`  과정이 생기다보니 어떤 packet이 새로운 연결 시도이고 기존에 대한 응답인지 구분하기 위해 header에 **Flag**라는 값을 넣어 통신한다
  - **TCP Flags**
    - `SYN`
      - 연결 시작 용도로 사용한다
      - 연결이 시작될 때 SYN Flag에 1로 표시해 보낸다
    - `ACK`
      - ACK 번호가 유효할 경우 1로 표시해 보낸다
      - 초기 SYN이 아닌 모든 packet은 기존 message에 대한 응답이므로 ACK flag가 1로 표기된다
    - `FIN`
      - 연결 종료 시 1로 표시된다
      - Data 전송을 마친 후 **정상적으로 양방향 종료** 시 사용된다
    - `RST`
      - 연결 종료시 1로 표시된다
      - 연결 강제 종료를 위해 **연결을 일방적으로 끊을 때** 사용된다
    - `URG`
      - 긴급 data인 경우 1로 표시해 보낸다
    - `PSH`
      - Server측에서 전송할 data가 없거나 data를 buffering 없이 응용 프로그램으로 즉시 전달할 것을 지시할 때 사용된다

<br>

<br>

## 3. UDP

- TCP와 달리 UDP는 Layer 4 protocol이 가져야 할 특징이 거의 없다
  - 4계층에서는 **신뢰성 있는 통신**을 위해 아래와 같은 작업을 수행했다
    - **연결을 미리 확립 (3-Way Handshake)**
    - Data를 잘 **분할**하고 **조립**하기 위해 `packet 번호`를 부여하고 수신된 data에 대해 응답
    - Data를 특정 단위(`Window Size`)로 보내고 memory에 유지하다가 `ACK Number`를 받은 후 통신이 잘 된 상황을 파악하고나서야 memory에서 이 data들을 제거
    - 만약 중간에 **유실**이 있으면 `Sequence Number`와 `ACK Number`를 비교해가며 이를 파악하고, memory에 유지해놓은 data를 이용해 **재전송**
      - 이 기능을 이용해 data 유실이 발생하거나 순서가 바뀌더라도 바로 잡을 수 있음
  - UDP에는 위의 TCP와 같은 기능이 전혀 없다
- UDP header는 TCP와 비교하면 내용이 거의 없다
  - UDP에는 4계층의 특징인 **신뢰 통신**을 위한 내용 (`Sequence Number`,`ACK Number`, `Flag`, `Window Size`) 이 없다

- Data 통신은 data 전송의 **신뢰성**이 핵심이다
  - application에서 걱정하지 않고 data를 만들고 사용하는 것이 data 통신의 목적이지만,
  - UDP는 **data 전송을 보장하지 않는 protocol** 이므로 제한된 용도로만 사용된다
- UDP는 음성 data나 실시간 streamnig과 같이 **시간에 민감한** protocol이나 application을 사용하는 경우나 사내 방송이나 증권 시세 데이터 전송에 사용되는 `multicast` 처럼 **단방향**으로 **다수의 단말**과 통신에 응답을 받기 어려운 환경에서 주로 사용된다
  - Data를 전송하는데 **신뢰성**보다 일부 data가 유실되더라도 시간에 맞추어 계속 전송하는 것이 중요한 화상회의 시스템과 같은 서비스의 경우 UDP를 사용한다
    - UDP는 중간에 data가 일부 유실되더라도 유실된 상태로 data를 처리한다!
- UDP는 TCP와 달리 통신 시작 전 `3-Way Handshake`와 같이 사전에 연결을 확립하는 절차가 없다
  - 그 대신 UDP에서 **첫 data**는 resource 확보를 위해 **Interrupt**를 거는 용도로  사용되고 유실된다
    - 그래서 UDP protocol을 사용하는 application이 대부분 이런 상황을 인지하고 동작하거나,
    - 연결 확립은 TCP protocol을 사용하고, application 끼리 모든 준비를 마친 후 실제 data만 UDP를 이용하는 경우가 대부분이다
- ex)
  - Netflix나 Youtube와 같이 **시간에 민감하지 않은** 단일 시청자를 위한 연결은 TCP를 사용한다
  - 실시간 화상회의 솔루션은 data 전송이 양방향으로 일어나고 **시간에 매우 민감**하게 반응하므로 TCP 이용 환경에서 data 유실이 발생하면 사용자는 network 품질이 나쁘다고 생각할 수 있으므로 UDP를 사용한다

<br>

### TCP vs UDP

| TCP                             | UDP                           |
| ------------------------------- | ----------------------------- |
| 연결 지향 (Connection Oriented) | 비연결형 (Connectionless)     |
| 오류 제어 수행 O                | 오류 제어 수행 X              |
| 흐름 제어 수행 O                | 흐름 제어 수행 X              |
| Unicast                         | Unicast, Multicast, Broadcast |
| 전이중 (Full Duplex)            | 반이중 (Half Duplex)          |
| Data 전송                       | 실시간 traffic 전송           |

<br>

`+`

#### Communication channels in telecommunications

- 단방향 통신(**simplex** communication)
  - 단방향 전송
  - ex) TV, Radio
- 반이중 통신(**half-duplex** communication)
  - 양방향으로 전송이 가능하지만, 동시에 양쪽에서는 전송할 수 없다
  - ex) 무전기
- 전이중 통신(**full-duplex** communication)
  - 동시에 양방향 전송이 가능하다
  - ex) 전화기
