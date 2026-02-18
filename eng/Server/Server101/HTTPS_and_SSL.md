# HTTPS and SSL

> Organizing confusing concepts
>
> Reference: [Opentutorials Course](https://opentutorials.org/course/228/4894), [minix.tstory.com](https://minix.tistory.com/395),
> [Professor Bill Buchanan's Website](https://asecuritysite.com/encryption/)

<br>

<br>

## HTTPS vs HTTP

<br>

### What is HTTP?

- An abbreviation for Hypertext Transfer Protocol, which refers to the **communication protocol** for transmitting **Hypertext**, namely **HTML**

<br>

### What is HTTPS?

- The last `S` in HTTPS stands for **Over Secure Socket Layer**, and as the word Secure suggests, we can infer that it is an **HTTP with enhanced security**
- Since HTTP transmits data in an unencrypted manner, it is very easy to intercept messages exchanged between the Server and the client
  - It is not safe!
    - ex) During the process of sending a password to the Server for login or viewing important confidential documents, malicious **eavesdropping** or data **tampering** can occur!
  - That is why **HTTPS** was created to address this!

<br>

<br>

## HTTPS and SSL

- Many people understand HTTPS and SSL as the same thing (including my past self...)

  - This is like understanding the Internet and the Web as the same thing!
  - `Why?`
    - Just as the Web is one of the services running on top of the Internet,
    - HTTPS is also a Protocol running on top of the SSL Protocol!

  <br>

![img](https://sites.google.com/site/tlsssloverview/_/rsrc/1337752119392/ssl-tls-protocol-layers/ssllayers.gif)<br>

When HTTP operates on top of SSL, it becomes HTTPS!

<br>

![image-20200828180431690](../../kor/images/image-20200828180431690.png)

<br>

<br>

## SSL and TLS

- These two are actually the same thing!
  - **SSL** was invented at Netscape, and as it became widely used, it was transferred to the standards organization `IETF` and renamed to **TLS**
  - **TLS** 1.0 succeeds **SSL** 3.0
  - So the official name is **TLS**
    - but, the name **SSL** is used much more frequently than **TLS**!

<br>

<br>

## SSL Digital Certificate

<br>

### What is an SSL Certificate?

- An **electronic document** where a third party **guarantees** the **communication** between the Client and the Server
  - Right after the Client connects to the Server, the Server delivers the **SSL certificate** information to the Client
  - The Client **verifies** whether this certificate information is trustworthy, and then proceeds with the next steps

<br>

### Benefits of Using SSL Digital Certificates

- Communication content can be **prevented from being exposed** to attackers
  - **Encryption** is needed for this!
- The Client can determine whether the server it is trying to connect to is a **trustworthy** server
- **Malicious modification** of communication content can be prevented

<br>

<br>

## Types of Encryption Used in SSL

<br>

### What is Encryption?

- When transmitting information to a remote location, if someone intercepts it in the middle, security is threatened
  - In this case, **encryption** makes it so that even if someone intercepts the information, they cannot interpret it, while the recipient at the destination can interpret it!
- Even for information that is not being sent to anyone but is only viewed by oneself, making it so that no one else can understand it and only oneself can understand it is also **encryption**!

<br>

### What is Decryption?

- Reverting **encrypted** information back to its pre-encrypted state!

<br>

#### What is a Key?

- The **reference** data for encryption & decryption
- You must have the Key to **encrypt** and **decrypt** information

<br>

<br>

### Symmetric-key Algorithm

- An encryption method where `encryption` and `decryption` can both be performed with the **same key**
  - The side performing `encryption` and the side performing `decryption` have the same Key!

<br>

#### Practice) Encrypting with a Symmetric Key

> Create a txt file for practice

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ echo 'this is a plain text' > plaintext.txt;

chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ ls
plaintext.txt

chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat plaintext.txt
this is a plain text
```

<br>

> Encrypt with the symmetric key

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl enc -e -des3 -salt -in plaintext.txt -out ciphertext.bin
enter des-ede3-cbc encryption password:
Verifying - enter des-ede3-cbc encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

- Command explanation
  - `enc -e -des3`
    - Encrypt using the **des3** method
  - `-in plaintext.txt -out ciphertext.bin`
    - Save the encryption result of plaintext.txt to the ciphertext.bin file

<br>

> Check the encrypted file

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat ciphertext.bin
7�x�w1������q�˴.!{�ՙ����e
```

<br>

> Decrypt with the symmetric key

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl enc -d -des3 -in ciphertext.bin -out plaintext2.txt;
enter des-ede3-cbc decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

- Command explanation
  - `enc -d`
    - Decrypt the ciphertext.bin file into the plaintext2.txt file using the above option

<br>

> Check the decryption result

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat plaintext2.txt
this is a plain text
```

- Decryption is possible simply by entering the public key!
  - This is the problem with symmetric keys
    - If the public key is exposed, security is compromised

<br>

#### Problems with the Symmetric Key Method

- It is difficult to deliver the symmetric key between the people exchanging encrypted messages
  - If the symmetric key is **leaked**, an attacker who obtains the key can **decrypt** the encrypted content, rendering the encryption useless...!
  - This problem is called the "key distribution problem".

<br>

<br>

### Public-key/Asymmetric Cryptography

- An encryption method introduced to improve the "key distribution problem" of symmetric keys
- Unlike symmetric keys, there are two Keys
  - If you encrypt with `A` key, you can decrypt with `B` key,
  - If you encrypt with `B` key, you can decrypt with `A` key
- One of the two keys is designated as the **private key**,
  - and the other is designated as the **public key**!

<br>

#### Example of Public Key Method

- The private key is kept only by oneself,
  1. The public key is provided to others
  2. The person who received the public key **encrypts** the information using the public key
  3. The encrypted information is sent to the person who has the private key
     - The owner of the private key **decrypts** the encrypted information using the `private key`
       - In this process, even if the public key is leaked, the information cannot be decrypted without knowing the private key, so it is **safe**!
         - why?
           - Because the public key can encrypt but cannot decrypt!

<br>

#### Application of the Public Key Method

1. The owner of the private key **encrypts** the information using the `private key` and then transmits the encrypted information along with the `public key`
2. The person who obtained the information + `public key` **decrypts** the encrypted information using the public key
   - In this process, if the `public key` is **leaked**, there is a risk that the data will be **decrypted** by an attacker
     - but, despite this risk, the reason for encrypting with the private key is because **the purpose is not to protect the data**!
       - Being able to **decrypt** the encrypted data with the `public key` means that the data was **encrypted** by the `private key` that is paired with the public key!
         - In other words, the `public key` **guarantees** the **identity** of the person who provided the data!
           - Why?
             - Because successfully **decrypting** using the `public key` **certifies** that the information was transmitted by the person who holds the `private key`!
               - This is the principle behind certificates!
           - This is called a **digital signature**

<br>

#### Practice) Using `RSA` Public Key

> Generate a key named `private.pem`

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl genrsa -out private.pem 1024;
Generating RSA private key, 1024 bit long modulus (2 primes)
......+++++
................................+++++
e is 65537 (0x010001)
```

- Command explanation
  - `openssl`
    - Using openssl
  - `genrsa`
    - Generate a private key using the **RSA** method
  - `1024`
    - Refers to the **complexity** of the encryption
      - The larger the number, the **safer** it is, but it requires more **computing power**!

<br>

> Check the generated **private key**

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ ls -al
total 24
drwxr-xr-x  2 chloe chloe 4096  8월 31 01:16 .
drwxr-xr-x 12 chloe chloe 4096  8월 29 16:07 ..
-rw-r--r--  1 chloe chloe   40  8월 29 16:13 ciphertext.bin
-rw-r--r--  1 chloe chloe   21  8월 29 16:22 plaintext2.txt
-rw-r--r--  1 chloe chloe   21  8월 29 16:08 plaintext.txt
-rw-------  1 chloe chloe  887  8월 31 01:16 private.pem

chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat private.pem
-----BEGIN RSA PRIVATE KEY-----
MIICXQIBAAKBgQDCOq2X1U25ME8Pk8T5hAKTxNCHt1VOJY9oIPdPMEJM6OseJ/VX
fybsXxU8+17WXsgNBYkT0LlNhuGpEDvxoaydMeAC7aPNlyewLVxHC11vP7GS6ccJ
/ARF6DjjM6zm465/sSpE5FPz+1Mkce5jgbeXqYb4L3nVLzlfMpaK/v8/LwIDAQAB
AoGBALqnc03XogLXBxN8Oa5kC6oAWTojmGoqNF+oVqKWSRDqQZFQazlzq286jQl2
tJQkr/G7oRkW3A1CEzjKriCu81bMf07a+X8wPvOEXxT6iaZ9GnVSHAadGdHXFPq3
wvgNz8IBp7AZUbaDilZEPf1dHStGwd5L6f2ObDgkICEaqmURAkEA6tj0PH09OPfH
h4chH36qrjgSCxPhb4B8XjRvxGTydTrsC3n+ECA95o6AVBfsALFVj1Tu5ovngN15
AX2TBezXeQJBANO5KOJGf/B61riXySVOYHOBc8d7ExUk+2W5aK41T4n3YD9HfT9Q
8w8aPqzTSzsNXrCV2nO72WV+6hi5cVmuGecCQDBD6GYqIxP7MIG1DuSnJrLpiSPH
sTQ2Rtkhk7rcOExJkMuHBeUQi0hADzW5OOKnj3sGrJarOCfu3Him8zlrhJkCQEtw
AuA0zGsr6YvWEUZombcuHcmq0Y7MIYMKQAEqX4/CA5ooZ7kCp8fuyvwbQQfmaKG0
kyR/fyNJyDFNCdUxUmsCQQDSAIPLDrZr1fvykKX9CLr9HJLYSrHD36T3y26Kq+ci
bN/NFuaYjq9g6kkVqH7usaY28Ro+BQUHINyUB92S08SJ
-----END RSA PRIVATE KEY-----
```

<br>

> Generate a **public key** for the created **private key**

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl rsa -in private.pem -out public.pem -outform PEM -pubout;
writing RSA key
```

- Command explanation
  - `-in private.pem`
    - Take the file named private.pem
  - `-out public.pem`
    - Create a file named public.pem
- Result explanation
  - `writing RSA key`
    - Means that an RSA method Key has been generated

<br>

> Create a file to encrypt

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ echo 'studying public key' > file.txt

chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat file.txt
studying public key
```

<br>

> **Encrypt** with the generated **public key**

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl rsautl -encrypt -inkey public.pem -pubin -in file.txt -out file.ssl;
```

- Command explanation
  - `openssl`
    - Using openssl
  - `-encrypt`
    - Encrypt
  - `-inkey public.pem`
    - Use public.pem as the key
      - This means the person with the public key performs the encryption
        - In other words, this is a command used when secretly transmitting information to the person who has the private key!
  - `-in file.txt`
    - Encrypt the file.txt file
  - `-out file.ssl`
    - Export the encrypted file as file.ssl

<br>

> Check the file **encrypted** with the **public key**

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat file.ssl
�
 ��b1�T�:�P��NU�0PwU'��� ����D�K�Y�7���������q5�p�����FA\��}�qĴ/=��i�!�s����S@ݪE����l�B��tJv�
                      ~,
��]�V����>7
```

- Through this, we can confirm that when someone tries to open the file encrypted with the `public key` during the process of transmitting it to the person who has the `private key`, the content cannot be read, i.e., it is encrypted!

<br>

> **Decrypt** with the **private key**

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl rsautl -decrypt -inkey private.pem -in file.ssl -out decrypted.txt
```

- Command explanation
  - `openssl`
    - Using openssl
  - `-decrypt`
    - Decrypt the encryption
  - `-inkey private.pem`
    - Use the private.pem file for decryption
  - `-in file.ssl`
    - The file.ssl file
  - `-out decrypted.txt`
    - Export the decrypted file as decrypted.txt

<br>

> Check the file **decrypted** with the private key

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat decrypted.txt
studying public key
```

#### Disadvantages of Public Key/Asymmetric Key Method

- Asymmetric keys are slower than symmetric keys...
  - They are difficult to use in situations where speed is important... (video chat, messenger, etc.)

- Because of this, most encryption protocols that prioritize speed use a mix of symmetric and asymmetric keys.

#### Symmetric Key/Asymmetric Key Protocols

- Notable examples include [wireguard Section 5.2](https://www.wireguard.com/papers/wireguard.pdf) built into the Linux kernel, and the messenger
  app [Signal's X3DH (which is also used in WhatsApp!)](https://signal.org/docs/specifications/x3dh/).

<br>

<br>

## SSL Certificate ... continue studying from here

<br>

<br>

*Still studying....*
