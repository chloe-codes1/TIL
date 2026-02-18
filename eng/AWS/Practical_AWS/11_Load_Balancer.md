# Load Balancer

> A deep dive into Load Balancer - Practical ver.

<br>

<br>

### Application Load Balancer (ALB, Layer 7)

- `HTTP`, `HTTPS`, `Web Socket` routing
- **Security group** mapping available
- HTTP 2.0 is also supported
  - Previously, it wasn't supported
    - So gRPC, Web RPC weren't possible..!

<br>

### Network Load Balancer (NLB, Layer 4)

- Supports everything
  - `TCP`, `TLS`, `UDP` routing
- Disadvantage
  - **Security Group** mapping is not supported!

<br>

### Classic Load Balancer (CLB, Layer 4)

- Similar to NLB (Layer 4)
  - However, TargetGroup specification is not supported
- **Security group** mapping available
