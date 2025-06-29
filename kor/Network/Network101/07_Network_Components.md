# Network Components

> 네트워크를 구축하고 사용하는데 필요한 구성 요소들을 알아보아요
>
> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

## 1. 네트워크 인터페이스 카드 (NIC)

- 흔히 `랜 카드`라고 부르는 부품의 정식 명칭은 **네트워크 인터페이스 카드 (Network Interface Card, NIC)**이다
  - NIC 외에도 `Network Card`, `Network Interface Controller` 라고도 부른다
- NIC는 **컴퓨터**를 **network**에 연결하기 위한 **하드웨어 장치**이다

<br>

### NIC의 주요 역할

- **직렬화 (Serialization)**
  - 네트워크 인터페이스 카드는 **전기적 신호**를 **데이터 신호 형태**로 또는 **데이터 신호 형태**를 **전기적 신호 형태**로 **변환**해준다
  - NIC 외부 cable에서는 **전기 신호** 형태로 data가 전송되는데 이러한 **상호 변환 작업**을 `직렬화` 라고 한다
- **MAC 주소**
  - 네트워크 인터페이스 카드는 MAC 주소를 가지고 있다
  - **받은 packet의 도착지 주소**가 자신의 MAC 주소가 아니면 **페기**하고, 자신의 주소가 맞으면 system 내부에서 처리할 수 있도록 **전달**한다
- **흐름 제어 (Flow Control)**
  - `Packet` 기반 네트워크에서는 다양한 통신이 **하나의 채널**을 이용하므로 이미 통신중인 data 처리 때문에 새로운 데이터를 받지 못할 수 있다
    - 이런 현상으로 **데이터 유실 방지**를 위해 **데이터를 받지 못할 때**는 상재방에게 **통신 중지를 요청**할 수 있고, 이 작업을 `흐름 제어` 라고 한다

<br>

### Multifunction NIC

- 네트워크 전송 기술로 `Ethernet`만 사용되는 것은 아니다
  - **Storage**와 **server**를 연결하는 `SAN (Storage Area Network)` 구성용 **Fibre Channel** 표준이 있고,
  - `Ethernet`에서 storage network를 구성하기 위한 **iSCSI protocol**도 있다
  - `슈퍼 컴퓨터`와 같이 여러대의 서버를 묶어 고성능 clustering을 구현할 수 있는 **HPC (High Performance Computing)** network에는 **InfiniBand** 기술도 사용된다
- 최근 이런 다양한 protocol이 `Ethernet` 기반으로 변화하고 있지만,
  - 아직도 이런 다양한 Protocol이 일부 network에서 사용 중이며
  - 이런 특수 network를 지원하고 가속할 수 있는 network card도 사용되고 있다

<br>

<br>

## 2. Cable and Connector

- 노트북이나 스마트폰, 태블릿에서 인터넷 연결을 위한 **무선 사용 빈도**가 점점 높아지고 있지만 회사 network에 접속하거나 server를 network와 연결하는 것과 같이 **신뢰도 높은 통신**이 필요한 경우에는 아직도 **유선**이 사용되고 있다
  - 이런 연결을 위해 제일 먼저 고려할 network 연결점은 **cable**이다
- **Cable**은 `Twisted Pair`, `동축 (Coaxial) cable`, `광 (Fiber-optic) cable` 3가지가 있다
  - 원하는 환경에 맞는 cable을 올바로 선택하려면 cable을 구성하는 **기본 요소**와 **표준**을 알아야 한다

<br>

### 2-1.  Ethernet network 표준

- 현재 대중화되어 있는 Ethernet 표준은 **기가 비트 이더넷**과 **10기가비트 이더넷**이다
  - 일반 PC 같은 종단은 기가비트 이더넷을, data center의 server와 같은 종단은 기가비트나 10기가비트 ethernet을 주로 사용하고 있다
  - Server와 switch 간 연결을 10기가비트 Ethernet으로 구성할 경우, switch에서는 상위 switch와의 연결을 위한 **업링크 대역폭**을 확보하기 위해 **40기가비트**나 **100기가비트** Ethernet을 사용한다
- Ethernet에서도 **cable의 종류**, **encoder의 종류** 등으로 세분화해 여러 가지 표준으로 나뉘지만 대중적으로 많이 사용되는 표준은 3가지이다
  1. **1,000BASE-T/10GBASE-T**
     - `Twisted pair cable`을 이용하는 기가 Ethernet 표준이다
  2. **1,000BASE-SX/10GBASE-SR**
     - `Multi-mode 광케이블`을 사용하고 **비교적 짧은 거리**를 보낼 수 있는 Ethernet 표준이다
  3. **1,000BASE-LX/10GBASE-LR**
     - `Single-mode 광케이블`을 사용하고 **비교적 긴 거리**를 보낼 수 있는 Ethernet 표준이다

