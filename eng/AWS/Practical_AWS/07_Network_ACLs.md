# Network ACLs

> A deep dive into Network ACL - Practical ver.

<br>

<br>

### Before getting started

Things that can control the network besides firewalls

- Routing Table
  - Controls where to send packets
- Network ACL
  - Transmits or blocks packets based on rules

<br>

<br>

### What are Network ACLs?

- Rules that determine whether to block or allow certain packets
- Configured rules apply to all resources, so you can't set too many
  - They apply to all resources in the subnet
    - Therefore, Network ACLs must be well designed
      - Why? Even if the firewall (SG) is properly configured, access may be blocked due to a **Deny Rule** in the `Network ACL`
- The more `Network ACL` rules there are, the more confusing firewall configuration becomes, so it's best to keep `Network ACL` rules as concise as possible
  - If firewall settings are done properly, you don't need to configure `Network ACLs` separately!

<br>

<br>

### Rule number in Network ACLs

- Network ACL rules have priorities
  - They are applied in order of highest priority (Rule number)!

<br>

<br>

### Network ACLs and Well Known Ports

- The reason why `1024 - 65535` is allowed in the **Port Range** of Network Inbound rules
  - == Because they are `Well Known Ports`!
    - [Learn about well known ports](https://chloe-codes1.gitbook.io/til/network/11_tcp_and_udp#1-layer-4-protocol-tcp-udp-and-service-port)
