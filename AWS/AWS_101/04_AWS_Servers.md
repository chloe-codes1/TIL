# AWS Servers

<br>

#### Contents

- Server Architecture
- AWS Server service
- Amazon EC2 (Elastic Compute Cloud)

<br>

#### Useful Informations

1. AWS Server service의 AZ (= Availability Zone )은 하나 이상의 data center로 구성되며, 독립된 장애 영역으로 설계된다
2. AWS region은 2개 이상의 AZ를 포함한다

<br>

<br>

## Server Architecture

<br>

### Web Server Architecture



![aws web server architecture 이미지 검색결과](https://tech.cloud.nongshim.co.kr/wp-content/uploads/2018/10/2-1-1-1024x688.png)



<br>

<br>

## AWS Server Service

<br>

### Availability Zone(AZ)

- AWS의 `data center`는 `가용 영역(AZ)` 내에 편성
- 각 가용 영역은 하나 이상의 data center로 구성
- 하나의 data center가 2개의 가용 영역에 포함될 수는 없음
- 각 가용 영역은 독립된 장애 영역으로 설계
- 가용 영역은 일반적인 대도시 region 내에서 물리적으로 격리되어 있으며, 별도의 무정전 전원 공급 장치와 현장 backup 발전 시설 외에도 독립적인 utility의 서로 다른 grid를 통해 전력을 공급받음으로써 단일 장애 지점이 더욱 줄어들게 됨
- 사용자는 시스템이 상주할 가용 영역을 선택해야함
- 시스템은 여러 가용 영역에 걸쳐 확장 가능하며 재해가 발생하는 경우, 임시 또는 장기 가용 영역 장애를 극복 할 수 있도록 시스템을 설계 해야함
- 여러개의 가용 영역에 application을 분산하면 자연 재해나 시스템 장애 등 대부분의 장애 상황ㅇ에서도 복원력 유지 가능

<br>

### Region

- Availability Zone은 다시 region으로 그룹화

- 각 AWS Region은 *2개 이상의 Availability Zone*을 포함

- 특정 region에 data를 저장하는 경우, 해당 region 내에서만 data가 복제됨

- AWS는 사용자가 data를 저장한 *region 외부로 data를 이동하지 않음*

  -> 비즈니스에서 이를 필요로 하는 경우, 여러 region에 걸쳐 data를 복제하는 작업은 사용자의 책임

- AWS에서는 각 region이 위치한 국가 및 지역에 대한 정보를 제공하며, 규정 준수와 network 지연 시간 요구 사항에 따라 data를 저장할 region을 선택하는 것은 사용자의 책임

- region 간 모든 통신은 `Public Internet Infra` 를 통해 이루어지므로, 민감한 data를 보호하기 위해 **암호화 방법**을 사용할 필요가 있음

- 사용 가능한 AWS 제품과 service는 region에 따라 달라지므로, 사용자는 해당 region에서 사용한 services를 잘 확인할 필요가 있음

<br>

### Virtual Private Cloud (VPC)

- 사용자의 AWS 계정 전용 virtual network
- AWS Cloud에서 다른 virtual network와 논리적으로 분리됨
- Amazon EC2 instance와 같은 AWS resource를 VPC에서 실행할 수 있는 `cloud`와 `network` 환경
- 다양한 resource를 시작하는 장소이며, 사용자 환경 및 resource 상호 격리에 대한 탁월한 제어 기능을 제공하도록 설계됨
- 각 VPC는 region 내에 존재하며 VPC 내에 있는 resource는 해당 region 외부에 존재할 수 없음
  - but, 같은 region 내에 다른 가용 영역이 있는 resource는 같은 VPC에 존재할 수 있음
- Internet gateway, NAT, firewall proxy를 사용하지 않고 VPC endpoint를 통해 AWS Service에 비공개로 연결 가능
- 사용 가능한 서비스에는 S3, DynamoDB, Kinesis Streams, Service Catalog, Ec2 System Manager(SSM), Elastic Load Balacing(ELB) API, Amazon Elastic Compute CLoud(EC2) API 및 SNS가 포함됨!

<br>

### Subnet (서브넷)

- VPC와 IP의 주소 범위
- 지정된 subnet으로 AWS resource를 시작 가능
- 인터넷에 연결되어야 하는 resource에는 `public subnet`을 사용
- 인터넷에 연결되지 않는 resource에는 `private subnet` 을 사용
  - ex) Network Address Translation(NAT)을 사용하여 인터넷에서 주소로 직접 access하지 못하게 할 instance에 대해서는 private subnet 사용
  - Private subnet에 있는 instance는 public subnet의 NAT gateway를 통해 traffic을 outing 하여 private IP address를 노출하지 않고 Internet에 access 가능