<br>

기가비트 Ethernet 표준 중 하나인 **1,000BASE-T**로 각 명칭의 의미를 설명하자면,

- 앞에 숫자 1,000은 **속도**를 나타낸다
  - 앞 숫자가 1,000이면 **1,000Mbps 속도**로 통신할 수 있는 networkDㅣ다
- 중간 문자는 **채널의 종류**에 대한 것으로
  - `BASE`는 **단일채널 통신**을 나타내고,
  - `BROAD`는 **다채널 통신**을 나타낸다
- 마지막 문자는 **cable type**을 나타낸은 것으로
  - `T` 문자는 **Twisted Pair cable**을 나타낸다
  - 마지막 문자에 의해 cable과 그에 맞춘 광신호, 트랜시버의 종류가 달라진다

<br>

### 2-2. Cable과 Connector의 구조

- cable은 물리적으로 `cable 본체`, `connector`, `transceiver`와 같은 여러 요소로 나뉜다
  - cable 본체는 **Twisted Pair**, **동축**, **광케이블**로 나뉘고
  - cable 본체의 종류에 따라 **connector**와 **transceiver**의 종류도 함께 달라진다
- `Twisted Pair Cable`의 경우 connector와 본체가 하나로 구성되어 있고, 별도의 transceiver가 없는 경우가 많다
- `광케이블`은 다양한 속도와 거리를 지원해야 하므로 transceiver, connector와 cable을 분리하는 경우가 많다

<br>

### 2-3. Cable - Twisted Pair Cable

- 가장 흔히 사용하는 cable은 `Twisted Pair` cable이다
- Twisted Pair cable은 **RJ-45** connector를 이용하고 cable 본체와 함께 연결되어 **분리할 수 없다**
- 컴퓨터나 server에 있는 **LAN port**에 끼우면 network에 연결된다
- **Twisted Pair cable의 종류**
  - 그물 형태의 shield가 있는 **STP (Shielded Twisted Pair)** cable
  - foil 형태의 shiled가 있는 **FTP (Foil Twisted Pair)** cable
  - shield가 없는 **UTP (Unshielded Twisted Pair)** cable
- shield가 twisted 된 pair마다 있는 경우와 전체 cable을 보호하기 위한 shield가 있는 경우에 따라 **STP/FTP**와 같은 cable이 사용되기도 한다
  - **STP/FTP**의 각 pair에는 foil로 shield되어 있고, 전체 cable을 보호하는 shield가 있는 cable이다
    - 이것은 **내부 간섭**과 **외부 간섭** 모두 잘 막아줄 수 있다!
- **Twisted Pair cable의 등급**
  - Twisted Pair cable은 `category` 단위로 cable 등급을 나눈다
  - 가장 많이 사용하는 cable은 **category 5E** cable 이다
    - **1G** 속도를 지원하는 대중적인 cable로 desktop, laptop과 같은 **일반 단말**을 연결하는 데는 **적합**하지만,
    - data center와 같이 **높은 대역폭**을 지원해야 할 때는 **적합하지 않다**

<br>

### 2-4. Cable - 동축 케이블

- `동축 케이블`은 cable TV와 ㅇ연결할 때 사용하는 두꺼운 검정 cable과 같은 종류이다
- 과거에는 **LAN 구간**에도 사용되었지만, **다루기 힘들고 고가**이므로 잘 사용되지 않고 cable TV나 internet 연결을 위해서만 사용되어 왔다
  - 하지만 최근에는 **10G 이상**의 **고속 연결**을 위해 **transceiver를 통합**한 `DAC (Direct Attach Copper)` cable을 많이 사용하는데 이 cable은 **동축 케이블** 중 하나이다

<br>

### 2-5. Cable - 광케이블

- 광케이블은 일반적으로 다른 구리선 (`UDP`, `동축`) 보다 **신뢰도**가 높고, 더 **먼 거리까지 통신**할 수 있어 **높은 대역폭**을 요구하거나 **먼거리를 통신**해야 하는 network 장비 간의 통신에 주로 사용된다
- cable은 **저항** 때문에 생기는 **감쇄**와 **주위 자기장**의 **간섭**으로부터 보호받아야 하는데 `광신호`를 기반으로 한 광케이블은 이런 **감쇄와 간섭으로부터 비교적 자유롭다**
- 광케이블은 `Single mode`와 `Multi mode` 2가지로 나뉜다
  - `Single mode`
    - **먼 거리 통신**을 지원하기 위헤 **cable 굵기가 매우 가늘고**, 신호를 보내는 광원으로 **레이저**를 사용한다
      - 레이저는 다른 빛에 비해 먼 거리를 퍼지지 않고 직진하는 성질이 있다
    - 하나의 레이저 신호로 가느다란 전송로를 통과하므로 single mode라고 부른다
    - **반사 각도가 작은** single mode가 훨씬 더 **먼 거리**로 전송할 수 있다
    - single mode cable은 **노란색**이다
  - `Multi mode`
    - single mode에 비해 **비교적 굵은 cable**을 사용하며 광원으로 **LED**를 사용한다
      - LED 광원은 레이저보다 쉽게 구현할 수 있어 multi mode cable과 transceiver 모두 가격이 single mode보다 저렴하다
    - 넓은 광 전송로에 **여러 가지 광원**이 전송되므로 multi mode 라고 한다
    - multi mode cable은 **주황색 (1G)**과 **하늘색(10G)**이다

