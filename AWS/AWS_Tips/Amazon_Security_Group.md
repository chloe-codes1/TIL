# Amazon Security Group

> Amazon 보안 그룹에 대해 알아보아요
>
> References: [책] AWS Discovery Book

<br>

### Amazon 보안 그룹 이란?

- 보안 그룹 (Security Group) 은 Instance에 대한 **inbound**, **outbound**의 Network Traffic을 제어하는 `가상의 방화벽` 역할을 수행한다
- EC2 Instance를 시작할 때 각 instance당 **최대 5개**의 보안 그룹을 할당할 수 있다
- 구성된 보안 그룹은 기존의 **On-premise** 에서 사용되고 있는 방화벽의 정책과 유사한 기능을 한다.
  - 다만, 보안그룹은 Network traffic에 대하나 **허용 (Allow)** 만 가능하며 **차단 (Deny)**은 설정할 수 없다!
    - why?
      - 보안그룹이 EC2 수준에 적용되기 때문에 적용되는 룰이기 때문!
        - **차단 기능**을 적용하기 위해서는 `VPC` 의 기능 중 하나인 `Network ACL` 을 통해 **Subnet** 수준에서 Network 흐름을 제어할 수 있다

<br>

<br>

### Amazon 보안 그룹의 주요 특징

<br>

#### 1. 보안 그룹은 생성 가능한 보안 그룹의 **숫자**와 **규칙** 에 제한이 있다

- VPC당 생성 가능한 보안 그룹의 개수는 기본 한도 **500개**이다
- 각 보안 그룹 당 추가할 수 있는 규칙 (rule) 의 개수는 **50개**로 제한되어 있다
- 네트워크 인터페이스 당 5개의 보안그룹을 적용할 수 있다
  - 다만, 필요한 경우 `AWS Support` 를 통해 한도 증가 요청을 할 수 있다

<br>

#### 2. 네트워크 트래픽을 위한 `허용 (Allow)` 정책은 있으나 `차단 (Deny)` 정책은 없다

- 일반적인 방화벽에서는 네트워크 흐름을 제어하기 위한 정책으로 허용 정책과 차단 정책이 모두 있다
  - but, 보안 그룹은 허용 정책은 있으나 차단 정책은 없다
    - 차단 정책을 적용하기 위해서는 **VPC**의 기능인 **Network ACL** 기능을 이용해야 한다.

<br>

#### 3. `Inbound Traffic`과 `Outbound Traffic`을 별도로 제어할 수 있다

<br>

#### 4. 초기 보안 그룹 설정에는 Inbound 보안 규칙이 없다

- 처음 EC2를 생성하고 다른 EC2와 통신하기를 원한다면,
  - 해당 EC2와의 통신을 위한 **Inbound 규칙**을 추가하여야만 EC2간 통신이 가능하다
