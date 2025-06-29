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

<br>

<br>

### 2-3. Protocol 변환

- `Router`의 또 다른 역할은 **서로 다른 protocol**로 구성된 network를 **연결**하는 것이다
- 현대 network는 `Ethernet`으로 수렴되기 때문에 protocol 변환의 역할이 많이 줄었지만, 과거에는 LAN에서 사용하는 protocol과 WAN에서 사용하는 protocol이 전혀 다른, 완전히 구분된 공간이었다
  - LAN은 다수의 컴퓨터가 서로 통신하는 데 초점을 맞추었고, WAN은 원거리 통신이 목적이었다
  - LAN 기술이 WAN 기술로 **변환**되어야만 Internet과 같은 **원격지 네트워크와의 통신**이 가능했고, 이 역할을 `Router`가 담당했다
- `Router`는 Layer 3에서 동작하는 장비이므로 Layer 3 주소 정보를 확인하고, 그 정보를 기반으로 동작한다
  - Router에 packet이 들어오면 `Layer 2까지의 header 정보`를 **벗겨내고** `Layer 3 주소`를 **확인**한 후 `Layer 2 hearder 정보`를 새로 **만들어** 외부로 내보낸다
    - 그래서 router에 들어올 때의 packet Layer 2  header 정보와 나갈 때의 packet Layer 2 정보가 다른 것이다
    - 이 기능을 이용하면 전혀 다른 기술 간 변환이 가능하다!

<br>

<br>

## 3. 경로 지정 - Routing/Switch

- Router가 packet을 처리할 때는 크게 두 가지 작업을 수행한다
  1. 경로 정보를 얻어 **경로 정보를 정리**하는 역할
  2. 정리된 경로 정보를 기반으로 **packet을 forwarding** 하는 역할
- Router는 자신이 분명히 알고 있는 주소가 아닌 목적지를 가진 packet이 들어오면 해당 packet을 버리므로, 들어오기 전에 **경로 정보를 충분히 수집**하고 있어야 router가 정상적으로 동작한다
  - Router는 복잡하고 많은 경로 정보를 얻어 **최적의 경로 정보**인 `routing table`을 적절히 유지해야 한다
- Router는 다양하고 많은 경로 정보를 얻을 수 있지만, 원하는 목적지 정보와 정확히 일치하지 않는 경우가 더 많다
  - Router는 **subnet 단위**로 routing 정보를 습득하고, routing 정보를 **최적화**하기 위해 `summary 작업`을 통해 여려 개의 subnet 정보를 **뭉쳐 전달** 한다
    - 그래서 router에 들어온 packet의 목적지 주소와 router가 갖고 있는 routing table 정보가 **정확히 일치하지 않더라도** (not exact match), 수많은 정보 중 목적지에 **가장 근접한 정보**를 찾아 packet을 forwarding 해야한다

<br>

### 3-1. Routing 동작과 Routing Table

- 현대 network에서는 단말부터 목적지까지의 경로를 모두 책임지는 것이 아니라 **인접한 router**까지만 경로를 지정하면,
  - 인접 router에서 최적의 경로를 파악한 후,
  - router로 packet을 forwarding 한다
- Network를 한 단계씩 뛰어넘는다는 의미로 이 기법을 `Hop by Hop routing`이라고 부르고, 인접한 router를 `Next Hop`이라고 부른다
  - Router는 packet이 목적지로 가는 전체 경로를 파악하지 않고, 최적의 `next hop`을 선택해 보내준다

<br>

#### `Next Hop`을 지정하는 방법

1. 다음 router의 IP를 지정 (Next hop IP address)
2. Router의 `outbound interface`를 지정
3. Router의 `outbound interface`와 다음 router의 IP를 동시에 지정

<br>

- Router에서 next hop을 지정할 때는 일반적으로 **상대방 router**의 `Interface IP address`를 지정하는 방법을 사용한다
- 특수한 경우에만 router의 `outbound interface`를 지정하는 방법을 쓸 수 있는데, 상대방의 `next hop IP`를 모르더라도 **MAC 주소 정보**를 알아낼 수 있을 때만 사용할 수 있다
  - 특수한 경우들
    1. WAN 구간 전용선에서 `PPP(Point-to-Point)`나 `HLDC(High Level Datalink Control)`와 같은 protocol을 사용해 **상대방의 MAC 주소를 알 필요가 없을 때**
    2. 상대방 router에서 proxy ARP가 동작해 정확한 IP 주소를 모르더라도 상대방의 MAC 주소를 알 수 있을 때
       - ARP란?
         - Address Resolution Protocol
         - 상대방의 MAC 주소를 알아내기 위해 사용되는 protocol
- Router가 packet을 어디로 forwarding할지 경로를 선택할 때는 **출발지를 고려하지 않는다**
  - 출발지와 상관없이 **목적지 주소**와 **routing table**을 비교해 어느 경로로 forwarding 할지 결정한다
    - 그래서 routing table을 만들 때
      - **목적지 정보만 수집**하고,
      - packet이 들어오면 목적지 주소를 확인해
      - packet을 **next hop으로 forwarding**한다

<br>

#### Routing Table에 저장하는 data

