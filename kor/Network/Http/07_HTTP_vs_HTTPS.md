# HTTP vs HTTPS

> [과거에 정리한 글](https://chloe-codes1.gitbook.io/til/server/server-101/https_and_ssl)
>

<br>

### HTTP 란?

Hypertext Transfrer Protocol의 약자로, Hypertext인 HTML을 전송하기 위한 통신 규약을 의미

<br>

### HTTPS 란?

- HTTPS 의 마지막 `S` 는 **Over Secure Socket Layer** 의 약자로 Secure라는 말에서 알 수 있듯이 **보안이 강화된** HTTP 라는 것을 짐작할 수 있다
- HTTP 는 암호화되지 않은 방법으로 데이터를 전송하기 때문에 Server와 client가 주고 받는 메시지를 감청하는 것이 매우 쉽다
  - 안전하지 않다!
    - ex) 로그인을 위해 Server로 비밀번호를 전송하거나 중요한 기밀 문서를 열람하는 과정에서 악의적인 **감청**이나 데이터의 **변조**등이 일어날 수 있다는 것!
  - 그래서 이를 보완한 것이 **HTTPS** 다!

<br>

### HTTPS 와 SSL (Secure Socket Layer)

- HTTPS 와 SSL을 같은 의미로 이해하고 있는 경우가 많다 (과거의 나...)
  - 이것은 마치 인터넷과 Web을 같은 의미로 이해하는 것과 같다!
- `Why?`
  - Web이 인터넷 위에서 돌아가는 서비스 중 하나인 것 처럼
  - HTTPS 도 SSL Protocol 위에서 돌아가는 Protocol이다!
- HTTP가 SSL 위에서 동작하면 HTTPS가 되는 것이다!

<br>

### SSL 과 TLS

- 이 둘은 사실 같은말이다!
  - Netscape에서 **SSL**이 발명되었고, 이것이 점차 폭넓게 사용되다가 표준화 기구인 `IETF` 의 관리로 변경되면서 **TLS**라는 이름으로 바뀌었다
  - **TLS** 1.0 은 **SSL** 3.0을 계승한다
  - 그래서 정식 명칭은 **TLS**이다
    - but, **TLS**라는 이름보다 **SSL**이라는 이름이 훨씬 많이 사용된다!

<br>

### SSL에서 사용하는 암호화의 종류

- `대칭키 방식 (Symmetric-key algorithm)`
  - **동일한 키**로 `암호화`와 `복호화`를 같이 할 수 있는 방식의 암호화 기법
    - `암호화`를 하는 쪽과 `복호화`를 하는 쪽이 동일한 Key를 가지고 있다!
  - 단점
    - 암호를 주고 받는 사람들 사이에 대칭키를 전달하는 것이 어렵다
      - 대칭키가 **유출**되면 키를 획득한 공격자는 암호의 내용을 **복호화** 할 수 있기 때문에 암호가 무용지물이 된다...!
      - 이러한 문제를 `key distribution problem`이라고 한다.
- `공개키/비대칭키 방식 (Public-key/asymmetric cryptography)`
  - 대칭키가 가지고 있는 `key distribution problem`을 개선하기 위해 등장한 암호화 방식
  - 대칭키와는 다르게 Key가 두 개 있다
    - `A` key로 암호화를 하면 `B` key로 복호화 할 수 있고,
    - `B` key로 암호화하면 `A` key로 복호화 할 수 있는 방식
  - 두 개의 키 중 하나를 **비공개 키 (private key, 개인키, 비밀키)** 로 하고,
    - 나머지를 **공개키 (public key)** 로 지정한다!
  - 공개키가 유출된다고해도 비공개키를 모르면 정보를 복호화 할 수 없기 때문에 **안전** 하다!
    - why?
      - 공개키로는 암호화는 할 수 있지만 복호화는 할 수 없기 때문!
