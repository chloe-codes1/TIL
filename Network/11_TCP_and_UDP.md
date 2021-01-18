# TCP / UDP

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

- 2계층과 3계층은 목적지를 정확히 찾아가기 위한 **주소 제공**이 목적이었지만, 4계층에서 동작하는 protocol은 만들어진 목적이 2, 3 계층과 조금 다르다
  - 목적지 단말 안에서 동작하는 여러 application process 중 **통신해야 할 목적지 process**를 정확히 찾아가고,
  - packet 순서가 바뀌지 않도록 잘 **조합**해 
  - **원래 data**를 잘 만들어내기 위한 역할을 한다

<br>

## 1. Layer 4 Protocol (TCP, UDP) and Service Port

- Data를 보내고 받는 Encapsulation, Decapsulation 과정에 각 계층에서 정의하는 header가 추가되고, 여러가지 정보가 들어간다
  - 다양한 정보 중 가장 중요한 두 가지 정보는 아래와 같다
    1. 각 계층에서 정의하는 정보
       - 수신 측의 동일 계층에서 사용하기 위한 정보
    2. 상위 protocol 지시자 정보
       - Decapsulation 과정에서 상위 계층의 protocol이나 process를 정확히 찾아가기 위한 목적으로 사용
- `TCP/IP Protocol Stack`에서 4계층은 TCP와 UDP가 담당한다
  - 4계층의 목적은 application에서 사용하는 process를 정확히 찾아가고, data를 분할한 `packet`을 잘 쪼개 보내고 잘 조립하는 것이다
  - packet을 분할하고 조립하기 위해 **Sequence Number**와 **ACK Number**를 사용한다

- `TCP/IP Protocol Stack`에서 상위 protocol 지시자는 **port**번호이다
  - 4계층 protocol 지시자인 port 번호는 **출발지와 목적지를 구분해 처리**해야 한다

<br>

#### Well Known Port

- HTTP TCP 80, HTTPS TCP 443, SMTP TCP 25와 같이 잘 알려진 Port를  **Well known** port 라고 한다
- 이 port들은 이미 인터넷 주소 할당 기구인 **IANA (Internet Assgined Numbers Authority)**에 등록되고 **1023**번 이하의 port 번호를 사용한다
- 다양한 application에 port 번호를 할당하기 위해 **Registered Port** 범위를 사용한다
  - `1024 ~ 49151` 의 범위이며,port 번호를 할당받기 위해 신청하면 **IANA**에 등록되어 관리된다
    - but, 공식 번호와 비공식 번호가 혼재되어 있고, 사설 port 번호로 사용되기도 한다
- **동적**, **사설**, **임시** port 의 범위는 `49152 ~ 65535` 이다
  - 이 범위의 port 번호는 IANA에 등록되어 사용되지 않는다
  - 이 port 번호는 자동으로 할당되거나, 사설 용도로 할당되고, client의 임시 port 번호로 사용된다!
- [IANA가 관리하는 Port 확인하기](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml) 

<br>

<br>