1. 목적지 주소
2. Next hop IP 주소, local outbound interface (optional!)

- Router에서 packet의 출발지 주소를 이용해 routing 하도록 `PBR (Policy-Based Routing)` 기능을 사용할 수 있지만, 목적지 주소만 수집하는 routing table로는 이 기능을 활성화 할 수 없고, router 정책과 관련된 별도 설정이 필요하다
  - PBR 기능을 사용하면 관리가 어려워지고, 문제가 발생하면 해결이 어려우므로 특별한 목적으로만 사용한다

<br>

#### 루프가 없는 (Loop Free) Layer 3: TTL (Time To Live)

- Layer 3의 IP header에는 `TTL` 이라는 field가 있다
  - 이 field는 packet이 network에 살아 있을 수 있는 시간(Hop)을 제한한다!
- Internet 구간에서 쓸모없는 packet이 돌아다녀 대역폭을 낭비하는 것을 막기 위해 router는 **주소가 불분명한 packet을 버린다**
- but, 운영되던 사이트가 갑자기 없어지는 경우가 생길 수 있고, 대안 경로를 찾다가 순간적으로 마주보는 두 대의 router의 next hop이 각각 상대방으로 구성되어 packet이 두 router 사이에서 계속 오가는 경우가 생길 수도 있다
  - 이럴 경우 두 router 간의 잘못된 routing으로 **L3 Loop**가 발생하게 된다
- 이렇게 packet이 영구적으로 사라지지 않는다면, 장비 간에 동일한 packet이 ping-pong을 치거나 Internet에 사라지지 않는 유령 packet이 넘쳐날 것이다
  - 그래서, 모든 packet은 **TTL**이라는 수명값을 가지고 있고, 이 값이 0이 되면 Network 장비에서 버려진다
- 여기서 `TTL`은 **실제 초와 같은 시간** 이 아니라, `hop` 을 지칭하며, 하나의 `hop` 을 **지날 때마다** TTL 값은 1씩 줄어든다

<br>

<br>

### 3-2. Routing (Router가 경로 정보를 얻는 방법)

Router가 경로 정보를 얻는 방법은 크게 3가지로 구분할 수 있다

1. `Direct Connected`
2. `Static Routing`
3. `Dynamic Routing`

위의 3가지 방법을 이용해 경로 정보를 수집하고, 수집된 경로 정보 중 목적지에 대한 **최적의 경로**를 선정해 `Routing Table`을 만든다

 <br>

#### 1. Direct Connected

- IP 주소를 입력할 때 사용된 **IP 주소**와 **Subnet mask**로 해당 IP 주소가 속한 **Network 주소 정보**를 알 수 있다
  - Router나 PC에선 이 정보로 해당 Network에 대한 Routing Table을 자동으로 만든다
    - 이 경로 정보를 `Direct Connected` 라고 한다.
- `Direct Connected`로 생성되는 경로 정보는 Interface에 IP를 설정하면 **자동으로 생성되는 정보**이므로,
  - 정보를 강제로 **지울 수 없고**,
  - 해당 Network 설정을 삭제하거나 해당 Network Interface가 **비활성화**되어야만 **자동으로 사라진다**

<br>

#### 2. Static Routing

- 관리자가 `목적지 Netowrk`와  `Next hop` 을 router에 **직접 지정**해 **경로 정보를 입력** 하는 것을 `Static Routing` 이라고 한다
  - `Static Routing`은 관리자가 경로를 직접 지정하므로, routing 정보를 매우 **직관적**으로 설정, 관리할 수 있다
- `Static Routing`은 `Direct Connected` 처럼 연결된 Network Interface 정보가 삭제되거나 비활성화되면 **연관된 Static Routing 정보가 자동으로 삭제** 된다.
  - but, Physical Interface가 아닌 Logical Interface는, Physical Interface가 비활성화되더라도 함께 비활성화되지 않는 경우도 있어 Routing Table에서 사라지지 않을 수 있다.

<br>

#### 3. Dynamic Routing

- `Static Routing`은 관리자가 변화가 적은 network에서 network를 손쉽게 관리할 수 있는 좋은 방법이지만, 큰 network는 `Static Routing` 만으로는 관리하기 어렵다
  - why?
    - `Static Routing` 적용 시 **장애로 인한 network** 경로 반영이 되지 않는다!
      - `Static Routing`은 **router 너머 다른 router의 상태 정보를 파악할 수 없기 때문에** router 사이의 회선이나 router에 장애가 발생하면, **장애 상황을 파악**하고 **대체 경로로 packet을 보낼 수 없기 때문**!
- `Dynamic Routing`은 이러한 `Static Routing` 의 단점을 보완하여, **router 끼리 자신이 알고 있는 경로 정보나 링크 상태 정보를 교환**해 전체 network 정보를 학습한다
  - 주기적 or 상태 정보가 변경될 때 router끼리 경로 정보가 교환되므로, router를 연결하는 회선이나 router 자체에 장애가 발생하면, 이 상황을 인지해 **대체 경로로 packet을 forwarding** 할 수 있다
- `Dynamic Routing` 에서는 **자신이 광고할 network를 선언**해주어야 한다
-
