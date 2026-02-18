# HTTP vs HTTPS

> [Previously written article](https://chloe-codes1.gitbook.io/til/server/server-101/https_and_ssl)

<br>

### What is HTTP?

An abbreviation for Hypertext Transfer Protocol, it refers to a communication protocol for transferring Hypertext HTML

<br>

### What is HTTPS?

- The last `S` in HTTPS stands for **Over Secure Socket Layer**, and as the word Secure suggests, it can be inferred that it is **security-enhanced** HTTP
- HTTP transmits data in an unencrypted manner, making it very easy to intercept messages exchanged between the Server and client
  - It is not safe!
    - ex) During the process of sending a password to the server for login or viewing important confidential documents, malicious **eavesdropping** or **tampering** of data can occur!
  - That's why **HTTPS** was developed to address this!

<br>

### HTTPS and SSL (Secure Socket Layer)

- Many people understand HTTPS and SSL as having the same meaning (myself in the past...)
  - This is like understanding the Internet and the Web as having the same meaning!
- `Why?`
  - Just as the Web is one of the services running on top of the Internet,
  - HTTPS is also a Protocol running on top of the SSL Protocol!
- When HTTP operates on top of SSL, it becomes HTTPS!

<br>

### SSL and TLS

- These two are actually the same thing!
  - **SSL** was invented by Netscape, and as it became increasingly widely used, it was renamed to **TLS** when management was transferred to the standards body `IETF`
  - **TLS** 1.0 succeeds **SSL** 3.0
  - Therefore, the official name is **TLS**
    - However, the name **SSL** is used much more commonly than **TLS**!

<br>

### Types of Encryption Used in SSL

- `Symmetric-key algorithm`
  - An encryption technique where **the same key** is used for both `encryption` and `decryption`
    - The party performing `encryption` and the party performing `decryption` have the same key!
  - Disadvantages
    - It is difficult to transmit the symmetric key between the parties exchanging encrypted messages
      - If the symmetric key is **leaked**, an attacker who obtains the key can **decrypt** the encrypted content, rendering the encryption useless...!
      - This problem is called `key distribution problem`.
- `Public-key/asymmetric cryptography`
  - An encryption method that emerged to improve the `key distribution problem` of symmetric keys
  - Unlike symmetric keys, there are two keys
    - If you encrypt with key `A`, you can decrypt with key `B`,
    - If you encrypt with key `B`, you can decrypt with key `A`
  - One of the two keys is designated as the **private key**,
    - And the other is designated as the **public key**!
  - Even if the public key is leaked, the information cannot be decrypted without knowing the private key, so it is **safe**!
    - Why?
      - Because the public key can be used for encryption but not for decryption!
