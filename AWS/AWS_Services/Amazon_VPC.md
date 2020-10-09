# Amazon VPC

> 꼭 알고 넘어가야 하는 AWS VPC!
>
> Reference: [인프런] DevOps : Infrastructure as Code with Terraform and AWS 강좌 by 송주영님

<br>

<br>

## Amazon VPC란?

- Amazon에서 제공하는 **private**한 네트워크 망 서비스
  - 사용자에게 aws 계정 전용 네트워크망을 만들어주는 서비스

<br>

<br>

## VPC의 핵심 구성요소

<br>

### Virtual Private Cloud (VPC)

- 사용자의 AWS 계정 전용 가상 네트워크

<br>

### Subnet

- VPC의 IP address 범위
  - 해당 VPC 안에서 IP 주소 범위를 어디까지 나누느냐에 대한 것
- Public Subnet vs Private Subnet
  - **Public Subnet**
    - EC2 같은 machine에 `공인 IP`가 붙어있으면 보통 Public subnet에 위치한 EC2 인스턴스라고 볼 수 있다
  - **Private Subnet**
    - `공인 IP`를 가지고 있지 않지만, `NAT Gateway`를 통해 인터넷을 할 수 있는 Subnet을 Private Subnet이라고 부른다

<br>

### Routing Table

- `Network traffic`을 **전달할 위치**를 결정하는데 사용되는 **routing**이라는 **규칙 집합**
  - 어떤 machine (ex. EC2)에서 **outbound**로 나가는 traffic이 어디로 나가느냐에 대한것
    - 내부로 나가느냐 외부로 나가느냐에 대한 규칙을 정하는 table

<br>

### Internet Gateway

- VPC의 **resource**와 **인터넷** 간의 통신을 활성화하기 위해 VPC에 연결하는 **gateway**
  - 인터넷을 연결하기 위해 필요한 서비스
  - 라우팅 테이블에 인터넷으로 나가는 서비스가 `Internet Gateway` 를 통한다면 **Public Subnet**이라고 부른다

<br>

### NAT Gateway

- `Network 주소 변환`을 통해 **Private subnet**에서 **인터넷** 또는 **기타 AWS 서비스**에 연결하는 gateway
  - 라이팅 테이블에 인터넷으로 나가는 서비스가 `NAT Gateway`를 통한다면 **Private Subnet**이라고 부른다

<br>

### Security Group

- 보안 그룹은 **instance**에 대한 `Inbound` 및 `Outbound` traffic을 제어하는 **가상 방화벽** 역할을 하는 규칙 집합
  - Inbound traffic을 어떤 규칙을 통해서 허용할 것인지
  - Outbound traffic을 어떤 규칙을 통해서 허용할 것인지에 관한 규칙을 가지고 있는 집합

 <br>

### VPC Endpoint

- VPC에 종속되어 있는 VPC 내부의 여러 AWS 서비스 간에 **Internet Gateway**나 **NAT Gateway**를 통하지 않고 바로 AWS 서비스를 사용할 수 있는 AWS 의 서비스
  - `Internet gateway`, `NAT device`, `VPC 연결` 또는 AWS Direct Connect 연결을 필요로 하지 않고, `PrivateLink` 구동 지원 및 AWS 서비스 및 VPC Endpoint service에 VPC를 비공개로 연결할 수 있다
  - **VPC의 Instance**는 **서비스의 resource** 와 통신하는 데 **Public IP**를 필요로 하지 않는다!
  - VPC와 기타 서비스 간의 traffic은 Amazon Network를 벗어나지 않는다



















