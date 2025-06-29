# Route 53

> Route 53  자세-히 알아보기 실무 ver.

<br>

<br>

### What is Amzaon Route 53?

: AWS가 제공하는 DNS (Domain Name Service)

<br>

<br>

### Supported DNS record types

: [AWS docs](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/ResourceRecordTypes.html)를 참고하면 자세히 정리되어 있지만 자주 쓰는 것을 간단히 정리해보기

- `A record type`
  - IPv4 address
- `AAAA record type`
  - IPv6 address
- `CNAME record type`
  - domain 주소가 다른 주소를 바라볼 때
- `MX record type`
  - 말 그대로 mail server
- `SPF record type`
  - mail 관련
- `TXT record type`
  - 조회하면 `"` 로 감싸진 1개 이상의 string을 return 한다
  - Usage
    - reverse dns lookup
    - auth
      - **domain 소유주가 맞는지 인증하는 방법**
        1. domain owner에게 메일 보내기
        - 내 domain에 mail service (MX record type, etc.)를 연결하고 메일을 받는 방법으로 인증한다
          - 이 방법은 조금 귀찮아서 아래의 `TXT record type`을 사용한다
        2. `TXT record` 에 token을 입력하도록 하기
           - 내가 보낸 값 (token)을 입력하게 하여 인증
             - 이 방법을 요즘 더 선호한다

<br>

<br>

### alias

- Route 53에만 있는 기능
- AWS Service를 연결할 때 사용한다
- LB는 `CNAME`으로 연결하면 안된다
  - why?
    - LB domain이 계속 바뀌기 때문이다
    - but, 이건 Cloud 환경이라서 그런 것!
  - ALB는 Instances로 구성되어 있다
    - Instance의 IP는 **2개 + a**이다
      - why? traffic이 많으면 더 많은 IP를 할당하기 때문이다
    - 그래서 다수의 IP를 domain 주소에 mapping해서 관리한다

<br>

#### 왜 alias를 사용할까?

- 만약 `CNAME`을 사용하면
  - 접속하는 client 입장에서 해당 domain 정보를 물어보면 최종 목적지 정보를 물어보고 다시 물어봐야 한다!
    - why?
      - `CNAME`은 연결되어 있으면 타고 타고 들어가다가 종단 **record**가 나온다
        - 그게 바로 IP
- `CNAME`이 아닌 `alias`를 사용하는 이유
  - **편리함**
    - `CNAME` 은 여러번 물어보기 때문에 불편한데 `alias`를 사용하면 편안하다
      - how?
        - AWS service들은 다 자기 자원이니까 **Route 53**이 대신 조회해서 최종 IP를 한번에 조회해준다
  - **성능**
    - Client 입장에서 성능이 약간 좋아진다
  - **비용**
    - Route 53 비용 과금 체계
      - 조회 시 A record < CNAME
        - CNAME이 더 비싸다
        - alias 비용 == A record

<br>

<br>

### Route 53 Tips

- 한 개의 domain 주소에 대해 여러개의 record type을 가질 수 있다
  - 같은 domain에 또 다른 record 추가 가능!
- 같은 record type에 대해 record 추가를 원할 시 multiline으로 등록 가능하다
  - 두 개를 등록하지 말자!
