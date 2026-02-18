# Security Group

> A deep dive into Security Group - Practical ver.

<br>

<br>

### Before getting started

- What was traditionally called a Firewall, AWS named `Security Group`
- Physical servers take a long time to scale up as needed
  - Data center VM environments, OpenStack, VMWare, etc. can do it at a reasonably fast speed
    - However, they still don't match the speed of the top 3 public cloud providers
- The concept of `Security Group` itself differs from the firewall configuration concept in on-premise environments
  - It was named `security group` to **logically map** firewall groups!

<br>

<br>

### Security Group Rule Set

Since the `Security group rule set` wraps around the EC2 (controlling from outside the EC2), when checking why access is blocked, you should look at the **rule set** rather than logging into the EC2 to check

<br>

#### Configuring Rule Sets

- Maximum number of rules (Rule Set) per Security Group == 200

- Maximum number of SGs assignable to a single EC2 == 5
  - Therefore, the maximum number of configurable rules (rule sets) per EC2 == 1000
- e.g.) I want to assign up to 10 SGs per EC2!
  - You need to reduce the number of rules (Rule set) per SG

<br>

<br>

### Inbound Rules

- `Inbound rules` determine whether to allow or deny access
- (We) use a pattern of closing all inbound traffic and opening only the necessary rules
  - When assigning permissions, start with minimal permissions and expand as needed!
    - Why?
      - Reducing excessively granted permissions is difficult because you have to find everything that's affected

<br>

<br>

### Outbound Rules

- If you lock down `Outbound rules` as tightly as `Inbound rules`, the complexity increases since you have to check both inbound and outbound
- Whether to control outbound traffic is something you need to consider

  - Should you allow requests to go anywhere?

    - Here, **anywhere** refers to the `NAT Gateway`!
