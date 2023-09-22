# Getting Started with Amazon VPC

> VPC 파헤치기!
>
> References: [Amazon VPC docs](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html), [44bits.io](https://www.44bits.io/ko/post/understanding_aws_vpc)

<br>

## What is Amazon VPC?

> 사용자가 정의한 가상 네트워크 (Virtual Private Cloud)

- VPC는 기존 서버 호스팅과 차별화된 중요한 특징들이 있다
  - VPC를 사용하면 네트워크 환경을 **직접 설계**할 수 있다
- VPC에서 IPv4와 IPv6를 모두 사용하여 리소스와 애플리케이션에 안전하고 쉽게 액세스할 수 있다

- VPC는 **논리적으로 격리된 공간을 프로비저닝** 한다
  - 하나의 계정에서 생성하는 리소스들만의 격리된 네트워크를 만들어주는 기능이 VPC!!
    - VPC를 사용하면 특정 사용자의 리소스들이 논리적으로 격리된 네트워크에서 생성되기 때문에 다른 사람들은 접근하는 것은 물론 보는 것도 불가능하다!
  - EC2-클래식 네트워크 환경은 다른 사용자들과 함께 사용하는 공용 공간
    - 과거에는 EC2-클래식과 EC2-VPC 네트워크 환경을 선택해서 사용할 수 있었음!! (그랬군..)
    - 현재 AWS에서는 AWS 계정을 생성할 때 리전 별로 **기본 VPC**를 함께 생성
      - 기본 VPC를 사용하면 아마존 VPC를 크게 의식하지 않더라도 EC2-클래식 네트워크를 사용하듯이 쉽게 AWS에서 제공하는 서비스들을 이용할 수 있음
      - 기본 VPC를 사용하더라도 EC2-클래식과 달리 격리된 네트워크 환경의 장점을 누릴 수 있다!

<br>

<br>

## VPC의 구성 요소들

<br>

### 1. VPC

- 프라이빗 클라우드를 만드는 데 가장 기본이 되는 리소스

- 논리적인 독립 네트워크를 구성하는 리소스

  - 이름과 IPv4 CIDR 블록을 필수적으로 가짐
    - **CIDR (Classless Inter-Domain Routing) 블록**
      - IP의 범위를 지정하는 방식
      - 구성
        - IP  주소
        - `/` 뒤에 오는 넷마스크 숫자
          - IP 범위를 나타냄
            - 이 숫자가 32이면 앞에 기술된 IP 정확히 하나를 가리킴
            - ex) `192.168.0.0/32`는 `192.168.0.0`을 가리킴
            - 범위는 지정된 IP부터 `2^(32-n)`개
              - ex) 뒤의 숫자가 24라면, `2^(32-24)=256`개의 IP 주소
              - ex)  `192.168.0.0/24`는 `192.168.0.0`에서 `192.168.1.255`까지의 IP

- 클라우드에서 생성하는 자원들은 기본적으로 특정 네트워크 위에서 생성되며 이에 접근하기 위한 프라이빗 IP를 가짐

  - 이 리소스들은 특정한 VPC 위에서 만들어진다!
    - VPC의 CIDR 범위 안에서 적절한 IP를 할당 받게 됨
    - ex)  `192.168.0.0/24` CIDR 블록을 가진 VPC에서 생성한 EC2 인스턴스는 `192.168.0.127`이라는 IP를 할당 받을 수 있음
  - VPC의 범위 내에서 할당 가능한 IP가 모두 할당되면 더 이상 리소스를 만들 수 없음
    - 적절한 크기의 VPC를 만들어야함!!
      - VPC의 최대 크기는 16 (`넷마스크`)
        - 2^(32-16)=65536 개의 IP 사용 가능

