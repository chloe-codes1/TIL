# VPC

> VPC 자세-히 알아보기 실무 ver.

<br>

<br>

### VPC란?

- 네트워크를 추상화해서 설명하기위해 AWS는 Virtual Private Cloud를 도입했다
- 한 계정에는 여러개의 VPC를 만들 수 있다!

<br>

<br>

### Default VPC

- 계정을 만들면 한 region에 **default VPC**가 한 개 만들어진다
  - Default VPC 에는 IPv4 CIDR   `172.31.0.0/16` 가 할당된다
  - Default VPC 내 default subnet에는 VPC CIDR 범위 내 `/20` 네트 블록이 할당된다
- 만약 default VPC에 그대로 Infra를 구성하는 경우
  - Infra를 구성하는 사람이 **해당 Network 대역을 사용해도 되느냐**가 문제이다
    - 만약 회사 규모가 클 경우, 지점/지사 별로 network  대역이 다를 것이다
      - 즉, 어디까지는 연결 될 수 있고, 어디는 연결될 수 없다는 문제점을 가진다
        - 그래서 서로 침범하는 것이 있진 않을지 확인하기 위해 각 Netwrok 대역 폭을 알고 있어야 하는 불편함이 있다

<br>

<br>

### CIDR Block을 잘 설계하기

- AWS VPC Network 대역에서 할당할 수 있는 IP 주소의 범위는 원래 `Network address`, `Broadcat address`  두 가지가 빠지는 것보다 많다
  - 총 5개가 빠진다
    - `Network address`
    - `Broadcast addrss`
    - `Reserved by AWS for VPC router`
    - `Reserved by AWS`
    - `Reserved by AWS for future use`
- LB도 우리가 갖고있는 VPC IP를 가져가므로 이것도 고려해야 한다
  - ALB, NLB, CLB 모두 redundant, HA 구성을 위해 각각 최소 2개 혹은 Traffic이 많으면 더 많이 가져간다

<br>

#### Public Cloud 환경에서의 CIDR 설정

- CIDR은 16으로 설정하자
  - 협소하게 생각하지 말자
    - 나중에 확장 공사하게 될 수도 있다
    - Cloud에서는 16bit가 적절하다!

<br>

<br>

#### Private IPv4 addresses

| RFC1918 name |       IP address range        | Number of addresses | Largest [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) block (subnet mask) | Host ID size | Mask bits | *[Classful](https://en.wikipedia.org/wiki/Classful_network)* description[[Note 1\]](https://en.wikipedia.org/wiki/Private_network#cite_note-4) |
| :----------: | :---------------------------: | :-----------------: | :----------------------------------------------------------: | :----------: | :-------: | :----------------------------------------------------------: |
| 24-bit block |   10.0.0.0 – 10.255.255.255   |      16777216       |                    10.0.0.0/8 (255.0.0.0)                    |   24 bits    |  8 bits   |                  **single class A network**                  |
| 20-bit block |  172.16.0.0 – 172.31.255.255  |       1048576       |                 172.16.0.0/12 (255.240.0.0)                  |   20 bits    |  12 bits  |              **16 contiguous class B networks**              |
| 16-bit block | 192.168.0.0 – 192.168.255.255 |        65536        |                 192.168.0.0/16 (255.255.0.0)                 |   16 bits    |  16 bits  |             **256 contiguous class C networks**              |

- AWS는 어느 Private IP 대역을 써도 상관 없다
- AWS 관리망이랑 충돌나지 않는다 (AWS 의 가상망 기술)

<br>

<br>

### DNS hostnames와 DNS resolution을 Enable 해야하는 이유

![dns](../../images/dns.png)

- `DNS hostnames`

  - enable 되어 있으면 AWS domain을 통해 **DNS lookup**이 가능하다

- `DNS resolution`

  - Disable 하면

    - EKS 연결시 문제가 발생할 수 있다
    - Route 53으로 alias 연결이 불가능하다