<br>

### 2-6. Connector

- connector는 cable의 끝부분으로 **network 장비**나 **network card**에 연결되는 부분이다
- Twisted Pair cable에서는 `RJ-45` connector를 사용하지만 광케이블은 다양한 connector가 있다
  - 광케이블은 주로 **LC connector**가 사용되고, **S3 connector**가 일부 사용된다
  - server에 광케이블을 사용하는 경우, network 연결 요청 시 connector type을 network 담당자에게 알려주어야만 적합한 cable을 사용할 수 있다

<br>

### 2-7. Transceiver

- Transceiver는 **외부 신호**를 computer 내부의 **전기 신호**로 **바꾸어**준다
- Tranceiver가 별도로 구분되지 않던 과거에는 다양한 `Ethernet 표준`과 cable을 만족하기 위해 network 장비나 NIC를 별도로 구매해야 했다
  - cable이 변경되면 network 장비와 NIC도 함께 변경해야 하는 문제를 해결하고 서로 다른 **다양한 network 표준**을 **혼용**해 사용할 수 있도록 transceiver를 사용한다
- Tranceiver 중 하나인 **GBIC (지빅)**은 초기 개발된 module 이름이고 이후 **SPF**나 **SPF+**와 같은 **상위 표준**이 나왔지만
  - 일반적으로 tranceiver 전체를 **GIBC**으로 통칭해 부르기도 한다
- 정확히 구분하자면,
  - **GBIC (GigaBit Interface Converter)**은 **SC type** connector 를 연결할 수 있는 interface이다
    - SC type connector는 광케이블에 주로 사용되는 connector이다
  - **SFP (Small Form-Factor Pluggable**는 **LC type**  connector를 연결 할 수 있다

- **Transceiver 없이** 전용 interface를 사용하면 길이나 속도마다 다른 network 장비나 NIC를 별도로 구매해야 하지만,
  - **Transceiver만 변경**하면 **통신 길이**와**속도**를 조절할 수 있어 최근 생상되는 대부분의 network 장비와 NIC는 transceiver를 지원하고 있다

<br>

<br>

## 3. Hub

- Hub는 cable과 동일한 **1계층 (Physical Layer)**에서 동작하는 장비이다
- Hub는 거리가 멀어질수록 줄어드는 전기 신호를 **재생성**해주고, HUB라는 용어 그대로 여러대의 장비를 **연결**할 목저으로 상요된다
- Hub는 단순히 **들어온 신호를 모든 port로 내보내** netowrk에 접속된 모든 단말이 **경쟁**하게 되므로 전체 network 성능이 줄어드는 문제가 있고,
  - `packet`이 **무한 순환**해 network 전체를 마비시키는 **loop**와 같은 다양한 **장애 원인**이 되어 hub는 현재 **거의 사용되지 않고** 있다

<br>

<br>

## 4. Switch

- Switch는 Hub와 동일하게 **여러 장비를 연결**하고 **통신을 중재**하는 **2계층(Data Link Layer) 장비**이다
- Switch는 **Hub의 역할**과 **통신을 중재**하는 2가지 역할을 모두 수행하므로 **Switching Hub**라고도 불린다
- Hub는 **단순히 전기신호를 재생성**해 출발지를 제외한 모든 port에 전기 신호를 내보내지만,
  - Switch는 Hub와 달리 **MAC 주소를 이해**할 수 있어 **목적지 MAC 주소의 위치를 파악**하고 정확한 목적지가 연결된 port로만 전기 신호를 보낸다
    - ex) A, B, C, D server가 있을 때 A에서 C로 통신해야 하는 상황에서
      - `Hub`는 A가 전기신호를 보내면 출발지 Port를 제외한 HUB에 있는 모든 port인 B, C, D에 전기 신호를 흘리지만,
      - `Switch`는 C로만 전기신호를 보낸다
        - B, D는 이번 통신의 영향을 전혀 받지 않아 그 사이 다른 통신을 **동시에** 수행할 수 있게 된다
- `Hub`는 **무전기**처럼 송수신을 동시에 할 수 없고 **한쪽 방향으로만 동작**하지만,
- `Switch`는 **전화기**처럼 송수신을 **동시에** 할 수 있다

