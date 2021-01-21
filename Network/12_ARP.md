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