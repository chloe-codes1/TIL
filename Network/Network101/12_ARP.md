# ARP (Address Resolution Protocol)

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

- OSI 7 Layers 중 2, 3계층이 **주소**를 가지고 있고 통신할 때 **목적지를 찾아갈 수 있도록** 하지만 2게층 `MAX 주소`와  3계층 `IP 주소`간에는 아무 관계도 없다
  - 2계층 `MAC 주소`는 hardware 생산업체가 임의적으로 할당한 주소이고,
  - 3계층 `IP 주소`는 **직접 할당**하거나 **DHCP**를 이용해 **자동으로 할당**받는다
- 실제 통신은 `IP 주소` 기반으로 일어나고 `MAC 주소`는 **상대방의 주소**를 자동으로 알아내서 통신하게 된다
  - 이때 상대방의 MAC 주소를 알아내기 위해 사용되는 protocol이 **ARP (Address Resolution Protocol)**이다

<br>

## 1. ARP란?

- Data 통신을 위해 2계층 물리적 주소인 `MAC 주소`와 3계층 논리적 주소인 `IP 주소` 두 개가 사용된다
  - IP 주소 체계는 물리적 MAC 주소와 전혀 연관성이 없으므로 **두 개의 주소를 연개**시켜 주기 위한 **mechanism** 이 필요하다
    - 이때 사용되는 protocol이 **ARP** 이다
- `ARP protocol`은 TCP/IP protocol을 위해서만 동작하는 것은 아니다
  - TCP-Ethernet protocol과 같이 3계층의 **논리적 주소**와 2층 **물리적 주소** 사이에 **관계가 없는 protocol**에서 ARP protocol과 같은 mechanism을 사용해 물리적 주소와 논리적 주소를 **연결**한다
- Host에서 아무 통신이 없다가 **처음 통신을 시도**하면 packet을 바로 `캡슐화 (Encapsulation)` 할 수 없다
  - 통신을 시도할 때 출발지와 목적지의 IP주소는 알고 있어 캡슐화하는데 문제는 없지만, **상대방의 MAC 주소를 알 수 없어** 2계층 캡슐화를 수행할 수 없다
    - 상대방의 주소를 알아내려면 `ARP Broadcast`를 이용해 network 전체에 **상대방의 MAC주소를 질의**해야한다
- `ARP Broadcast`를 받은 목적지는 `ARP protocol`을 이용해 **자신의 MAC주소**를 **응답**한다
  - 이 작업이 완료되면 출발지, 목적지 모두 **상대방에 대한 MAC주소**를 **학습** 하고,
  - 이후 packet이 정상적으로 encapsulation되어 상대방에게 전달될 수 있다
- `Packet Network`에서는 **큰 데이터**를 **잘라 전송**하므로 **여러 개의 packet**을 전송해야 한다
  - Packet을 보낼 때마다 `ARP Broadcast`를 수행하면 network 통신의 **효율성**이 크게 **저하**되므로 **memory에 정보를 저장**해두고 **재사용**한다
    - 성능 유지를 위해서는 `ARP Table`을 오래 유지하는 것이 좋지만, 논리 주소(IP)는 언제든 바뀔 수 있으므로 **일정 시간 동안 통신이 없으면** 이 table은 **삭제**된다

<br>

<br>

## 2. ARP 동작

- ARP Packet은 여러 가지 field 중 ARP data에 사용되는 아래의 4개 field가 중요하게 사용된다
  1. 송신자 hardware MAC 주소
  2. 송신자 IP Protocol 주소
  3. 대상자 MAC 주소
  4. 대상자 IP Protocol 주소
