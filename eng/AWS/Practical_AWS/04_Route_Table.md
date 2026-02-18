# Route Table

> A deep dive into Routing Table - Practical ver.

<br>

<br>

### What is Route Table?

- A `routing table` affects **subnets**
- A `routing table` is **dependent** on the **VPC**
  - However, a single routing table can be associated with two or more subnets
    - That's why public subnets and DB subnets use the same routing table!
      - However, private subnets use separate routing tables to prepare for **NAT gateway** failures!

<br>

### Route Table in Private Subnet

- In the case of **private subnets**
  - If `FROM` is internal and `TO` is external, you can configure routing through the route table
  - But if `FROM` is external and `TO` is internal, it won't work!
    - You must configure it to go through a **Public LB**!
