# Types of Computer Network

> LAN, MAN, WAN에 대해 알아 보아요

<br><br>

Network는 **규모**와 **관리 범위**에 따라 `LAN`, `MAN`, `WAN` 3가지로 구분된다

- **LAN (Local Area Network)**
  - 사용자 내부 network
- **MAN (Metro Area Network)**
  - 한 도시 정도를 연결하고 관리하는 network
- **WAN (Wide Area Network)**
  - 멀리 떨어진 LAN을 연결해주는 network

<br>

예전에는 LAN, MAN, WAN에서 사용하는 기술이 모두 달라 사용하는 **protocol**이나 **전송 기술**에 따라 쉽게 구분할 수 있었다

But, 현재는 대부분이 **Ethernet**으로 통합되면서 사용자가 전송 기술을 구분하는 것은 무의미해져서 **관리 범위 기준**으로 LAN, MAN, WAN을 구분한다

<br>

<br>

### LAN (Local Area Network)

- home network와 사무실용 network 처럼 비교적 **소규모**의 network를 말한다
- 먼 거리를 통신할 필요가 없어 **switch**와 같이 비교적 간단한 장비로 연결된 network를 LAN이라고 불러왔다
- 소모 비용, 신뢰도, 구축 및 관리를 위해 다양한 기술이 사용되지만,
  - 현재는 대부분 **Ethernet** 기반 전송 기술을 사용한다
- 전송 기술에 대한 구분 외에 **관리 범위**에서의 LAN은 자신이 소유한 건물이나 대지에 **직접 구축한 선로**로 동작시키는 network로 정의할 수 있다
  - 과거에는 대규모 공장이나 대학과 같은 광범위한 network를 별도로 구분했지만, 최근에는 이런 구분도 무의미해졌다.

<br>

<br>

### WAN (Wide Area Network)

- **먼 거리**에 있는 network를 연결하기 위해 사용한다
- 멀리 떨어진 **LAN을 서로 연결**하거나 **internet에 접속하기 위한 network**가 WAN에 해당한다
- WAN은 특별한 경우가 아니면 직접 구축할 수 없는 범위의 network이므로 대부분 `통신사업자`로 부터 회선을 임대해 사용한다
  - 원격지 연결을 위해 `통신사업자`로부터 빌려 쓰는 network이다
    - 자신이 소유한 땅이나 건물이 아닌 곳을 지나 원격지로 통신해야 할 때 사용하며 **사용계약**에 의해 비용이 부과된다

<br><br>

### MAN (Metro Area Network)

- 수~수십 Km 범위의 한 도시를 network로 연결하는 개념이다
- 일반적으로 도시 단위의 network를 구분할 때는
  - **통신사가 이미 갖고 있는 infra 기반**으로 network를 구축하면 **WAN**,
  - **자체 infra**를 통해 network를 구축하면 **MAN**으로 구분하기도 한다
