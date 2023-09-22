# HTTPS and SSL

> 헷갈리는 개념들을 정리해요
>
> Reference: [생활코딩 강좌](https://opentutorials.org/course/228/4894), [minix.tstory.com](https://minix.tistory.com/395),
> [Bill Buchanan 교수님 웹사이트](https://asecuritysite.com/encryption/)

<br>

<br>

## HTTPS vs HTTP

<br>

### HTTP 란?

- Hypertext Transfrer Protocol의 약자로, **Hypertext**인 **HTML**을 전송하기 위한 **통신 규약**을 의미

<br>

### HTTPS 란?

- HTTPS 의 마지막 `S` 는 **Over Secure Socket Layer** 의 약자로 Secure라는 말에서 알 수 있듯이 **보안이 강화된** HTTP 라는 것을 짐작할 수 있다
- HTTP 는 암호화되지 않은 방법으로 데이터를 전송하기 때문에 Server와 client가 주고 받는 메시지를 감청하는 것이 매우 쉽다
  - 안전하지 않다!
    - ex) 로그인을 위해 Server로 비밀번호를 전송하거나 중요한 기밀 문서를 열람하는 과정에서 악의적인 **감청**이나 데이터의 **변조**등이 일어날 수 있다는 것!
  - 그래서 이를 보완한 것이 **HTTPS** 다!

<br>

<br>

## HTTPS 와 SSL

- HTTPS 와 SSL을 같은 의미로 이해하고 있는 경우가 많다 (과거의 나...)

  - 이것은 마치 인터넷과 Web을 같은 의미로 이해하는 것과 같다!
  - `Why?`
    - Web이 인터넷 위에서 돌아가는 서비스 중 하나인 것 처럼
    - HTTPS 도 SSL Protocol 위에서 돌아가는 Protocol이다!

  <br>

![img](https://sites.google.com/site/tlsssloverview/_/rsrc/1337752119392/ssl-tls-protocol-layers/ssllayers.gif)<br>

HTTP가 SSL 위에서 동작하면 HTTPS가 되는 것이다!

<br>

![image-20200828180431690](../../images/image-20200828180431690.png)

<br>

<br>

## SSL 과 TLS

- 이 둘은 사실 같은말이다!
  - Netscape에서 **SSL**이 발명되었고, 이것이 점차 폭넓게 사용되다가 표준화 기구인 `IETF` 의 관리로 변경되면서 **TLS**라는 이름으로 바뀌었다
  - **TLS** 1.0 은 **SSL** 3.0을 계승한다
  - 그래서 정식 명칭은 **TLS**이다
    - but, **TLS**라는 이름보다 **SSL**이라는 이름이 훨씬 많이 사용된다!

<br>

<br>

## SSL 디지털 인증서

<br>

### SSL 인증서란?

- Client와 Server의 **통신**을 제 3자가 **보증**해주는 **전자화된 문서**
  - Client 가 Server에 접속한 직후 Server는 Client에게 **SSL 인증서** 정보를 전달한다
  - Client는 이 인증서 정보가 신뢰할 수 있는 것인지를 **검증** 한 후에 다음 절차를 수행하게 된다

<br>

### SSL 디지털 인증서를 이용했을 때의 이점

- 통신 내용이 공격자에게 **노출**되는 것을 막을 수 있다
  - 그러기 위해서는 **암호화**가 필요하다!
- Client가 접속하려는 server 가 **신뢰 할 수 있는** 서버인지 판단할 수 있따
- 통신 내용의 **악의적인 변경**을 방지할 수 있다

<br>

<br>

## SSL에서 사용하는 암호화의 종류

<br>

### 암호화란?

- 정보를 원격지에 전달할 때 중간에서 누군가가 정보를 가로채면 보안이 위협받는다
  - 이 때 누군가가 가로채더라도 정보를 해석할 수 없게 하고, 목적지에 있는 수신자는 해석할 수 있도록 하는 것이 **암호화**이다!
- 누군가에게 전송하는 것이 아니라 자기 혼자서 보는 정보라도 자기가 아닌 다른 사람이 그것을 이해할 수 없고, 자신만이 그것을 이해할 수 있게 하는것도 **암호화**이다!

<br>

### 복호화란?

- **암호화**된 정보를 암호화 되기 이전 상태로 돌리는 것!

<br>

#### Key 란?

- 암호화 & 복호화의 **기준**이 되는 데이터
- Key를 가지고 있어야지만 정보를 **암호화**, **복호화** 할 수 있다

<br>

<br>

### 대칭키 방식 (Symmetric-key algorithm)

- **동일한 키**로 `암호화`와 `복호화`를 같이 할 수 있는 방식의 암호화 기법
  - `암호화`를 하는 쪽과 `복호화`를 하는 쪽이 동일한 Key를 가지고 있다!

<br>

#### 실습) 대칭키로 암호화 해보기

> 실습에 사용할 txt 파일 생성

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

> 대칭키로 암호화 하기

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl enc -e -des3 -salt -in plaintext.txt -out ciphertext.bin
enter des-ede3-cbc encryption password:
Verifying - enter des-ede3-cbc encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

- 명령어 설명
  - `enc -e -des3`
    - **des3** 방식으로 암호화 하기
  - `-in plaintext.txt -out ciphertext.bin`
    - plaintext.txt 파일을 암호화 한 결과를 ciphertext.bin 파일에 저장하기

<br>

> 암호화 된 파일 확인

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat ciphertext.bin 
7�x�w1������q�˴.!{�ՙ����e
```

<br>

> 대칭키로 복호화 하기

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl enc -d -des3 -in ciphertext.bin -out plaintext2.txt;
enter des-ede3-cbc decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

- 명렁어 설명
  - `enc -d`
    - 위의 옵션으로 ciphertext.bin 파일을 plaintext2.txt 파일로 복호화 하기

<br>

> 복호화 결과 확인

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat plaintext2.txt 
this is a plain text
```

- 공개키만 입력하면 그대로 복호화가 가능하다!
  - 이것이 대칭키의 문제
    - 공개키가 노출되면 보안 위협을 받는다

<br>

#### 대칭키 방식의 문제점

- 암호를 주고 받는 사람들 사이에 대칭키를 전달하는 것이 어렵다
  - 대칭키가 **유출**되면 키를 획득한 공격자는 암호의 내용을 **복호화** 할 수 있기 때문에 암호가 무용지물이 된다...!
  - 이러한 문제를 "key distribution problem"이라고 한다.

<br>

<br>

### 공개키/비대칭키 방식 (Public-key/asymmetric cryptography)

- 대칭키가 가지고 있는 "key distribution problem"을 개선하기 위해 등장한 암호화 방식
- 대칭키와는 다르게 Key가 두 개 있다
  - `A` key로 암호화를 하면 `B` key로 복호화 할 수 있고,
  - `B` key로 암호화하면 `A` key로 복호화 할 수 있는 방식
- 두 개의 키 중 하나를 **비공개 키 (private key, 개인키, 비밀키)**로 하고,
  - 나머지를 **공개키 (public key)**로 지정한다!

<br>

#### 공개키 방식 예시

- 비공개키는 자신만이 가지고 있고,
  1. 공개키를 타인에게 제공한다
  2. 공개키를 제공 받은 타인은 공개키를 이용해서 정보를 **암호화**한다
  3. 암호화한 정보를 비공개키를 가지고 있는 사람에게 전송한다
     - 비공개키의 소유자는 `비공개키`를 이용해서 암호화된 정보를 **복호화**한다
       - 이 과정에서 공개키가 유출된다고해도 비공개키를 모르면 정보를 복호화 할 수 없기 때문에 **안전**하다!
         - why?
           - 공개키로는 암호화는 할 수 있지만 복호화는 할 수 없기 때문!

<br>

#### 공개키 방식의 응용

1. 비공개키의 소유자는 `비공개키`를 이용해서 정보를 **암호화** 한 후에 `공개키`와 함께 암호화된 정보를 전송한다
2. 정보 + `공개키` 를 획득한 사람은 공개키를 이용해서 암호화된 정보를 **복호화**한다
   - 이 과정에서 `공개키`가 **유출**된다면 공격자에 의해 데이터가 **복호화** 될 위험이 있다
     - but, 이런 위험에도 불구하고 비공개키를 이용해서 암호화를 하는 이유는 이것이 **데이터를 보호하는 목적이 아니기 때문이다**!
       - 암호화된 데이터를 `공개키`를 가지고 **복호화** 할 수 있다는 것은 그 데이터가 공개키와 쌍을 이루는 `비공개키`에 의해 **암호화** 되었다는 것을 의미한다!
         - 즉, `공개키`가 데이터를 제공한 사람의 **신원**을 **보장**해주게 되는 것이다!
           - Why?
             - `공개키`를 이용하여 **복호화**에 성공했다는 것은 `비밀키`를 가지고 있는 사람이 전송한 정보라는 것을 **보증**하는 것이기 때문!
               - 이것이 바로 인증서의 원리이다!
           - 이러한 것을 **전자 서명**이라고 부른다

<br>

#### 실습) `RSA` 방식의 공개키 사용해보기

> `private.pem` 이라는 이름의 key 생성

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl genrsa -out private.pem 1024;
Generating RSA private key, 1024 bit long modulus (2 primes)
......+++++
................................+++++
e is 65537 (0x010001)
```

- 명령어 설명
  - `openssl`
    - openssl로
  - `genrsa`
    - **RSA** 방식으로 된 private key를 생성하라
  - `1024`
    - 암호의 **복잡도**를 의미
      - 숫자가 커질수록 **안전**해지지만 더 많은 **컴퓨팅 파워**를 필요로 한다!

<br>

> 생성된 **private key** 확인

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

> 생성한 **비공개키**에 대한 **공개키** 생성

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl rsa -in private.pem -out public.pem -outform PEM -pubout;
writing RSA key
```

- 명령어 설명
  - `-in private.pem`
    - private.pem 이라는 파일을 가져와서
  - `-out public.pem`
    - public.pem 이라는 파일을 만들어라
- 결과 설명
  - `writing RSA key`
    - RSA 방식의 Key를 생성했다는 뜻

<br>

> 암호화 할 파일 생성

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ echo 'studying public key' > file.txt

chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat file.txt 
studying public key
```

<br>

> 생성한 **공개키**로 **암호화**하기

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl rsautl -encrypt -inkey public.pem -pubin -in file.txt -out file.ssl;
```

- 명령어 설명
  - `openssl`
    - openssl을 이용해서
  - `-encrypt`
    - 암호화 해라
  - `-inkey public.pem`
    - key로 public.pem을 사용하겠다
      - 공개키를 가지고있는 사람이 암호화를 한다는 뜻
        - 즉, 비공개키를 가지고 있는 사람에게 은밀하게 어떤 정보를 전송할 때 사용하는 명령!
  - `-in file.txt`
    - file.txt 파일을 암호화 하겠다
  - `-out file.ssl`
    - 암호화 된 파일을 file.ssl로 export 하겠다

<br>

> **공개키**로 **암호화** 한 파일 확인하기

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat file.ssl 
�
 ��b1�T�:�P��NU�0PwU'��� ����D�K�Y�7���������q5�p�����FA\��}�qĴ/=��i�!�s����S@ݪE����l�B��tJv�
                      ~,
��]�V����>7
```

- 이를 통해 `공개키`로 **암호화** 된 파일을 `비공개키`를 가지고 있는 사람에게 전송하는 과정에서 누군가가 암호화 된 파일을 열어보려고 했을 때, 내용을 읽어볼 수 없다는 것, 즉 암호화 되어있는 것을 확인 할 수 있다!

<br>

> **비공개 키** 로 **복호화** 하기

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ openssl rsautl -decrypt -inkey private.pem -in file.ssl -out decrypted.txt
```

- 명령어 설명
  - `openssl`
    - openssl을 사용하여
  - `-decrypt`
    - 암호를 복호화 하겠다
  - `-inkey private.pem`
    - private.pem 파일을 사용하여 복호화 하겠다
  - `-in file.ssl`
    - file.ssl 파일을
  - `-out decrypted.txt`
    - 복호화 된 파일을 decrypted.txt로 export 하겠다

<br>

> 비공개키로 **복호화** 된 파일 확인

```bash
chloe@chloe-XPS-15-9570 ~/SSAFY/TIL-codes/ssl
$ cat decrypted.txt 
studying public key
```

#### 공개키/비대칭키 방식의 단점

- 비대칭키는 대칭키보다 속도가 느리다...
  - 속도를 중요시하는 상황에서는 쓰기가 힘들다...(화상채팅, 메신저, 등등)

- 이 때문에 속도를 중요시하는 대부분의 암호화 프로토콜에서는 대칭키와 비대칭키를 섞어서 쓴다.

#### 대칭키/비대칭키 프로토콜들

- 대표로써 리눅스 커널에 내장된 [wireguard Section 5.2](https://www.wireguard.com/papers/wireguard.pdf), 메신저
  앱인 [signal의 X3DH (whatsapp에서도 이가 사용된다!)](https://signal.org/docs/specifications/x3dh/)가 있다.

<br>

<br>

## SSL 인증서 ... 부터 공부하면 됨

<br>

<br>

*계속 공부중....*
