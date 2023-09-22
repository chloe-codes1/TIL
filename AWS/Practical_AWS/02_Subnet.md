# Subnet

> Subnet 자세-히 알아보기 실무 ver.

<br>

<br>

### Subnet이란?

- VPC의 IP 주소 범위
  - VPC 안에서 구간을 나눠주는 것
- AWS의 VPC는 Subnet 없이 동작할 수 없다!

<br>

### Subnet 이름

- 개념적으로 나눈 것
  - public
  - private
- 꼭 subnet의 이름으로 `public` 이나 `private`을 쓰지 않아도 된다
- DB subnet을 별도로 나누는 것은 취향차이다

<br>

### Subnet의 CIDR Block

- Subnet도 CIDR block을 지정해야 한다
- Subnet끼리 CIDR이 **충돌**나면 안된다
- Subnet CIDR은 **VPC 범위**를 벗어나면 안된다
  - IP의 최대 제약은 VPC size니까!
- VPC 내에 Subnet으로 땅따먹기 하는 것이다
  - 만약, Subnet의 IP가 부족하면 땅따먹기 빈 공간에 subnet을 하나 더 만들면 된다!
    - but, resource 생성 시 **subnet option** 이 두 가지가 되므로 어떤 subnet을 선택할지 고민 될 것이다..
      - 중간에 추가로 subnet을 만들지 말고 처음에 잘 설계하자!
  - Subnet을 VPC 빈공간에 추가로 생성할 수는 있지만, Subnet 두 개를 **합칠 수는 없다**