- VPC를 만들 때 또 하나 고려해야할 점!

  - CIDR의 범위를 지정하는데 특별한 제약은 없지만, 인터넷과 연결되어 있는 경우 문제가 발생할 수 있음

    - ex)  이건 그냥 참고만!

      > 예를 들어 `52.12.0.0/16`을 CIDR 블록으로 지정한 경우를 생각해보겠습니다. 이 VPC에서 `52.12.0.0/16`로 접속하는 트래픽은 VPC 내부로 라우트 됩니다. 그런데 이 범위의 IP는 인터넷에서 사용할 수 있는 IP입니다. 따라서 이 VPC에서는 `52.12.0.0/16`에 속한 인터넷 IP에 접근하는 것이 원천적으로 불가능합니다. 인터넷 연결이 필요한 경우 반드시 사설망 대역을 사용해야 하며, 인터넷 연결이 필요하지 않더라도 가능하면 사설망 대역을 사용하는 것을 권장합니다. 사설망 대역은 `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`가 있습니다.

  - VPC는 독립된 네트워크 환경으로 구성되기 때문에 CIDR이 같거나 겹치더라도 생성하는 것이 가능

    - 추후에 다수의 VPC를 함께 사용하는 경우 IP 대역이 겹치면 문제가 발생할 수 있음
      - **VPC를 만드는 것은 쉽지만 한 번 만들고 나면 기존 CIDR을 변경하는 것은 불가능**
        - 변경 불가, 새로운 CIDR 추가는 가능
      - 문제 생겨서 VPC 내부 자원 이동하게 되면 힘드므로
        - 프로덕션 환경을 구축할 때는 VPC 제약사항들을 충분히 이해하고 CIDR을 정하는 것이 좋다!!!!!
          - 기본 VPC의 CIDR 블록은 `172.31.0.0/16`

<br>

<br>

### 2. 서브넷 (Subnet)

- VPC만 가지고는 아직 아무것도 할 수 없음
  - VPC는 다시 한 번 CIDR 블록을 가지는 단위로 나눠진다
- 서브넷은 실제로 리소스가 생성되는 물리적인 공간인 `가용존 (AZ: Available Zone)`과 연결
  - VPC 가 논리적인 범위를 의미한다면,
  - Subnet은 VPC 안에서 실제로 리소스가 생성될 수 있는 네트워크
    - 다른 서비스의 resource 를 생성할 때 VPC만 지정하는 경우는 없다!
      - VPC 와 Subnet을 모두 지정하거나
      - Subnet을 지정하면 VPC 는 자동적으로 유추되기도 한다!
- 하나의 VPC 는 N개의 Subnet을 가질 수 있다
  - `Subnet 의 최대 크기` == `VPC 크기`
  - VPC 와 동일한 크기의 Subnet을 하나만 만드는 것도 가능
  - subnet을 만들지 안을 수도 있지만, 이 경우 VPC 로 아무것도 할 수 없음
  - 일반적으로 사용할 수 있는 AZ를 고려해서 적절한 크기의 Subnet들을 AZ 수만큼 생성해서 사용
    - **N 개의 AZ만큼 Subnet을 만들어 리소스를 분산하면 재해 대응 측면에서도 유리함!!**
      - `ap-northeast-2`   (Asia Pacific Seoul) 에는 4개의 AZ 가 있음! - 07.17.2020  
        - AWS region에 위치한 AZ는 백업 전원 장비, 네트워킹 및 인터넷 연결 기능이 있는 별도 시설을 갖춘 **한 개 이상의 개별 데이터 센터**로 구성됨
- Subnet의 netamask 범위는 16 (65535 개) 에서 28 (6개)을 사용할 수 있음
- VPC CIDR block 범위에 속하는 CIDR  block을 지정 할 수 있음
  - 하나의 subnet은 하나의 AZ와 연결
    - 1 subnet - 1 AZ
  - Region에 따라서 사용 가능한 AZ의 개수는 다르다
    - 보통 2개 이상
    - 우리 서울은 4개! 짝짝짝!
  - 재해 대응을 위해 AZ만큼 subnet을 나누는 경우 특정 region 에서 사용 가능한 가용존의 개수를 미리 확인할 필요가 있음
    - 모든 AZ를 사용하지 않더라도 2개 이상의 AZ를 사용하는 게 일반적
      - 그래서 면접 과제에  AZ (subnet) 2개 인듯
  - 기본  VPC 에서는 AZ 개수만큼 `Netmask` 20의 subnet을 자동적으로 생성함

<br>

`+`

#### Subnet을 2개 생성하는 이유

