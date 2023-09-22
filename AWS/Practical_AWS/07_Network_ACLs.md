# Network ACLs

> Network ACL 자세-히 알아보기 실무 ver.

<br>

<br>

### Before getting started

방화벽 외에 Network를 제어할 수 있는 것

- Routing Table
  - Packet을 어디로 보낼지 제어
- Network ACL
  - 규칙에 따라 packet을 전송 or 차단

<br>

<br>

### What are Network ACLS?

- 어떤 packet을 차단할지 말지에 대한 규칙
- 설정한 규칙은 모든 resource에 적용되므로 많이 설정할 수 없다
  - 해당 subnet의 모든 resource에 적용된다
    - 그렇기 때문에, Network ACL을 잘 설계해야한다
      - why? 방화벽(SG)은 제대로 설정했는데 `Network ACL`에 **Deny Rule**이 있어서 접근 불가일 수도 있다
- `Network ACL` 규칙이 많아질 수록 방화벽 설정에 있어서 헷갈리게 되므로 `Network ACL`은 최대한 간결한 규칙으로 가져가는 것이 좋다
  - 방화벽 설정을 잘하면 `Network ACL` 을 따로 설정하지 않아도 된다!

<br>

<br>

### Rule number in Network ACLs

- Network ACL 규칙에는 우선순위가 있다
  - 우선순위 (Rule number)가 높은 순서로 적용 받는다!

<br>

<br>

### Network ACL과 Well known Port

- Network Inbound rule에서 **Port Range**에 `1024 - 65535`를 허용해놓는 이유
  - == `Well known Port`이기 때문이다!
    - [well known port 알아보기](https://chloe-codes1.gitbook.io/til/network/11_tcp_and_udp#1-layer-4-protocol-tcp-udp-and-service-port)
