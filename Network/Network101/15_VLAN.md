# VLAN

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

## 1. What is VLAN?

- 물리적 배치와 상관없이 LAN을 **논리적으로 분할, 구성**하는 기술
  - 한 대의 `Switch`를 여러개의 `VLAN`으로 분할할 수 있다
    - 별도의 switch 처럼 동작한다
- 기업에서의 부서별 네트워크 분할 및 스마트폰, PC 등 다수의 단말이 네트워크에 연결됨에 따라 **네트워크 분할**이 중요하다
  - **네트워크 분할이 필요한 이유**
    1. **과도한 broadcast**로 인한 단말들의 **성능 저하**
    2. 보안 향상을 위한 차단 용도
    3. 서비스 성격에 따른 정책 적용
- `VLAN`을 나누면 하나의 장비를 **서로 다른 network를 갖도록 논리적으로 분할**한 것이므로 `Unicast` 뿐만 아니라 `Broadcast` 도 **VLAN 간에 통신할 수 없다**
  - 만약 `VLAN` 간의 통신이 필요하다면, 서로 다른 network 간의 통신이므로 3계층 장비의 도움이 필요하다
- `VLAN`을 사용하면 **물리적 구성과 상관없이** network를 분리할 수 있고, 물리적으로 다른 층에 있는 단말이 하나의 `VLAN`을 사용해 **동일한 network로 묶을 수 있다**
  - 분리된 단말 간에는 `3계층 장비`를 통해 통신하게 된다

<br>

<br>

## 2. Types of VLANS

`VLAN`  할당 방식에는 **port 기반**의 VLAN과 **MAC 주소 기반**의 VLAN이 있다

<br>

### Port Based VLAN

- VLAN이 처음 도입되었을 때는 switch가 고가였고 여러 hub를 묶는 역할을 switch가 담당했으므로 switch를 분할해 여러 network에 사용하는 것이 VLAN 기능을 적용하는 목적이었다
  - 이렇게 switch의 위치를 **논리적으로 분할**해 사용하는 것이 목적인 VLAN을 `Port Based VLAN`  이라고 부른다
    - 우리가 일반적으로 언급하는 대부분의 VLAN은 `Port Based VLAN`이다
  - 어떤 단말이 접속하든지 **switch의 특정 port**에 **VLAN을 할당**하면 할당된 VLAN에 속하게 된다

- `Port Based VLAN`으로 설정된 switch에서 **VLAN 설정 기준은 Switch의 port** 이다
  - ex)
    - AA PC가 1번 port에 연결되면 VLAN 10에 속하고, 4번 port에 연결되면 VLAN 20에 속한다

<br>

### Mac Based VLAN

- 사용자들의 자리 이동이 많아지면서 **MAC Address**를 기반으로 한 `Mac Based VLAN`이 개발되었다
  - `Mac Based VLAN`을 사용하면 유선 사용자가 이동하더라도 같은 VLAN에 할당된다
- **Switch의 고정 port**에 VLAN을 할당하는 것이 아니라 switch에 연결되는 **단말의 MAC Address**를 기반으로 VLAN을 할당하는 기술이다
- 단말이 연결되면, 단말의 MAC Address를 인식한 switch가 해당 port를 지정된 VLAN으로 변경한다
  - 단말에 따라 VLAN 정보가 바뀔 수 있어 `Dynamic VLAN`이라고도 부른다

- `Mac Based VLAN`의 **VLAN 할당 기준**은 **PC의 MAC주소**이다
  - ex)
    - AA PC는 **어떤 switch의 어떤 port**에 접속하더라도 **동일한 VLAN**이 할당된다

<br>

<br>

## 3. How VLAN Works (Trunk/Access)

- `Port Based VPN` 에서는 **Switch의 각 port**에 각각 사용할 **VLAN을 설정**하는데, 한 대의 switch에 연결되더라도 **서로 다른 VLAN이 설정된 prot 간**에는 **통신할 수 없다**
  - `VLAN`이 다르면 **별도의 분리된 switch에 연결된 것**과 같으므로 VLAN 간 통신이 불가능하다
    - 서로 다른 VLAN 간 통신을 위해서는 `router`와 같은 3계층 장비를 사용해야 한다
      - `VLAN`으로 구분된 network에서는 `broadcast`인 **ARP Request**가 다른 VLAN으로 전달될 수 없으므로 3계층 장비를 이용해 통신해야 한다
