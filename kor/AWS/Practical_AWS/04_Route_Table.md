# Route Table

> Routing Table 자세-히 알아보기 실무 ver.

<br>

<br>

### What is Route Table?

- `routing table`은 **subnet**에 영향을 준다
- `routing table`은 **VPC**에 **종속적**이다
  - 단, 하나의 routing table이 2개 이상의 subnet에 연결될 수도 있다
    - 그래서 public subnet, db는 같은 routing table을 사용한다!
      - but, private은 **NAT gateway** 장애 시에 대비하여 각각 다른 routing table을 사용한다!

<br>

### Route Table in Private Subnet

- **Private subnet**의 경우
  - `FROM`이 내부고, `TO`가 외부이면 route table을 설정해서 routing 할 수 있지만
  - `FROM`이 외부, `TO` 가 내부면 안된다!
    - **Public LB**를 통과하도록 설정해야 한다!