<br>

### Elastic Compute Cloud (EC2)

- AWS Service의 핵심

- AWS cloud에서 확장 가능한 computing 제공

- EC2를 사용하면 hardware에 선투자 할 필요가 없어 더 빠르게 application을 개발하고 배포 가능

- EC2를 통해 원하는 만큼 virtual server를 구축하고, 보안 및 네트워크 구성과 storage 관리 가능

- EC2는 요건이나 갑작스러운 접속 증가 등 변동사항에 따라 확장하거나 축소할 수 있어 traffic 예층 필요성 감소

- EC2가 제공하는 기능들
  1. `Virtual Computing Environment`	
     -  컴퓨터 및 메모리 기능에 따라 목적에 맞는 instance 생성 
  2. `Amazon Machine Image (AMI)`  :Server에 필요한 OS와 여러 software들이 적절히 구성된 상태로  제공되는 template으로 instance 생성이 가능instance를 위한 CPU, 메모리, storage , networking 용량의 여러 가지 구성을 제공
  3. `Instance Store Volume`
     - Instance will be deleted when you shutdown since it's a storage volume for saving temporary data
  4. `Amazon Elastic Block Store (Amazon EBS)`
     - ESB Volume을 사용해 Permanent Storage Volume에 data 저장 가능
  5. `Security Group` 
     - Instance에 연결할 수 있는 Protocol, Port, Source IP 범위를 지정하는 Firewall 기능 제공
  6. `Elastic IP (EIP)`
     - Fixed IPv4 address for Dynamic Cloud Computing
  7. `Tag`
     - 사용자가 생성하여 Amazon EC2 resource에 할당할  수 있는 meta data

  

  <br>

### Relational Database Service (RDS)

- Cloud에서 RDBMS를 더욱 쉽게 설정, 운영 및 확장 할 수 있도록 지원하는 web service
  - 산업 표준 관계형 데이터베이스를 위한 경제적이고 크기 조절이 가능한 용량을 제공하고 공통 데이터베이스 관리 작업을 관리
- Amazon RDS를 사용하면 CPU, memory, storage 및 IOPS(Input/Output Operations Per Second) 가 따로 분할되므로 독립적으로 확장 가능
- CPU가 더 많이 필요하거나 IOPS가 더 적게 필요하거나 Storage가 더 많이 필요할 경우 쉽게 할당이 가능하다
- RDS manages backup, software patch, automatic error detection & recovery
- MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL Server 그리고 MySQL 호환 `Amazon Aurora DB engine` 등 익순한 database 제품을 사용 가능
  - Package security 외에도 AWS Identity, Access Management(IAM)을 사용해 사용자 및 권한을 정의하는 방법으로 RDS database에 access 하 ㄹ수 있는 사용자를 제어 가능 

<br>

### Elastic Load Balancing  (ELB)

- 들어오는 application traffic 을 Amazon EC2 instance, container, IP address와 같은 여러 대상에 자동으로 분산
- 단일 AZ(Availability Zone)  or 다중 AZ에서 다양한 application 부하를 처리하므로 내결함성과 가용성이 향상됨 
- **3 Load Balancers in ELB**
  - ELB 에는 세 가지 Load Balancer가 존재하는데 모두 application의 내결함성에 필요한 고가용성, 자동 확장/축소, 강력한 보안 기능 제공
    1. `Application Load Balancer`
       - Application Layer 7에서 작동함
       - 요청 content를 기반으로 VPC 내의 대상으로 traffic routing
       - Layer 7 HTTP/HTTPS application을 Load balancing 하고 SSL/TLS 암호 및 protocol이 사용되도록하여 application의 보안을 개선
    2. `Network Load Balancer`
    3. `Class Load Balancer`
    4. 

- d

