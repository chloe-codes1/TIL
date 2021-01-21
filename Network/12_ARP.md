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