- 가용존 하나와 연결된 하나의 서브넷만 있더라도 EC2 인스턴스를 생성하는 것은 가능!
  - but, EC2를 비롯한 많은 AWS의 서비스에서는 멀티AZ라는 개념을 지원하고 있다
  - 하나 이상의 가용존에 유사한 리소스를 동시에 배치하는 기능

- 이렇게 하는 이유는 **장애 대응**과 관련이 있다!
  - 하나의 리전에는 다수의 가용존들이 있음
  - 이 가용존은 단순히 가상적으로 분리되어있는 것이 아니고, 물리적인 공간도 분리되어있다!
    - 다수의 가용존에 유사한 리소스를 배치함으로써 하나의 가용존에 문제가 생기더라도 서비스에 장애가 발생하지 않도록 설계하는 것이 가능
  - AWS에서는 리전 당 2개 이상의 가용존을 제공하고, 2개 이상의 가용존(서브넷)을 전제로 네트워크를 설계하는 것을 권장한다!

<br>

<br>

### 3. Route Table

> Subnet과 연결되어있는 resource

- Subnet에서 network를 이용할 때 `Route table` 을 사용해서 목적지를 찾게 됨

  - Route table은 Subnet과 연결되어 있지만 VPC를 생성할 때 만들어지고 VPC에도 연결되어 있음
  - router table은 VPC에 속한 Subnet을 만들 때 기본 route table로 사용됨

- **하나의 route table은 VPC에 속한 다수의 Subnet에서  사용할 수 있음**

- 자동 생성되는 Route table에는 한 가지 rule만 정의되어 있음

  - VPC의 CIDR block을 목적지로 하는 경우 타깃이 `local` 인 규칙

    - ex) VPC의 CIDR Block이 `127.31.0.0/16` 일 때 network 안에서 목적지가 `192.31.0.0/16` 범위에 있는 resource 를 찾는다면 VPC 내부에서 찾는다

    - 이 규칙은 삭제할 수 없다!!!!!

      - 인터넷을 연결하거나, 다른 VPC와 통신하기 위해서는 Route table에 Route 규칙을 추가적으로 정의해야 함!

<br>

<br>

### 4. 인터넷 게이트웨이 (Internet Gateway)

- VPC는 기본적으로 격리된 네트워크 환경
  - VPC에서 생성된 resource들은 기본적으로 인터넷을 사용할 수가 없음
    - 인터넷에 연결하기 위해서는 Internet Gateway가 필요하다!
- Routing table에 Internet Gateway를 향하는 적절한 **규칙**을 추가해주면 특정 Subnet이 인터넷과 연결됨
  - but, `Subnet`과 `Internet Gateway` 를 연결하는 것 만으로는 인터넷을 사용할 수 없다!
    - Internet을 사용하고자 하는 resource는 Public IP를 가지고 있어야 함

<br>

`+`

#### NAT 게이트웨이

: Private subnet의 인터넷을 향한 Outbound 트래픽을 허용해줌 (IPv4용)

<br>

<br>

### 5. DHCP Option Set

> TCP/IP Network 상의 Host로 설정 정보를 전달하는 DHCP 표준

- DHCP를 사용하면
  - Domain Name Server
  - Domain Name
  - NTP (Network Time Protocol) Server
  - NetBIOS Server
    - 등의 정보를  설정할 수 있음
- 일반적으로 VPC 생성 시 만들어지는 **DHCP Option set**을 그대로 사용

<br>

<br>

### 6. Network ACL (Access Control List)

> 주고 (outbound), 받는 (inbound) traffic을 제어하는 가상 방화벽

- 하나의 Network ACL 은 다수의 Subnet 에서 재 사용 할 수 있음
- subnet 앞 단에서 traffic을 제어하는 역할

<br>

<br>

### 7. Security Group

> Instance의 앞 단에서 Traffic을 제어하는 가상 방화벽

- Network ACL의 규칙을 통과하더라도 Security Group의 규칙을 통과하지 못 하면 Instance와 통신하지 못 할 수 있음

<br>

*Network ACL과 Security Group 을 통해서 안전한 네트워크 환경을 구축할 수 있다* !

<br>
