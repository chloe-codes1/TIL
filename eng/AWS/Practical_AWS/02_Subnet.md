# Subnet

> A deep dive into Subnet - Practical ver.

<br>

<br>

### What is a Subnet?

- The IP address range of a VPC
  - It divides the VPC into segments
- AWS VPC cannot operate without subnets!

<br>

### Subnet Names

- It is a conceptual division
  - public
  - private
- You don't necessarily have to use `public` or `private` as subnet names
- Separating DB subnets is a matter of preference

<br>

### Subnet CIDR Block

- Subnets also require a CIDR block to be specified
- Subnet CIDRs must **not conflict** with each other
- Subnet CIDRs must **not exceed the VPC range**
  - Because the VPC size is the maximum IP constraint!
- Think of it as claiming territory within the VPC with subnets
  - If a subnet runs out of IPs, you can create another subnet in the unclaimed space!
    - However, when creating resources, there will be two **subnet options**, so you'll have to decide which subnet to choose...
      - Don't add subnets later -- design it properly from the start!
  - You can add subnets to the unclaimed space in the VPC, but you **cannot merge** two subnets
