# HTTPS and SSL

> 헷갈리는 개념들을 정리해요
>
> Reference: [생활코딩 강좌](https://opentutorials.org/course/228/4894)

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
    -  ex) 로그인을 위해 Server로 비밀번호를 전송하거나 중요한 기밀 문서를 열람하는 과정에서 악의적인 **감청**이나 데이터의 **변조**등이 일어날 수 있다는 것!
  - 그래서 이를 보완한 것이 **HTTPS** 다!

<br>

<br>

## HTTPS 와 SSL

- HTTPS 와 SSL을 같은 의미로 이해하고 있는 경우가 많다 (과거의 나...)

  - 이것은 마치 인터넷과 Web을 같은 의미로 이해하는 것과 같다!
  - `Why?`
    - Web이 인터넷 위에서 돌아가는 서비스 중 하나인 것 처럼
    -  HTTPS 도 SSL Protocol 위에서 돌아가는 Protocol이다!

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

<br>

<br>

### 공개키 방식

- 대칭키 방식의 단점을 개선하기 위해 등장한 암호화 방식
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
           - 이러한 것을 **전자 서명**이라고 부른다!

<br>





<br>

<br>

*계속 공부중....*