- Switch port에 **VLAN을 설정하여 network를 분리**하면 물리적으로 switch를 분리할 때보다 **효율적**으로 장비를 사용할 수 있다
  - VLAN 분리는 **다수의 논리적인 switch**를 만드는 효과가 있다
- 여러 개의 VLAN이 존재하는 상황에서 switch를 서로 연결해야 하는 경우에는 각 VLAN 끼리 통신하려면 **VLAN 개수만큼 port를 연결**해야 한다
  - VLAN이 분할된 switch는 **물리적인 별도의 switch로 취급**된다
  - ex)
    - Switch 하나에 3개의 VLAN이 구성되어 있는 경우, **각 VLAN이 switch 간에 통신**하려면 3개의 port가 필요하다
      - VLAN을 더 많이 사용하는 중/대형 network에서 이렇게 VLAN별로 port를 연결하면 **장비 간의 연결**만으로도 **많은 port가 낭비**된다
  - 이 문제를 해결하기 위해 `VLAN Tag 기능`이 등장했다!

<br>

### Tagged Port (Trunk Port)

- Tag 기능은 **하나의 port에 여러 개의 VLAN을 함께 전송할 수 있게** 해준다
  - 이 port를 `Tagged port` 또는 `Trunk port`라고 한다
- 여러 개의 VLAN을 동시에 전송해야 하는 `Tagged port`는 통신할 때 **Ethernet Frame** 중간에 **VLAN Field**를 끼워 넣어 이 정보를 이용한다
  - `Tagged Port` 로 packet을 보낼 때는 **VLAN ID**를 **붙이고**, 수신측에서는 이 **VLAN ID**를 **제거**하면서 해당 VLAN ID의 VLAN으로 packet을 보낼 수 있게 된다
- `Tagged Port`를 사용하면 VLAN마다 통신하기 위해 필요했던 여러 개의 port를 하나로 묶어 사용할 수 있으므로 **port 낭비 없이** network를 유연하게 design 할 수 있다
- `Tagged Port` 기능이 switch에 생기면서 switch의 packet 전송에 사용하는 **MAC Address Table**에도 변화가 생겼다
  - 다른 VLAN끼리 통신하지 못하도록 **Mac Address Table**에 **VLAN을 지정하는 field**가 추가된 것이다!
    - 즉, 하나의 switch에서 VLAN을 이용해 network를 분리하면 **VLAN 별로 Mac Address Table이 존재하는 것 처럼** 동작한다

- `Tagged Port`는 여러 개의 VLAN, 즉 **여러 network**를 **하나의 물리적 port**로 전달하는 데 사용된다
- `Tagged Port`는 일반적으로 **여러 network가 동시에 설정**된 switch 간의 연결에서 사용된다
- `Tagged Port`로 packet이 들어올 경우 **Tag를 벗겨내면서 Tag된 VLAN 쪽으로 packet을 전송**한다

<br>

### Untagged Port (Access Port)

- 일반적인 port를 `Untagged Port` 또는 `Access Port` 라고 한다
- `Untagged Port` **하나의 VLAN**에 속한 경우에만 사용된다
  - 그래서 일반적으로 하나의 network에 속한 server의 경우 `Untagged`로 설정한다

- `Untagged Port`로 packet이 들어올 경우, 같은 VLAN으로만 packet을 전송한다

<br>

<br>

### 가상화 Server

- Switch 간의 연결이 아닌 sever와 연결된 port도 **가상화 server**가 연결될 때는 **여러 VLAN과 통신**해야 할 수도 있다
  - 이 경우 server와 연결된 port더라도 `Untagged`가 아닌 `Tagged`로 설정한다
    - Tagged 상태이므로 가상화 server쪽 interface에서도 tagged 상태로 설정해야 한다
  - 가상화 server 내부에 **가상 switch**가 존재하므로 **switch간 연결**로 보면 더 이해하기 쉽다

<br>

<br>

### VLAN 간 통신

- VLAN은 switch 통신을 분할하는 기능 때문에 `unicast`, `multicast`, `broadcast`모두 VLAN을 넘어가지 못한다
- 일반적으로 VLAN이 다르다는 것은 **별도의 network로 분할**한 것이기 때문에 **network가 다르고**, **IP 주소 할당도 다른 network로 할당**되는 것이 일반적이다
  - 다른 network 간의 통신이 필요하다면 `router`와 같은 **3계층 장비**의 도움이 필요하다  
