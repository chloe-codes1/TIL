# AWS Online Cloud Clinic #1 - 3/4

<br>

<br>

### 협업 tools

> Coronavirus로 인한 재택근무 활성화로 협업 tool에 대한 관심이 높아짐

- 잔디
- notion
- Trello

<br>

<br>

## AWS Seoul Region Newly Released Services

<br>

### 1. EC2 다중 Instance에 연결 가능한 provisioning IOPS `io1` EBS Volume 출시

- EFS는 비용이 비싼 경향이 있어서 망설여질텐데, 다중 instance에 연결 가능한 EBS Volume이 출시되어서 활용하기 좋을 것 같다

<br>

### 2.  AWS Compute Optimizer

- EC2에 다양한 instance type이 있는데 내 application에 맞는 instance를 고르는 것이 쉬운 일이 아님
- 그것을 최적화 할 수 있도록 도와주는게 AWS Compute Optimizer!
- 사용자의 가상 서버 workload를 분석해서 어떤 option을 사용해야 비용을 절감할 수 있는지 알려줌

<br>

### 3. AWS Saving Plans

1. Compute Saving Plans
   - Region, Instance family, size, tenancy, OS에 상관없이 적용 가능
   - EC2 instance, AWS Fargate, AWS Lambda service 사용량에 적용 가능
   - 시간당 약정 설정 가능
2. EC2 Saving Plans
   - Size, tenancy, OS에 상관없이 commit된 EC2 Family 및 Region 내 instance 사용량에 적용 가능

<br>

<br>

## QnA

<br>

- Q1) Amazon athena의 computing power 제한이 있나요?
  - Athena
    - Serverless data query engine
    - Open Source
  - Computing power 제한은 없음
  - Best practice AWS Blog에 나와 있음
    - ex) 압축하기 etc.

<br>

- Q2) 곧 영국 및 독일 사용자를 위한 웹서비스를 구축 예정하고 있습니다. EC2는 당연히 해당리전에 있어야 하는데 원래 미국 리전에서 관리하는 RDS 도 똑같이 영국과 독일 리전에 넣어야할까요? 분리하는게 맞을 듯 한데 관리 때문에 미국 리전의 RDS을 그냥 쓰자는 내부 의견도 있습니다
  - 기본적으로는 server와 db server를 같은 region에 두는 것이 일반적
  - 유럽 내 서비스의 경우 개인정보 저장 이슈 (GDPR)가 있을 수 있으니 유럽 내 region에 RDS를 두는것을 권장
  - Amazon Aurora는 global database 기능이 추가되는 등 문제를 보완하기 위한 서비스들이 나오고는 있지, latency 문제, 보안 issue를 고려해서 선택하는게 좋을 것.

<br>

- Q3) DocumentDB를 Seoul region에서 사용하고 있는데 global service 때문에 다른 region으로 확장 할 수 있을까요?
  - Documentdb의 snapshot은 아직까지 타 region으로 복사가 되지 않음
  - Amazon DynamoDB는 global table cross과 regional replication 제공
  - Amazon Aurora도 global data service 제공
  - 그 외 db들은 global service 지원이 어려우므로 참고

<br>

<br>

## Tips

- AWS site 내의 FAQ 참고하기
  - 강의, 책보다 site에 정리된 자료가 더 많고 정확하다
- 책추천
  - 배워서 바로 쓰는 14가지 AWS 구축 패턴 (AWSKRUG Machine Learning Study 주최자 정도현님이 번역하심! 사야겠다)
  - <https://brunch.co.kr/@topasvga/666> 에 AWS 관련 추천도서 정리되어 있으니 참고
