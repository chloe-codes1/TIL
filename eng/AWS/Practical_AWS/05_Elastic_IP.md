# Elastic IP

> A deep dive into Elastic IP - Practical ver.

<br>

<br>

### Elastic IP == Static IP

- When an EC2 Instance's `Elastic IP` field is empty but `Public IPv4` has a value
  - The IP changes when the instance is stopped & started
    - Assigning a value to **Elastic IP** allows you to use a fixed IP without this issue!
      - However, you cannot create an **Elastic IP** based on a previously assigned `Public IP`
        - You should set up the **Elastic IP** when initially creating the instance!

<br>

<br>

### Elastic IP Charges

- AWS charges you if an Elastic IP is not assigned to anything!
  - If it's attached to an EC2, there's no charge
    - Why?
      - AWS's reasoning is: "IPv4 is a finite resource, so we charge to encourage conservation when it's not in use"
        - However, if it's attached to an EC2, you're already paying for the instance, so they don't charge additionally

<br>

<br>

### Elastic IP address limit

- The number of **Elastic IPs** you can own per account is limited
  - Since IPv4 is a finite resource, AWS won't provide too many if you request excessively
  - By default, you can own 5 **Elastic IPs** per region

<br>

<br>

<br>

`+`

#### Public IP

- Just because something is in a public subnet doesn't mean it must have a public IP!
  - *But you probably created it in a public subnet because you need public connectivity, right?*
- If an EC2 exists in a public subnet without a Public IP
  - External to internal access is not possible
  - Internal to external access is also not possible
- The reason EC2 instances in a private subnet can access the outside even without a Public IP is because they go through the NAT's Public IP
- The reason SSH access works even without a Public IP
  - It's because firewall settings are configured
