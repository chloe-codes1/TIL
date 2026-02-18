# VPC Peering

> A deep dive into VPC Peering - Practical ver.
>
> Reference: [aws docs](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html)

<br>

<br>

### What is VPC Peering?

- A feature that connects two different VPCs
  - Once two VPCs are connected, a pathway for internal communication is created!
- Peering can also be configured across `different accounts` / `different regions`
  - Benefits of setting up peering connections between different regions
    - **DR (Disaster Recovery)** configuration becomes possible
    - You can peer multiple regions and use them
      - e.g.) Accessing a Thailand service from within the country

<br>

<br>

### Working with VPC Peering

- `Requester VPC` & `Accepter VPC`
  - Although the names are requester and accepter, they do not indicate direction!
    - Direction can be configured differently based on subnet communication
- Sending VPC's CIDR Block >= Receiving VPC's CIDR Block
  - Why?
    - If the receiving VPC's CIDR Block is larger than the sending VPC's CIDR Block, communication obviously won't work!
  - Typically, the CIDR Blocks of both VPCs are set to be the same, but the receiving VPC's can be smaller
    - Being smaller is not a problem

<br>

<br>

### Things you should be aware of

1. When configuring a `Peering Connection`, the `CIDR Blocks` of the two VPCs must not conflict
   - Why?
     - Since the two VPCs are being connected rather than existing separately, they cannot have conflicting CIDRs

2. Additional charges apply when traffic passes through the **peering connection**
   - However, it's not a significant amount!
