# Elastic IP

> Elastic IP 자세-히 알아보기 실무 ver.

<br>

<br>

### Elastic IP == 고정 IP

- EC2 Instance의 `Elastic IP` 값은 비어 있고, `Public IPv4` 값은 채워져 있을 때
  - Instance가 stopn & start 할 때 IP가 바뀐다
    - **Elasitc IP**에 값을 할당 받으면 이러한 현상 없이 고정된 IP를 사용할 수 있다!
      - but, 기존에 할당받은 `Public IP`를 바탕으로 **Elastic IP**를 생성할 수는 없다
        - 애초에 처음 instance를 생성할 때 **Elastic IP**를 설정하는 것!

<br>

<br>

### Elasic IP Charges

- Elasic IP가 어딘가에 할당되어 있지 않으면 AWS에서 과금을 시킨다!
  - EC2에 연결되어 있으면 과금하지 안흔다
    - why?
      - "IPv4는 유한 자원이기 때문에 사용하지 않으면 아껴쓰라는 의미로 과금한다" 는 AWS의 의견이 있다
        - but, EC2에 연결되어 있으면 그만큼의 비용을 어짜피 내는 것이므로 과금하지 않는 것 같다

<br>

<br>

### Elastic IP address limit

- 한 계정당 소유할 수 있는 **Elastic IP**의 개수는 제한적이다
  - IPv4는 유한 자원이기 때문에 너무 많이 요청하면 AWS에서 제공하지 않는다
  - Default로는 region 당 5개의 **Elastic IP**를 소유할 수 있다

<br>

<br>

<br>

`+`

#### Public IP

- Public subnet에 있다고 꼭 public IP를 가져가야 하는 것은 아니다!
  - *하지만 public 연결이 필요해서 public subnet에 생성했겠지?*
- EC2가 Public subnet에 존재하는데 Public IP가 없으면
  - 외부에서 내부로 접근 불가
  - 내부에서 외부로도 접근 불가
- Private subnet에 존재하는데 Public IP가 없어도 외부로 접근 가능한 이유는 NAT Public IP를 타고 나가기 때문이다
- Public IP 가 없어도 ssh로 접근이 되는 이유
  - 방화벽 설정이 되어 있어서이다
