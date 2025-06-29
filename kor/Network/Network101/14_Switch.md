# Switch

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

## Before Getting Started

<br>

### Switch 란?

- Network의 가장 핵심장비인 **Switch**는 2계층 주소인 `MAC 주소`를 기반으로 동작한다
- Switch는 network 중간에서 `packet`을 받아 **필요한 곳에만 보내주는** network의 **중재자 역할**을 한다
  - Switch는 아무 설정 없이 network에 연결해도 `MAC 주소`를 기반으로 **packet을 전달**하는 기본 동작을 수행할 수 있다
- Switch는 `MAC 주소`를 인식하고 packet을 전달하는 switch의 기본 동작 외에도
  - 한 대의 장비에서 **논리적으로 network를 분리**할 수 있는 `VLAN 기능`,
  - **Network Loop를 방지**하는 `STP (Spanning Tree Protocol)`과 같은 기능을 기본적으로 가지고 있다

<br>

<br>

## Swtich 장비 동작

- Switch는 network에서 **통신을 중재**하는 장비이다
- Switch가 없던 오래된 `Ethernet Network`에서는 **packet**을 전송할 때 서로 **경합**해 그로 인한 **network 성능 저하**가 컸다
  - 이런 경쟁을 없애고 packet을 **동시에 여러 장비가 서로 간섭 없이 통신**할 수 있도록 도와주는 장비가 `Switch` 이다
    - Switch를 사용하면 **여러 단말이 한번에 통신**할 수 있어 **통신하기 위해 기다리거나 충돌 때문에 대기** 하는 문제가 해결되고 network 전체의 **통신 효율성이 향상**된다
- Switch의 핵심 역할은 **누가 어느 위치에 있는지 파악**하고 실제 통신이 시작되면 자신이 알고 있는 위치로 **packet을 정확히 전송**하는 것이다
  - 이런 동작은 Swith가 **2계층 주소를 이해**하고,
    - 단말의 주소인 `MAC 주소`와 단말이 위치하는 `Interface 정보`를 mapping한 **MAC Address Table**을 갖고 있어서 가능하다
- Switch는 전송하려는 packet의 **header 안에 있는 2계층 목적지 주소**를 확인하고, MAC Address Table에서 해당 주소가 **어느 port에 있는지** 확인해 해당 packet을 **그 port로만 전송** 한다
  - 이런 역할을 수행하기 위해 Switch는 `MAC 주소`와 `port`가 mapping 된 **MAC Address Table**이 필요하다
    - 만약 Table이 없는 도착지 주소를 가진 packet이 switch로 들어오면,
      - Switch는 **전체 port로 packet을 전송**한다
    - Packet의 도착지 주소가 Table에 있으면,
      - **해당 주소가 mapping 된 port로만 packet을 전송**하고, 다른 port로는 전송하지 않는다
  - Switch의 위와 같은 동작 방식은 아래의 3가지로 정리할 수 있다
    1. Flooding
    2. Address Learning
    3. Fowarding/Filtering

<br>

### 1. Flooding

- Switch는 부팅하면 **network 관련 정보가 아무것도 없다**
  - 이때 switch는 **network 통신을 중재**하는 자신의 역할을 다하지 못하고 마치 **hub**처럼 동작한다
    - `Hub`는 들어온 port를 제외하고 **모든 port로 packet을 전달**한다
      - Switch가 hub와 같이 **모든 port로 packet을 흘리는 동작 방식**을 `Flooding`이라고 한다
- Switch는 packet이 들어오면 **도착지 MAC 주소를 확인**하고, 자신이 갖고 있는 MAC Address Table에서 해당 MAC 주소가 있는지 확인한다
  - MAC Address Table에 matching되는 목적지 MAC 주소 정보가 없으면 **모든 port에 같은 내용의 packet을 전송**한다
    - Switch는 `LAN`에서 동작하므로, 자신이 정보를 갖고 있지 않아도 **어딘가에 장비가 있을 수 있다**는 가정 하에 위와 같은 작업을 수행한다
- Flooding 동작은 Switch의 정상적인 동작이지만, 이런 동작이 많아지면 Switch가 제 역할을 못하게 된다
  - Packet이 switch에 들어오면 **해당 packet 정보의 MAC 주소**를 보고 이를 **학습**해 **MAC Address Table**을 만든 후 이를 통해 packet을 전송한다

<br>

#### 비정상적인 Flooding

- Switch가 packet을 flooding한다는 것은 **switch가 제 기능을 못한다**는 뜻이다
  - `Ethernet - TCP/IP` network에서는 **ARP Broadcast**를 미리 주고받은 후 data가 전달되므로 **실제로 data를 보내고 받을 때는 switch가 packet을 flooding 하지 않는다**
- Switch를 사용하면 **필요한 곳에만 packet을 forwarding**하므로 주변 통신을 **악의적으로 가로채기 힘들어** 모든 packet을 flooding하는 `hub` 에 비해 보안에 도움이 된다
  - 이런 switch의 기능을 무력화해 주변 통신을 모니터링하는 공격 기법이 사용된다
    - ex)
      - Switch에게 엉뚱한 MAC address를 습득시키거나
      - Switch의 MAC Address Table을 꽉 차게 해 switch **flooding 동작을 유도**할 수 있다
  - 만약 switch가 아무 이유없이 packet을 flooding 한다면,
    - Switch가 정상적으로 동작하지 않거나
    - 주변에서 공격이 수행되는 상황일 수 있다
