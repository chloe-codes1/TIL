# Network Address Types

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

Network에서 출발지에서 목적지로 data를 전송할 때 사용하는 **통신 방식**에는 `유니캐스트 (Unicast)`, `브로드캐스트 (Broadcast)`, `멀티캐스트 (Multicast)`, `애니캐스트 (Anycast)`가 있다

<br>

### 1. Unicast

- 출발지와 목적지가 **명확히 하나**로 정해져 있는 **1:1** 통신 방식이다
- 실제로 사용하는 **대부분의 통신**은 `Unicast` 방식을 사용한다

<br>

### 2. Broadcast

- 목적지 주소가 **모든**으로 표기되어 있는 **1:모든** 통신 방식이다
- `Unicast`로 통신하기 전, 주로 상대방의 **정확한 위치**를 알기 위해 사용된다
- 주소 체계에 따라 `Broadcast`를 다양하게 분류할 수 있지만 기본 동작은 **Local network 내**에서 **모든 host로 packet을 전달**해야 할 때 사용된다

<br>

### 3. Multicast

- **Multicast group address**를 이용해 **해당 group에 속한 다수의 host**로 packet을 전송하기 위한 **1:그룹**  통신 방식이다
  - 여기서 group은 multicast 구독 host group을 뜻한다
- IPTV와 같은 실시간 방송을 볼 때 `multicast` 통신 방식을 사용한다
- 사내 방송이나 증권 시세 전송과 같이 **단방향**으로 **다수**에게 **동시에 같은 내용**을 전달해야 할 때 사용된다

<br>

### 4. Anycast

- Anycast **주소가 같은 host** 중에서 **가장 가깝거나 가장 효율적**으로 서비스할 수 있는 host와 통신하는 방식이다
  - 목적지가 동일 group내의 1개 host인 **1:1** 통신 방식이다
- `Anycast`의 **gateway** 성질을 이용해서 **가장 가까운 DNS server를 찾을 때** 사용하거나 **가장 가까운 gateway**를 찾는 `anycast gateway` 기능에 사용하기도 한다
- **최종 통신**은 1:1로 `unicast`와 `anycast`가 동일하지만 **통신할 수 있는 후보자**는 서로 다르다
  - `unicast`는 출발지와 목적지가 모두 한 대씩 이지만,
  - `anycasst`는 **같은 목적지 주소**를 가진 서버가 여러 대여서 **통신 가능한 다수의 후보군**이 있다

<br>

### 통신 방식 정리

| Type          | 통신 대상 | 범위                   | IPv4 | IPv6 | 예제 |
| ------------- | --------- | ---------------------- | ---- | ---- | ---- |
| **Unicast**   | 1 : 1     | 전체 network           | O    | O    | HTTP |
| **Broadcast** | 1 : 모든  | subnet (local network) | O    | X    | ARP  |
| **Multicast** | 1 : 그룹  | 정의된 구간            | O    | O    | 방송 |
| **Anycast**   | 1 : 1     | 전체 network           | △    | O    | DNS  |

- 현재 주로 사용되는 network 주소 체계는 **IPv4 기반**이다
  - 일부 mobile network와 대규모 data center 위주로 새로운 **IPv6** 기반 주소 체계가 사용되고 있다
  - **IPv6**에서는 `Broadcast`가 존재하지 않고 **link local multicast**로 대체되어 사용된다
- 통신 방식을 구분할 때 중요한 것은 실제 데이터를 전달하려는 출발지가 기준이 아니라 **목적지 주소를 기준으로 구분**된다는 것이다

<br>

<br>

`+`

### BUM Traffic

- BUM Traffic의 BUM은 **B (Broadcast)**, **U (Unknown Unicast)**, **M (Multicast)**를 지칭한다
  - B, U, M은 서로 다른 종류의 traffic이지만 **network에서의 동작은 서로 비슷**하다
- `Unknown Unicast`는 unicast여서 **목적지 주소는 명확히 명시**되어 있지만 **network에서의 동작**은 `Broadcast`와 같을 때를 가리킨다
  - `Switch`가 **목적지에 대한 주소**를 학습하지 못한 상황 (switch 입장에서 unknown)이어서 packet을 모든 port로 **flooding** 하는 unicast를 `unknown unicast`라고 한다
- BUM Traffic이 중요한 이유는 `unicast`이지만 실제 겉으로 보이는 동작 방식은 `broadcast` 에 가깝기 때문이다
  - 물론 `unicast`이므로 전달 받는 **모든 단말 NIC (Network Interface Card)**에서 **도착지 주소를 확인**하고 자신이 목적지가 아니므로 **packet을 버린다**
  - 하지만 network입장에서는 **network 자원을 쓸데없이 사용**하므로 network 상에서 **불필요한 BUM Traffic**이 많아지면 network의 **성은ㅇ이 저하** 될 수 있다!
- `Ethernet` 환경에서는 **ARP Broadcast**를 먼저 보내고 이후 통신을 시작하므로 BUM Traffic이 많이 발생하지 않는다
