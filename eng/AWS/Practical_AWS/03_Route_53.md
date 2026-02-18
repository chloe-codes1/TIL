# Route 53

> A deep dive into Route 53 - Practical ver.

<br>

<br>

### What is Amazon Route 53?

: A DNS (Domain Name Service) provided by AWS

<br>

<br>

### Supported DNS record types

: The [AWS docs](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/ResourceRecordTypes.html) provide detailed information, but here's a brief summary of the commonly used ones

- `A record type`
  - IPv4 address
- `AAAA record type`
  - IPv6 address
- `CNAME record type`
  - When a domain address points to another address
- `MX record type`
  - As the name suggests, mail server
- `SPF record type`
  - Mail related
- `TXT record type`
  - When queried, it returns one or more strings wrapped in `"`
  - Usage
    - reverse dns lookup
    - auth
      - **A method to verify that the domain owner is legitimate**
        1. Send an email to the domain owner
        - Authenticate by connecting a mail service (MX record type, etc.) to your domain and receiving the email
          - This method is a bit cumbersome, so the `TXT record type` below is used instead
        2. Have the owner enter a token in the `TXT record`
           - Authenticate by having them enter a value (token) you sent
             - This method is more preferred nowadays

<br>

<br>

### alias

- A feature exclusive to Route 53
- Used to connect AWS services
- LBs should NOT be connected using `CNAME`
  - Why?
    - Because the LB domain changes constantly
    - However, this is specific to the cloud environment!
  - ALBs are composed of Instances
    - An Instance has **2 + a** IPs
      - Why? Because more IPs are assigned when traffic is high
    - So multiple IPs are mapped and managed under a domain address

<br>

#### Why use alias?

- If you use `CNAME`
  - From the connecting client's perspective, when it queries for domain information, it has to ask for the final destination and then ask again!
    - Why?
      - `CNAME` follows chains of connections until it reaches the terminal **record**
        - Which is the IP
- The reason for using `alias` instead of `CNAME`
  - **Convenience**
    - `CNAME` requires multiple queries which is inconvenient, but using `alias` makes it simpler
      - How?
        - Since AWS services are all its own resources, **Route 53** queries on your behalf and returns the final IP in a single lookup
  - **Performance**
    - Performance is slightly better from the client's perspective
  - **Cost**
    - Route 53 billing structure
      - Query cost: A record < CNAME
        - CNAME is more expensive
        - alias cost == A record

<br>

<br>

### Route 53 Tips

- A single domain address can have multiple record types
  - You can add additional records to the same domain!
- If you want to add records of the same record type, you can register them as multiline
  - Don't create two separate records!