- 이외에도 `ARP poisoning` 기법을 이용해 모니터링해야 할 IP의 MAC 주소가 공격자 자신인 것처럼 속여 원하는 통신을 받는 방법을 사용하기도 하므로 유의해야 한다

<br>

### 2. Address Learning

- Switch가 packet의 도착지 MAC 주소를 확인하여 **원하는 port로 forwarding**하는 switch의 동작을 정상적으로 수행하려면 **MAC Address Table**을 만들고 유지해야 한다
  - `MAC Address Table`은 어느 위치 (port)에 어떤 장비 (MAC 주소)가 연결되었는지에 대한 정보가 저장되어 있는 **임시 table**이다
    - 이런 **MAC Address Table을 만들고 유지하는 과정**을 `Address Learning`이라고 한다
- `Address Learning`은 packet의 **출발지 MAC 주소 정보**를 이용한다
  - Packet이 특정 port에 들어오면 switch에는 해당 packet의 **출발지 MAC 주소**와 **port 번호**를 MAC Addrss Table에 기록한다
    - 1번 port에서 들어온 packet의 출발지 MAC 주소가 AAAA라면, 1번 port에 AAAA MAC 주소를 가진 장비가 연결되어 있따고 추론할 수 있어 이런 방법으로 정보를 습득한다
- `Address Learning`은 MAC 주소 정보를 사용하므로 broadcast나 multicast에 대한 MAC 주소를 학습할 수 없다
  - 두 가지 모두 **목적지 MAC 주소 field**에서만 사용하기 때문이다!

<br>

#### 사전 정의된 MAC Address Table

- Switch는 `MAC address learning` 작업으로 주변 장비의 MAC 주소를 학습하는 것 외에도 **사전에 미리 정의된 MAC 주소 정보**를 가지고 있다
  - 이런 사전 정의된 주소는 packet을 처리하기 위한 주소가 아니라 대부분 **switch 간 통신을 위해 사용되는 주소**이다
  - 이러한 종류의 주소도 `MAC Address Table`에서 정보를 확인할 수 있는데 **switch에서 자체 처리되는 주소**는 특정 port로 내보내는 것이 아니라 switch에서 자체 처리하므로
    - 인접 port 정보가 없거나
    - CPU 혹은 관리 module을 지정하는 요어로 표기된다

<br><br>

### 3. Forwarding/Filtering

- Switch의 동작은 매우 간단한데, Packet이 switch에 들어온 경우
  - **도착지 MAC 주소**를 확인하고
  - 자신이 가진 **MAC Address Table**과 비교해 맞는 정보가 있으면 **match되는 해당 port로 packet을 forwarding**한다
    - 이때, 다른 port로는 해당 packet을 보내지 않으므로 이 동작을 `filtering`이라고 한다
- Switch는 `fowarding`과 `filtering`을 통해 **목적지로만 packet이 전달되도록 동작**한다
- Switch에서는 `forwarding`과 `filtering` 작업이 **여러 port에서 동시에 수행**될 수 있다
  - 통신이 다른 port에 영향을 미치지 않으므로, 다른 port에서 기존 통신 작업으로부터 **독립적으로 동작**할 수 있다

- Switch는 **일반적인 Unicast**에 대해서만 `forwarding`과 `filtering` 작업을 수행한다
  - **BUM Traffic**이라고 부르는 Broadcast, Unknown Unicast, Multicast는 조금 다르게 동작한다
    - 출발지 MAC 주소로 broadcast나 multicast 모두 출발지가 사용되지 않으므로, 해당 traffic은 전달이나 filtering 작업을 하지 않고 **모두 flooding**한다
    - Unkonw Unicast도 **MAC Table에 없는 주소**이므로 broadcast와 동일하게 flooding 한다

<br>.

#### LAN에서의 ARP - Switch 동작

- `Ethernet - TCP/IP` network에서는 switch가 unicast를 flooding하는 경우가 거의 없다
  - Packet을 만들기 전에 통신해야 하는 단말의 MAC 주소를 알아내기 위해 `ARP Broadcast`가 먼저 수행되어야 하므로 Unicast보다 ARP Broadcast가 먼저 network에 전달된다
    - 이 ARP를 이용한 MAC 주소 습득 과정에서 이미 switch는 통신하는 출발지와 목적지의 MAC 주소를 **습득**할 수 있고, 실제 unicast 통신이 시작되면 이미 만들어진 MAC Address Table로 packet을 `forwarding`, `filtering`한다
- ARP와 MAC Table은 일정 시간 동안 지워지지 않는데, 이 시간을 **aging time**이라고 한다
  - 일반적으로 MAC Table의 aging time이 단말의 ARP aging time보다 길어서 Ethernet network를 flooding없이 효율적으로 운영할 수 있다
