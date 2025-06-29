# VPC Peering

> VPC Peering 자세-히 알아보기 실무 ver.
>
> Reference: [aws docs](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html)

<br>

<br>

### What is VPC Peering?

- 서로 다른 두 개의 VPC를 연결해 주는 기능
  - 두 개의 VPC가 연결되면 내부 통신 할 수 있는 통로가 생긴다!
- `다른 계정` / `다른 region`에서도 peering 설정이 가능하다
  - 서로 다른 region 간 peering connection을 설정함으로써 얻는 효과
    - **DR (Disaster Recovery: 재해 복구)** 구성 가능
    - 여러 region을 peering 해놓고 사용 가능하다
      - ex) 태국 서비스를 국내에서 접속

<br>

<br>

### Working with VPC Peering

- `Requester VPC` & `Accepter VPC`
  - 이름이 requester와 accepter지만, 방향을 뜻하는 것은 아니다!
    - Subnet 통신에 따라 방향을 다르게 설정할 수 있다
- 보내려는 VPC의 CIDR Block >= 받는 VPC의 CIDR Block
  - why?
    - 보내려는 VPC의 CIDR Block보다 받는 VPC의 CIDR Block이 더 크면 당연하 통신이 안된다!
  - 보통은 두 VPC의 CIDR Block을 같게 설정하지만, 받는 VPC가 더 작게 할 수 있다
    - 작아도 문제되지 않는다

<br>

<br>

### Things you should be aware of

1. `Peering Connection` 설정 시 두  개의 VPC의 `CIDR Block`이 충돌하면 안된다
   - why?
     - 각각의 VPC가 따로 존재하는 것이 아니라 둘을 연결하는 것이므로 충돌나는 CIDR을 가지면 안된다

2. **Peeriing 구간**을 통과하면 금액이 더 부과된다
   - 하지만 큰 금액은 아니다!