- ARP는 위의 4개의 field를 이용해 아래와 같이 동작한다
  - ex) Server A (`1.1.1.1`)  -------- Server B (`1.1.1.2`)
    - Server A에서 server B로 ping을 보내려고 할 때, server A에서는 3계층의 IP주소까지 캡슐화 할 수 있지만, 목적지 MAC 주소를 모르기 때문에 정상적으로 packet을 만들 수 없다
    - Server A는 목적지 server B의 MAC 주소를 알아내기 위해 ARP 요청을 network에 **broadcast**한다
      - ARP packet을 network에 broadcast할 때 2계층 MAC 주소는 출발지를 자신의 MAC 주소로, 도착지는 broadcast (FF-FF-FF-FF-FF-FF)로 채우고,
      - ARP protocol field의 전송자 MAC과 IP에는 자신의 주소로, 대상자 IP 주소는 `10.1.1.2`, 대상자 MAC 주소는 `00-00-00-00-00-00`으로 채워 network에 뿌린다
    - 2계층 목적지 주소가 broadcast 주소이므로 이 ARP packet은 **같은 network** 안에 있는 **모든 단말**에 보내지고 모든 단말은 ARP protocol 내용을 확인한다
      - 확인해서 ARP protocol의 대상자 IP가 자신이 맞는지 확인해 **자신이 아니면** ARP packet을 **버린다**
    - Server B에서는 ARP 요청의 대상자 IP 주소가 자신의 IP이므로 **ARP 요청을 처리**하고 그에 대한 **응답**을 보낸다
      - 이때는 송신자와 대상자의 위치가 바뀐다
    - ARP 요청을 처음 보냈던 server A와 달리 server B에서는 ARP 요청을 수신하면서 이미 ARP 요청을 보낸 sever A의 IP 주소와 MAC 주소를 알고 있어 **모든 ARP field를 채워 응답** 할 수 있다
      - ARP 요청에서 받은 server A의 정보를 이용해 대상자 MAC, IP 주소를 채우고 자신의 MAC, IP 주소를 송신자 MAC, IP 주소로 채워 응답한다
        - ARP **요청**을 처음 보낼 때는 **broadcast**인 반면, (2계층 목적지 MAC 주소가 broadcast이므로)
        - ARP **응답**을 보낼 때는 출발지와 도착지 MAC 주소가 명시되어 있는 **unicast**이다
    - Server A는 server B부터 ARP 응답을 받아 자신의 **ARP cache table**을 **갱신**한다
      - 이 ARP cache table은 정해진 시간동안 **server B와의 통신이 없을 때**까지 유지된다
        - 해당 시간 안에 통신이 다시 이루어지면 그 시간은 다시 **초기화**된다
    - ARP cache table이 **갱신**된 후에는 **상대방의 MAC 주소**를 알고 있으므로 도착지 MAC 주소 field를 완성해 **ping packet**을 보낼 수 있다

<br>

<br>

## 3. GARP

- 일반적인 ARP 외에도 ARP protocol field를 그대로 사용하지만 **내용을 변경**해 **원래 ARP protocol의 목적과 다른 용도로 사용**하는 `GARP`. `RARP`와 같은 protocol 이 있다
- `GARP`는 Gratuitous ARP의 약자로, **대상자 IP field**에 **자신의 IP 주소**를 채워 ARP 요청을 보낸다
  - ARP가 상대방의 MAC 주소를 알아내기 위해 사용되는 반면, `GARP`는 **자신의 IP와 MAC 주소를 알릴 목적**으로 사용된다
    - 그렇기 때문에 GARP의 목적지 MAC 주소 (2계층 destination MAC)는 **broadcast MAC 주소**를 사용한다
- `GARP`의 packet을 살펴보면
  - 송신자 MAC (Sender MAC)은 자신의 MAC 주소,
  - 송신자 IP (Sender IP) 주소는 자신의 IP주소,
  - 대상자 MAC (Target MAC) 주소는 모두 **0**으로 표기해 `00:00:00:00:00:00`,
  - 대상자 IP (Target IP)  주소도 자신의 IP 주소로 넣어 network에 **broadcast** 한다

<br>

### 3-1. 다른 ARP 요청 vs GARP

- 같은점
  - 대상자 MAC 주소가 `00:00:00:00:00:00` 으로 채워진 것이고
- 다른점
  - 송신자와 대상자 IP 주소가 자신으로 동일하다

<br>

### 3-2. GARP를 사용해 동일 Network에 자신의 IP 주소와 MAC 주소를 알려주는 이유

#### 1. IP 주소 충돌 감지

- IP 주소는 유일하게 할당되어야 하는 값이지만 여러가지 이유로 내가 할당받은 IP를 다른 사람이 쓰고있을 수 있다
  - IP 충돌 때문에 통신이 안 되는 것을 예방하기 위해 자신에게 할당된 IP가 network에서 이미 사용되고 있는지 `GARP`를 통해 확인한다
- 단말이 network에 연결되면 `GARP`를 통해 현재 설정된 IP 주소를 **network에서 사용되고 있는지 확인**할 수 있다
  - 만약 `GARP`에 대한 응답이 오면 network 상에서 해당 IP를 이미 사용 중인 단말이 있다는 것을 알 수 있다

#### 2. 상대방 (동일 subnet 상의 다른 상대방)의 ARP Table 갱신

