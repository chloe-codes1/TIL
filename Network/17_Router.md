# Router

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

## 1. What is Router?

- `Router`는 **layer 3**에서 동작하는 여러 network 장비의 대표격으로, 이름처럼 **경로를 지정**해주는 장비이다
- `Router`에 들어오는 packet의 **목적지 IP 주소**를 확인하고, 자신이 가진 경로(`Route`) 정보를 이용해 packet을 **최적의 경로**로 **forwarding**한다
- `Router`는 **원격지 network**와 연결할 때 필수 network 장비이며, network를 구성하는 핵심 장비이다
  - 서로 다른 network 간에 통신할 때 `router`가 반드시 필요하다!

<br>

### Router vs L3 Switch

- `Switch`는 대표적인 2계층 장비이지만, router처럼 3계층에서 동작하는 `L3 Switch`라고 부르는 장비도 많이 사용되고 있다
- 기존에 Router는 software로 구현하고, switch는 hardware로 구현하는 형태로 구분하거나 다양한 기능의 router와 packet을 빨리 보내는 데 최적화 된 switch로 구분했었다
  - 최근에는, 기술 발달로 `Router`와 `L3 switch`를 구분하기는 어렵다
    - 이 문서에서 말하는 내용은 router로 설명하고 있지만, L3 switch로도 모두 동일하게 적용되는 내용이다!

<br>

<br>

## 2. How Does a Router Work?

- `Router`는 **다양한 경로 정보**를 수집해 **최적의 경로**를 `routing table`에 저장한 후, 
  - `packet`이 router로 들어오면 도착지 IP 주소와 routing table을 비교해 최선의 경로로 packet을 내보낸다
- Switch와 반대로 router는 들어온 packet의 **목적지 주소**가 routing table에 없으면 **packet을 버린다**
- Router는 packet forwarding 과정에서 **기존 layer 2 header 정보**를 **제거**한 후 **새로운 layer 2 header**를 만들어낸다
- 위의 router 동작 방식을 `경로 지정`, `Broadcast control`, `Protocol 변환`이라고 한다

<br>

### 2-1. 경로 지정

- Router의 가장 중요한 역할은 **경로 지정**이다
  - 경로 정보를 모아 `routing table`을 만들고, `packet`을 **forwarding**한다
    - IP 주소는 `network 주소`와 `host 주소`로 나뉜 계층 구조를 기반으로 설계되어 local network와 원격지 network를 구분할 수 있고, network 주소를 기반으로 경로를 찾아갈 수 있다
    - Router는 이 IP 주소를 확인해 원격지에 있는 적절한 경로로 packet을 forwarding한다
- Router는 경로를 지정해 packet을 forwarding 하는 역할을 두 가지로 구분해 수행한다
  1. 경로 정보를 얻는 역할과
  2. 얻은 경로 정보를 확인하고, packet을 forwarding 하는 역할이다
- Router는 자신이 얻은 **경로 정보에 포함되는 packet만 forwarding**하므로 정확한 목적지 경로를 얻는 것이 매우 중요하다

<br>

#### Router가 경로 정보를 얻는 방법

- IP 주소를 입력하면서 자연스럽게 인접 Network 정보를 얻는 방법
- 관리자가 직접 경로 정보를 입력하는 방법
- Router끼리 서로 경로 정보를 자동으로 교환하는 방법

<br>

<br>

### 2-2. Broadcast Control

- `Switch`는 packet의 **도착지 정보**를 모르면 어딘가에 존재할지 모를 장비와의 통신을 위해 **flooding**해 packet을 모든 포트에 전송한다
  - LAN 어딘가에 도착지가 있을 수 있다고 가정하고 packet을 전체 network에 flooding 하는 것이 쓸모없는 packet이 전소오디어 전체 network의 성능에 무리가 갈 수 있다고 생각할 수 있지만, 
    - LAN은 크기가 작아 **flooding에 대한 영향이 작고**, 
    - 도착지 network interface card(NIC)에서 **자신의 주소와 packet 도착지 주소가 다르면** packet을 버리기 때문에 이런 flooding 작업은 **network에 큰 무리를 주지 않는다**
- 반면 `Router`는 **packet을 원격지로 보내는 것을 목표**로 개발되어 **Layer 3에서 동작**하고, **분명한 도착지 정보가 있을 때만** 통신을 허락한다
  - Internet 연결은 대부분 지정된 대역폭만 빌려 사용하므로, **쓸모없는 통신이 network를 차지**하는 것을 최대한 막으려고 노력한다
    - 만약 LAN에서 switch가 동작하는 것처럼 
      - 목적지가 없거나
      - 명확하지 않은 packet이 flooding 된다면,
    - Internet에 쓸모 없는 packet이 가득 차 **통신불능** 상태가 될 수 있다
- `Router`는 **바로 연결되어 있는 network 정보**를 제외하고 **경로 습득 설정**을 하지 않으면 packet을 **forwarding 할 수 없다**
  - Router의 기본 동작은 `multicast 정보`를 습득하지 않고, `broadcast packet`을 전달하지 않는다
    - Router의 이 기능을 이용해 **broadcast가 다른 network로 전파**되는 것을 막을 수 있다
      - 이 기능을 `Broadcast / Multicast Control` 이라고 한다
  - Network에 broadcast가 많이 발생하는 경우, router로 network를 분리하면 broadcast network를 분할해 network **성능**을 높일 수 있다

