# VPC Endpoints

> VPC Endpoints 자세-히 알아보기 실무 ver.

<br>

<br>

### Before Getting Started

#### What are Scopes?

- `Global Scope`
  - 말 그대로 global한 scope
  - ex)
    - IAM
- `AZ Scope`
  - 만들면 우리 VPC의 IP를 소모하는 것들
  - ex)
    - ENI
    - ELB
    - ElastiCache
- `Region Scope`
  - 만든다고 우리 VPC의 IP를 소모하지 않는 resource들의 scope
    - 완전 관리형 services
  - **Internet 통신**을 하게 된다
    - why?
      - 우리 VPC 밖에 있으니까!
    - 그렇기 때문에 **Outbound Traffic**, **보안/네트워크 구성** 등을 고려해야 한다
      - 이때 사용하는 service가 바로 `VPC Endpoints`다!!
  - ex)
    - SQS
    - Kinesis
    - S3
      - AWS Console에서는 **Global**이라고 나온다
        - S3는 **3중 복제**가 기본이다
          - 즉, 예전에 Seoul Region에 AZ가 a, c zone 두 개 였을 때도 **hidden AZ**가 있던 것이다!
          - 그래서 3중 복제가 기본인 S3 service를 제공할 수 있었다

<br>

<br>

### What are VPC Endpoints?

- VPC 내부에서 통신하는 것 처럼 일종의 통로를 만들어 주는 service
  - 만약 이렇게 통로를 만들면, 외부 통신 설정을 하지 않은 EC2여도 Endpoint로 나갈 수 있다!

<br>

<br>

### Endpoint Types

#### 1. Gateway Type

- 다른 쪽으로 traffic을 흘려준다
- 우리 VPC IP를 소모하되,
  - SG등 방화벽으로 접근을 제어하지 않는다
- 규칙을 아래 두 가지에서만 탄다
  1. `Routing Table`
  2. `ACL`
     - ACL은 Subnet에 종속적이지 않다!
       - 즉, AZ의 영향을 받지 않는다
     - 요청자 Destination만 맞으면 해당 Endpoint로 보내준다
- 각 VPC별로 resource (ex. S3)마다 한 개씩 필요하다
- ex)
  - S3
  - DynamoDB
- **Gateway Type의 장점**
  - 비용
    - `내부 통신` 비용이 나가므로 경제적이다
  - 보안
    - `내부 통신`이므로 외부 통신보다 고려할 사항이 줄어든다

<br>

#### 2. Interface Type

- Interface는 `Network Interface`를 말한다
  - **Network Interface Card**라고 생각하면 편하다
- 우리 VPC의 IP를 소모한다
  - SG등 방화벽으로 접근 제어가 가능하다
    - `NAT Gateway`도 Interface Type이다!
- Interface Type은 Routing Table을 설정하지 않는다