- `가상 MAC 주소`를 사용하지 않는 **database HA (High Availability)** solution에서 주로 사용한다
  - **Database HA**는 주로 두 database server가 하나의 가상 IP 주소로 서비스한다
    - 두 대의 database중 하나만 동작하고, 나머지 한 대는 대기하는 `Active-Standby`로 동작한다
    - `Active` 상태인 server가 **가상 IP 주소** 요청에 응답해 서비스하지만 MAC 주소는 가상 주소가 아닌 **실제 MAC 주소**를 사용한다
  - 만약 요청에 응답하던 `master 장비` A가 동작하지 않을 경우, 대기하던 장비 B가 `active`로 동작해 가상 IP 주소에 대한 `ARP 요청`에 응답한다
    - `Active`로 새로 변경된 장비 B와 처음 통신하는 단말은 변경된 active의 MAC 주소를 학습해 통신이 가능하지만,
    - 기존 master 장비 A를 `active`   로 인식하고 통신하던 단말은 A의 MAC 주소가 **ARP Cache Table**에 남아 있어 단말이 계속 A로 packet을 보낸다
    - 이렇게 기존 정보가 남아 있는 단말이 보낸 packet은 정상적으로 동작하지 않아 network에서 응답이 불가능하거나, `Standby` 상태인 A쪽으로 packet이 보내지므로 정상적인 service를 받을 수 없게 된다
      - 이런 형상을 예방하기 위해 `Standby` 장비가 `Active` 상태가 되면 **GARP Packet**을 network에 보내 active 장비가 **변경** 되었음을  알려준다
        - 이후 local network 단말들의 **ARP table**에는 해당 가상 IP 주소가 MAC주소로 갱신되어 통신된다
- 최근 network 장비에서는 위와같은 형태의 HA는 잘 쓰이지 않는다
  - **GARP**를 이용해 **packet을 가로채는** 기법이 많이 사용되어 **보안상의 이유**로 GARP를 받더라도 ARP table을 갱신하지 않는 단말들이 존재할 가능성이 있어 이런 문제가 발생하지 않는 `가상 MAC`을 사용하는 `HA solution`이 사용된다

#### 3. HA (High Availability) 용도의 Clustering, `VRRP (Virtual Router Redundancy Protocol)`, `HSRP (Hot Standby Router Protocol)`

- 앞에 2번의 HA solution의 경우 **장비 이중화**를 위해 사용되지만, **실제 MAC 주소를 사용하지 않고 가상 MAC을 사용하는** `Clustering`, `VRRP`, `HSRP`와 같은 **FHRP (First Hop Redundancy Protocol)**에서도 GARP가 사용된다
  - Database HA solution에서 GARP 사용 목적이 **ARP Table 갱신**이었던 반면,
  - `Clustering` 이나 FHRP의 사용은 Network에 있는 **switch 장비의 MAC Table 갱신**이 목적이다
    - `Clustering`에서 가상 MAC 주소를 사용하는 경우, 단말은 ARP 정보를 가상 MAC 주소로 학습하므로 **단말의 ARP Table을 갱신할 필요가 없다**
    - but, `Clustering` 중간에 있는 **switch의 MAC Table**은 master가 변경되었을 때 **가상 MAC 주소의 위치**를 적절히 찾아가도록 **update**해야 하므로 **master가 변경되는 시점에 MAC Table의 갱신**이 필요하다
  - 따라서 Slave가 master로 역할이 변경되면 `GARP`를 전송하고 switch에서는 이 GARP를 통해 MAC 주소에 대한 port 정보를 새로 변경해 MAC table을 갱신한다

<br>

<br>

## 4. RARP

- Reverse ARP의 줄임말로 말그대로 반대로 동작하는 ARP이다
  - `GARP`처럼 ARP Protocol 구조는 같지만,
    - filed에 들어가는 내용이 다르고
    - 원래 목적과 반대로 사용된다
  - **ARP vs RARP**
    - `ARP`
      - IP 주소 -> `ARP` -> MAC 주소
    - `RARP`
      - MAC 주소 -> `RARP` -> IP 주소
- `RARP`는 **IP 주소가 정해져 있지 않은 단말**이 **IP 할당을 요청**할 때 사용한다
  - `ARP` 는 내가 통신해야 할 상대방의 MAC 주소를 모를 때 상대방의 IP 주소로  MAC 주소를 물어볼 목적으로 만들어진 protocol 이다
  - 반대로 `RARP`는 나 자신의 MAC 주소는 알지만 IP가 아직 할당되지 않아 **IP를 할당해주는 server**에 **어떤 IP 주소를 써야 하는지** 물어볼 때 사용된다
- RARP는 과거에 network host 주소 할당에 사용되었지만 제한된 기능으로 인해 `BOOTP`와 `DHCP`로 대체되어 사용되지 않는다
