# Network Components

> 네트워크를 구축하고 사용하는데 필요한 구성 요소들을 알아보아요
>
> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

### 1. 네트워크 인터페이스 카드 (NIC)

- 흔히 `랜 카드`라고 부르는 부품의 정식 명칭은 **네트워크 인터페이스 카드 (Network Interface Card, NIC)**이다
  - NIC 외에도 `Network Card`, `Network Interface Controller` 라고도 부른다
- NIC는 **컴퓨터**를 **network**에 연결하기 위한 **하드웨어 장치**이다

<br>

#### NIC의 주요 역할

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

#### Multifunction NIC

- 네트워크 전송 기술로 `Ethernet`만 사용되는 것은 아니다
  - **Storage**와 **server**를 연결하는 `SAN (Storage Area Network)` 구성용 **Fibre Channel** 표준이 있고,
  - `Ethernet`에서 storage network를 구성하기 위한 **iSCSI protocol**도 있다
  - `슈퍼 컴퓨터`와 같이 여러대의 서버를 묶어 고성능 clustering을 구현할 수 있는 **HPC (High Performance Computing)** network에는 **InfiniBand** 기술도 사용된다
- 최근 이런 다양한 protocol이 `Ethernet` 기반으로 변화하고 있지만, 
  - 아직도 이런 다양한 Protocol이 일부 network에서 사용 중이며
  - 이런 특수 network를 지원하고 가속할 수 있는 network card도 사용되고 있다