<br>

<br>

## 5. Router

- Network 크기가 점점 커지면서 **먼 지역**에 위치한 network와 통신해야 하는 요구사항이 늘어나면서 router가 필요해졌다
- Router는 OSI 7계층 중 **3계층 (Network Layer)**에서 동작하면서 **먼 거리**로 통신할 수 있는 protocol로 변환한다
- Router는 원격지로 쓸데없는 packet이 전송되지 않도록 **broadcast**와 **multicast**를 control하고, **불분명한 주소**로 통신을 시도할 경우 이를 버린다
  - **정확한 방향**으로 packet이 전송되도록 **경로를 지정**하고 **최적의 경로**로 packet을 **forwarding** 한다
    - 즉, router의 역할은 **network 주소 확인** 후 **경로 지정**이다
- 최근 일반 사용자가 Router 장비를 접하기는 어렵지만, router와 유사한 역할을 하는 `L3 Switch`와 `공유기`는 쉽게 찾아볼 수 있다

<br>

<br>

## 6. Load Balancer

- 일반적으로 Load Balancer는 OSI 7계층 중 **4계층 (Transport Layer)**에서 동작한다
- `application layer`에서 application protocol의 특징을 이해하고 동작하는 `7계층 Load Balancer`를 별도로 **ADC (Application Delivery Controller)**라고 부른다
- **L4 Switch**라고 부르는 network 장비도 load balancer의 한 종류로, `switch`처럼 **여러 port**를 가지고 있으면서 **load balancer 역할**을 하는 장비를 지칭한다
- Load Balancer는 **4계층 port 주소를 확인**하는 동시에 **IP 주소를 변경**할 수 있다
- Load Balancer가 가장 많이 사용되는 service는 **Web**이다
  - Web server 를 **증설**하고싶을 때 load balancer를 web server 앞에 두고 web server를 여러 대로 늘려준다
    - **대표 IP**는 load balancer가 갖고, load balancer가 각 web server로 **packet의 목적지 IP 주소**를 **변경**해 보내준다
  - 이런 원리를 이용해 여러 대의 web server가 동시에 동작해 서비스 **성능**을 높여주는 동시에
  - 일부 web server에 문제가 발생하더라도 빠른 시간안에 서비스가 **복구**되도록 도와준다
    - 이런 기능을 위해 load balancer는 IP 변환 외에도 **service health check** 기능이나 **대용량 session 처리 기능**이 있다!

<br>

<br>

## 7. 보안 장비 (방화벽/IPS)

- 대부분의 network 장비는 **정확한 정보 전달**에 초점이 맞추어져 있지만,
  - 보안 장비는 정보를 잘 **제어**하고 **공격을 방어**하는데 초점이 맞추어져 있다
- **방어 목적**과 보안 장비가 **설치되는 위치**에 맞추어 다양한 보안 장비가 사용된다
- 일반적으로 가장 유명한 보안 장비는 **방화벽**이다
  - `방화벽`은 OSI 7계층 중 **4계층 (Transport Layer)**에서 동작해 방화벽을 통과하는 **packet의 3, 4게층 정보**를 확인하고,
  - packet을 **정책과 비교**해 버리거나 forwarding 한다

<br>

<br>

## 8. 기타 (모뎀/공유기)

### 8-1. 공유기

- 거의 모든 가정이나 작은 회사에서 사용하는 `공유기`는 **2계층 switch**, **3계층 router**, **4계층 NAT와 방화벽** 기능을 한곳에 모아놓은 장비이다
- 공유기 내부는 `Switch 부분`, `무선 부분`, `Router 부분` 회로로 나뉜다
  - 겉으로는 하나의 장비처럼 보이자만 내부저긍로는 크게 **switch**와 **무선 AP**, **Router** 로 구분되는 복잡한 장비이다

<br>

### 8-2. Modem

- `Modem`은 **짧은 거리를 통신하는 기술**과 **먼 거리를 통실하는 기술**이 달라 이 기술들을 **변환**해 주는 장비이다
- 공유기의 `LAN (Local Area Network)` port와 `WAN (Wide Area Network)` port는 모두 일반 Ethernet에서 100m 이상 먼 거리로 data를 보내지 못하므로 **먼 거리 통신이 가능한 기술**로 **변환**해주는 modem이 별도로 필요하다
- 통신사업자 netowrk 종류와 쓰이는 기술에 따라 여러 종류의 modem이 사용된다
  - `기가 인터넷`의 경우 대부분 **FTTH (Fiber To THe Home) modem**을 사용하고,
  - `동축 케이블 인터넷`은 **Cable modem**,
  - `전화선`을 사용할 경우 **ADSL (Asymmetric Digital Subscriber Line) modem**, **VDSL (Very high bit-rate Digital Subscriber Line) modem** 을 사용한다

<br>
