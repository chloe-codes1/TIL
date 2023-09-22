# Load Balancer

> Load Balancer 자세-히 알아보기 실무 ver.

<br>

<br>

### Application Load Balancer (ALB, Layer 7)

- `HTTP`, `HTTPS`, `Web Socket` routing
- **Security group** mapping 가능
- HTTP 2.0 도 된다
  - 이전에는 안됐었다
    - 그래서 gRPC, Web RPC 못했었다..!

<br>

### Network Load Balancer (NLB, Layer 4)

- 다 된다
  - `TCP`, `TLS`, `UDP` routing
- 단점
  - **Security Group** mapping이 안된다!

<br>

### Class Load Balancer (CLB, Layer 4)

- NLB와 유사하다 (Layer 4)
  - but, TargetGroup 지정이 안된다
- **Security group** mapping 가능
