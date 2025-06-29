# Protocol

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

### Before getting started

- 규정/규약과 관련된 내용을 언급할 때 **protocol** 이라는 용어를 사용한다
- 네트워크에서도 **통신할 때의 규약**을 말할 때 protocol 이라는 용어를 사용한다

<br>

<br>

### Protocol

- **물리적 측면**
  - data 전송 매체, 신호 규약, 회선 규격 등
  - `Ethernet`이 널리 쓰인다
- **논리적 측면**
  - 장치들끼리 통신하기 위한 protocol 규격
  - `TCP/IP`가 널리 쓰인다

<br>

#### bit 기반 protocol

- `protocol`은 적은 data를 이용해 효율적으로 사용하기 위해 대부분 **2진수 bit** 기반으로 만들어졌다
  - 최소한의 bit로 내용을 전송하기 위해 까다롭게 약속하고 그 약속을 철저히 지켜야 통신할 수 있었다

<br>

#### Application level protocol

- `application level protocol`은 bit 기반이 아닌 문자 기반 protocol이 많이 사용되고 있다
  - **HTTP**와 **SMPT**와 같은 protocol이 대표적이다
  - bit로 message를 전달하지 않고 문자 자체를 이용해 **header**, **header 값**, **data**를 표현하고 전달한다
  - 효율성은 bit 기반 protocol 보다 떨어지지만, 문자로 정의되어 있어 header 정의가 자유롭고 **확장이 가능**하다

<br>

#### Protocol stack

- 일반적으로 `TCP/IP`는 protocol이 아닌 **protocol stack**이라고 부른다

  - **TCP**와 **IP**는 별도의 layer에서 동작하는 protocol 이지만, 함께 사용하고 있는데 이러한 protocol 묶음을 protocol stack이라 부른다
  - **TCP/IP** protocol stack에는 TCP, IP 뿐만 아니라 `UTP`, `ICMP`, `ARP`, `HTTP`, `SMTP`, `FTP`와 같은 매우 다양한**application layer protocol**이 있다

- TCP/IP protocol stack은 아래의 4개 부분으로 나뉜다

  - **Pysical layer**

    - Ethernet

  - **Network layer**

    - data가 목적지에 찾아가도록 해준다

  - **Transport layer**

    - 잘린 `packet`을 data 형태로 잘 조합하도록 도와준다

  - **application layer**
