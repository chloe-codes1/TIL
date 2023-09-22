# Find EC2 Instance by Domain Name

> 해당 Domain 이 어떤 EC2 Instance 인지 모를 때 찾는 방법을 공유해요

<br>

<br>

### 1. Route 53 Console 이동

- **Hosted zones**
  - url 검색
  - `Value/Route traffic to`  에서 주소 복사

<br>

### 2. EC2 Console 이동

- **Load Balancers**
  - 위에서 복사한 url에서
    - Internal 앞부분과 맨 뒤에 . 지우고 검색
  - `Listeners` tab 선택
    - Default: forwarding to ~~~~~~ 에서 ~~~ 를 클릭
- **Target groups**
  - instance 찾았다!!!!
