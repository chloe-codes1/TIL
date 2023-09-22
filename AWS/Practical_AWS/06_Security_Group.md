# Security Group

> Security Group 자세-히 알아보기 실무 ver.

<br>

<br>

### Before getting started

- 기존에 Firewall (방화벽)이라고 부르는 것을 AWS가 `Security Group` 이라고 이름을 지음
- 물리 server는 필요할 때마다 증설하는 것이 물리적으로 시간이 오래 걸린다
  - Data center의 VM 환경, OpenStack, VM Ware 등은 어느 정도는 빠른 속도로 가능하다
    - but, 그래도 Public Cloud 3사만큼 빠른 속도를 갖지는 않는다
- `Security Group` 이라는 개념 자체가 on-premise 환경의 방화벽 설정의 개념과는 차이가 난다
  - 방화벽 group을 **논리 mapping** 하기 위해 `security group` 이라는 이름을 갖게 되었다!

<br>

<br>

### Security Group Rule Set

`Security group rule set` 자체가 EC2를 감싸는 형식이기 때문에 (EC2 바깥에서 제어) 접근이 왜 안되는지 확인할 때 EC2에 접속해서 확인하는 것이 아니라 **rule set**을 보고 확인해야 한다

<br>

#### Rule Set 설정하기

- Security Group 1개당 최대 규칙 (Rule Set) 수 == 200개

- EC2 1개 최대 할당 SG 수 == 5개
  - 즉, EC2 1대당 설정 가능한 최대 규칙 (rule set) 수 == 1000개
- ex) EC2 1개당 SG을 10개까지 할당하고 싶어!
  - SG 1개당 규칙 (Rule set)을 줄여야한다

<br>

<br>

### Inbound Rules

- 접근을 허용할지 말지를 설정하는 것이 `Inbound rule`이다
- (우리는) Inbound 전체를 닫아놓고 필요한 규칙만 열어주는 형식을 사용하고 있다
  - 권한을 할당할 때는 작은 권한을 주고, 넓혀 나가는 방식으로 해야한다!
    - why?
      - 과도하게 주어진 권한 할당을 줄이는 것은 적용되는 것들을 모두 찾아내야 하므로 어렵다

<br>

<br>

### Outbound Rules

- `Outbound rule` 마저도 `Inbound rule` 처럼 tight 하게 막아버리면 inbound도 봐야하고 outbound도 봐야하므로 복잡도가 증가한다
- 내부에서 나가는 traffic을 제어할 것인가는 고민해야할 부분이다
  
  - 아무 곳에나 요청을 보내도 되도록 허용할 것인가?
  
    - 여기서 **아무곳**은 `NAT Gateway`를 뜻한다!
  