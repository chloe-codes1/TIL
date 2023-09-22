# AWS HA Load Balancing

<br>

#### Contents

- Amazon Elastic Load Balancing
- Amazon Auto Scaling
- ELB 및 Auto Scaling 구축하기

<br>

#### Useful Informations

1. Amazon Elastic Load Balancing은 확장성, 성능 및 보안을 보장하여 application의 내결함성을 확보할 수 있다

   - ELB는 단일 가용 영역 또는 여러 가용 영역에서 다양한 application의 부하를 처리할 수 있다

2. ELB는 application의 요구 사항에 따라 적절한 Load Balancer를 선택할 수 있다

   - 유연한 application 관리가 필요한 경우 `Application Load Balancer`를 사용하는 것이 좋음
   - Application에 탁월한 성능 및 고정 IP가 필요한 경우 `Network Load Balancer`를 사용하는 것이 좋음
   - 기존 application이 EC2-Classic Network 내에 구축되어 있는 경우 `Classic Load Balancer`를 사용해야 함

<br>

<br>

## Amazon Elastic Load Balancing

> 확장성, 성능 및 보안을  보장하여 application의 내결함성 확보

<br>

- Elastic Load Balancing은 들어오는 application traffic을 Amazon EC2 instance, container, IP address, Lambda function과 같은 여러 대상에 자동으로 분산시킴
- ELB는 단일 가용 영역 또는 여러 가용 영역에서 다양한 application 부하를 처리할 수 있음
- ELB가 제공하는 세 가지 Load Balancer는 모두 application의 `내결함성`에 필요한 **HA (High Availability)**, **자동 확장/축소**, **강력한 보안**을 갖추고 있음

<br>

### Amazon Elastic Load Balancing 사례

<br>

#### 1. Application 내결함성 향상

- ELB는 대상 (Amazon EC2 instance, container, IP address, Lambda function)과 여러 가용 영역에 traffic을 자동으로 분산시키는 동시에 정상 상태인 대상만 traffic을 수신하도록 함으로써 application의 내결함성을 제공함
- 단일 가용 영역의 모든 대상이 정상 상태가 아닐 경우, ELB는 다른 가용 영역에 있는 정상 상태인 대상으로 traffic을 routing 함
- 대상이 정상 상태로 복구되면 Load Balancing은 자동으로 원래 대상으로 재개됨

<br>

#### 2. Container식 application의 자동 Load Balancing

- Elastic Load Balancing의 향상된 Container 지원을 통해 동일한 Amazon EC2 instance의 여러 port에서 Load Balancing이 가능함
- 완전 관리형 container 상품을 제공하는 `Amazon EC2 Container Service (ECS)` 와의 완벽한 통합도 활용할 수 있음
- Service를 Load Balancer에 등록하기만 하면 ECS는 `Docker COntainer` 의 등록 및 등록 취소를 투명하게 관리함
- Load Balancer는 port를 자동으로 탐지하여 동적으로 스스로를 재구성함

<br>

#### 3. Application 자동 조정

- Elastic Load Balancing은 고객의 수요에 맞춰 application이 확장/축소 할 수 있다는 확신을 제공함
- Amazon EC2 instance 중 하나의 지연 시간이 사전 정의된 임계치를 초과하면 Amazon Ec2 instance의 `Auto Scaling` 을 trigger 하는 기능을 통해 application이 항상 다음 고객 요청을 처리할 준비를 갖추게 됨

<br>

#### 4. Amazon Virtual Private Cloud (Amazon VPC)에서의 Elastic Load Balancing 사용

- Elastic Load Balancing을 사용하면 손쉽게 VPC로 가는 인터넷 연결 진입점을 만들거나 VPC 내 application tier 간에 요청 **traffic을 routing**을  할 수 있음
- Load Balancer에 **보안 그룹**을 할당해 허용된 source 목록에 대해 어떤 port를 열 것인지 제어할 수 있음
- Elastic Load Balancing은 VPC와 통합되므로 기존의 모든 Network `ACL (Access Control List)`와 `routing table`이 추가 Network 제어를 계속 제공함
- VPC에서 Load Balancer를 만들 때 Load Balancer를 **Internet에 연결할지** (이게 기본값) or **내부에서 사용할지** 지정 가능
  - 내부에서 사용하는 것을 선택하면 Load Balancer에 연결하기 위한 Internet gateway가 필요하지 않으며 Load Balancer의 `DNS(Domain Name System) record`에서 Load Balancer의 **사설 IP 주소**가 사용됨

<br>

#### 5. Elastic Load Balancing을 사용한 Hybrid Load Balancing

- Elastic Load Balancing은 같은 Load Balancer를 사용하여 AWS와 On-premise resource 전체에 Load Balancing을 할 수 있는 기능을 제공함
- ex) AWS와 On-premise resource 모두에 application traffic을 분산시켜야 하는 경우, 모든 resource를 같은 대상 그룹에 등록하고 해당 대상 그룹을 Load Balancer에 연결하면 됨
- AWS에 하나의 Load Balancer와 On-premise resource에 다른 Load Balancer, 즉 두 개의 Load Balancer를 사용하여 AWS 와 On-premise resource 전체에서 DNS 기반 **가중치 Load Balancing**을 사용할 수도 있음
- `Hybrid Load Balancing`을 사용하여 하나는 VPC에 있고 다른 하나는 On-premise 위치에 있는 별개의 application을 활용할 수도 있음
- VPC 대상을 하나의 대상 그룹에 넣고 On-premise 대상을 또 다른 대상 그룹에 넣은 후 `content based routing` 을 사용하여 traffic을 각 대상 그룹으로 routing 할 수 있음

<br>

#### 6. HTTP(S)를 통해 Lambda function 호출

- Elastic Load Balancing은 HTTP(S)요청 서비스를 위한 `Lambda function` 호출을 지원함
  - 사용자는 web browser를 포함하여 HTTP client에서 `serverless application`에 access 할 수 있음
- Lambda function을 대상으로 등록하고 Application Load Balancer의 content based routing 규칙에 대한 지원을 활용하여 요청을 다른 lambda function으로 routing 할 수 있음
- Server or Serverless application을 사용하는 application에 대해 `Application Load Balancer`를 **공통 HTTP End Point**로 사용할 수 있음
- Lambda function을 사용하여 web site 전체를 구축하거나 EC2 instance, container, On-premise server 및 Lambda function을 결합하여 application을 만들 수 있음

<br><br>

### Amazon Elastic Load Balancing 기능

<br>

1. #### 고가용성

   : ELB는 traffic을 단일 가용 영역 또는 여러 가용 영역에 있는 여러 대상(Amazon EC2 instance, container, IP address) 에 자동으로 분산함

2. #### 상태 확인

   : ELB는 비정상 대상을 감지하고, 해당 대상으로 traffic 전송을 중단한 다음, 나머지 정상 대상으로 load를 분산 할 수 있음

3. #### 보안 기능

   - Amazon Virtual Private Cloud(VPC)를 사용하면 Load Balancer와 연결된 보안 그룹을 생성 및 관리하여 추가 네트워킹 및 보안 option을 제공할 수 있음
   - 인터넷을 사용하지 않고 내부 Load Balancer를 생성 할 수도 있음

4. #### `TLS (Transport Layer Security)` 종료

   : ELB는 통합 인증서 관리 및 `SSL (Secure Socket Layer)` 와 `TLS` 복호화를 지원하므로 유연하게 Load Balancer의 SSL 설정을 중앙에서 관리하고 application의 CPU 집약적인 작업을 줄일 수 있음

5. #### **Layer 4** or **Layer 7** Load Balancing

   : Layer 7 전용 기능에 대해 HTTP/HTTPS application을 Load Balancing 하거나 `TCP (Transmission Control Protocol)` or `UDP (User Datagram Protocol)` 를 활용하는 application에 대해 엄격한 Layer 4 balancing을 사용할 수 있음

6. #### Monitoring

   : ELB는 application 성능을 실시간으로 monitoring 할 수 있도록 **Amazon CloudWatch** 지표 및 요청 추적과 통합을 제공함

<br>

<br>

### ELB 제품

> Application 요구 사항에 따라 적절한 Load Balancer를 선택 할 수 있음

- #### `Application Load Balancer`

  :  유연한 application 관리가 필요한 경우

  - 요청 수준 (Layer 7)에서 작동하는 Application Load Balancer는 요청의 content에 따라 EC2 instance, container, IP address, Lambda function 등의 대상으로 traffic을 routing 함

  - HTTP 및 HTTPS traffic의 고급 Load Balancing에 적합한 Application Load Balancer는 **Micro service**와 **container based application**을 비롯한 최신 application architecture 전달을 위한 고급 요청 라우팅 기능을 제공함

    - Application Load Balancer는 client와 load balancer 간 HTTPS 종료를 지원함
    - AWS Identity and Access Management(IAM) 및 AWS Certificate Manager의 사전 정의된 보안 정책을 통해 SSL 인증서 관리도 제공함

  - Application Load Balancer는 항상 최신 **SSL/TLS 암호** 및 protocol이 사용되도록 하여 application의 보안을 간소화하고 개선함

  - **SNI (서버 이름 표시)**

    - SNI는 TLS handshake 시작 시 client가 연결할 host 이름을 표시하는 TLS protocol에 대한 확장 프로그램이다
    - Load Balancer는 같은 보안 listener를 통해 여러 개의 인증서를 제시할 수 있으므로 단일 보안 listener를 사용하여 여러개의 보안 web site를 지원하도록 할 수 있음
    - Application Load Balancer가 SNI를 사용한 **스마트 인증서 선택 알고리즘**을 지원함
    - Client가 표시하는 host 이름이 여러 인증서와 일치할 경우 Load Balancer가 client의 기능을 포함한 여러 요소를 기반으로 사용할 *최적의 인증서*를 결정함

  - IP주소를 대상으로 사용

    - Application back-end의 IP 주소를 대상으로 사용하여 AWS 또는 On-premise에 hosting 된 application을 load balancing 할 수 있음
      - => Instance의 모든 IP 주소 및 interface에 hosting 된 application back-end로 load balancing 할 수 있음
    - 같은 instance에 hosting 된 각 application은 연결된 보안 그룹을 가질 수 있고, 같은 port를 사용할 수 있음
    - IP 주소를 대상으로 사용하여 On-premise (Direct Connect or VPN), pairing 된 VPC 및 EC2-Classic (ClassicLink 사용)에 hosting 된 application을 load balancing 할 수 있음
    - AWS와 On-premise resource에 걸쳐 load balancing 할 수 있는 기능은 Cloud로 migration 또는 cloud로 busting 하거나 cloud로 장애 조치하는데 도움이 됨

  - Lambda 함수를 대상으로 사용

    - Application Load Balancer에서 HTTP request를 처리하는 Lambda function을 호출하여 web browser를 포함한 모든 HTTP client에서 serverless application에 대한 사용자 access를 제공 할 수 있음
    - Lambda function을 Load balancer의 대상으로 등록하고 content 기반 routing 규칙에 대한 지원을 통하여 요청을 다른 Lambda 함수로 routing 할 수 있음
    - Server 및 serverless computing을 사용하는 application에 대해 application load balancer를 공통 HTTP end point로 사용할 수 있음

    <br>

- #### `Network Load Balancer`

  : Application에 탁월한 성능 및 고정 IP가 필요한 경우

  - 연결 수준(Layer 4)에서 작동하는 Network Load Balancer는 IP 프로토콜 데이터를 기반으로 Amazon Virtual Private Cloud(VPC) 내의 대상으로 연결을 routing 함
  - TCP 및 UDP traffic 모두의 Load balancing에 적합한 Network Load Balancer는 **매우 짧은 지연시간**을 유지하면서 초당 수백만개의 요청을 처리할 수 있음
  - Network Load Balancer는 가용 영역당 하나의 정적 IP address를 사용하면서 *갑작스럽고 변동이 심한 traffic pattern을 처리하는데 최적화* 되었음
  - `Auto Scaling`, `Amazon EC2 Container Service(ECS)`, `Amazon CloudFormation`, 및 `AWS Certificate Manager(ACM)` 과 같은 다른 AWS service와 통합됨
  - 고가용성
    - Load Balancer는 등록된 대상의 상태를 monitoring하고 정상 대상으로만 traffic을 routing 함
  - 높은 처리량
    - Network Load Balancer는 traffic 증가를 처리할 수 있도록 설계되었으며 초당 수백만 개의 요청을 load balancing 할 수 있음
    - 갑작스롭고 변동이 심한 traffic pattern 도 처리할 수 있음
  - 짧은 지연시간
  - Source IP address유지
    - Client 측 source IP를 유지하므로 back-end가 client의 IP 주소를 확인할 수 있음
    - 그런 다음 추가 처리를 위해 application에서 이를 사용 할 수 있음
  - 정적 IP 지원
    - Application이 load balancer의 front-end IP로 사용할 수 있는 가용 영역 (subnet)별로 정적 IP를 자동으로 제공함
  - 탄력적 IP 지원
    - 가용 영역(subnet) 별로 탄력적 IP를 지정하여 자체 고정 IP를 제공할 수 있는 option이 제공됨
  - TLS (Transport Layer Security) Offload
    - Client와 Load balancer 간 TLS 종료를 지원
    - Network Load Balancer에서 TLS가 종료되더라도 원본 IP는 계속 back-end application에 보존됨
  - 상태 확인
    - Network 및 application 대상 둘 다에 대한 상태 확인을 지원함
    - 빠른 진단과 강력한 debugging을 위해 상태 확인에 대한 완전한 가시성과 장애가 발생하는 이유가 Network Load Balancer API의 'reason codes' 과 대상 상태 확인에 연결된 Amazon CloudWatch 지표를 통해 제공됨
  - DNS 장애 조치
    - Network Load Balancer에 등록된 정상 대상이 없거나 해당 영역의 **Network Load Balancer Node**가 비정상인 경우, `Amazon Route 53`이 다른 가용 영역에 있는 Load Balancer node로 traffic을 보냄
  - Amazon Route 53과의 통합
    - Network Load Balancer가 응답하지 않는 경우, Route 53과의 통합이 server에서 사용할 수 없는 Load Balancer IP 주소를 제거하고 traffic을 다른 region에 있는 대체 Load Balancer로 보냄
  - AWS service와 통합
  - 수명이 긴 TCP 연결
    - Network Load Balancer는 WebSocket 유형의 application에 적합한 수명이 긴 TCP 연결을 지원함

<br>

- #### `Classic Load Balancer`

  : 기존 application이 EC2-Classic Network 내에 구축되어 있는 경우

  - Classic Load Balancer는 여러 Amazon EC2 instance에서 기본적인 load balancing을 제공하며, 요청 수준 및 연결 수준에서 작동함
  - EC2-Classic Network 내에 구축된 application 용
  - Virtual Private Cloud(VPC) 를 사용할 때
    - Layer 7 - Application Load Balancer
    - Layer 4 - Network Load Balancer
  - 고가용성
    - 수신되는 application traffic에 대응하여 요청 처리 용량을 자동으로 조정함
  - 상태 확인 (Monitoring)
    - Classic Load Balancer는 Amazon EC2 instance의 상태를 감지 할 수 있음
    - 비정상 EC2 instance를 감지한 경우, 더 이상 해당 instance로 traffic을 routing 하지 않고 정상 instance 전체로 load 를 분배함
  - 보안 기능
    - Amazon Virtual Private Cloud (VPC)를 사용할 경우 Classic Load Balancer와 연결된 보안 그룹을 생성 및 관리하여 추가 Networking 및 보안 옵션을 제공할 수 있음
    - **Public IP address** 없이 Classic Load Balancer를 생성하여 Internet에 연결되지 않은 내부 Load Balancer로 사용할 수 있음
  - SSL (Secure Socket Layer) Off Load
    - SSL 복호화 off load
    - 중앙 집중식 SSL 인증서 관리
    - Public key 인증을 사용한 back-end instance 암호화
    - 유연한 암호 지원을 사용하면 load balancer가 client에게 제공하는 암호 및 protocol을 제어할 수 있음
  - 고정 세션
    - 쿠키를 사용하여 사용자 session을 특정 EC2 instance에 고정시키는 기능 지원
    - 사용자가 application에 access하는 동안 traffic은 동일한 instance로 routing 됨
  - IPv6 지원
    - Classic Load Balancer는 EC2-Classic Network에서 Internet protocol version 4 & 6 모두 사용할 수 있도록 지원함
  - Layer 4 & Layer 7 Load Balancing
    - HTTP/HTTPS application을 load balancing 하고 `X-Forwarded` 및 고정 session 과 같은 Layer 7 전용 기능을 사용할 수 있음
    - TCP protocol 만 사용하는 application에 대해 엄격한 Layer 4 load balancing을 사용할 수 있음
  - 운영 Monitoring
  - Logging
    - Access log 기능을 사용하여 load balancer로 전송된 요청을 모두 기록하고 이후 분석을 위해 Amazon S3에 log를 저장함
    - Log는 application 장애 진단 및 web traffic 분석에 유용함
    - `AWS CloudTrail` 을 사용하여 사용자 계정에 대한 Classic Load Balancer API 호출을 기록하고 log 파일을 전달할 수 있음
    - API 호출 기록을 사용하면 보안 분석 resource 변경 사항 추적, 규정 준수 감사를 수행할 수 있음

<br>

<br>

### ELB Services

> Elastic Load Balancing은 다음 서비스를 통해 application의 가용성 및 확장성을 개선함

<br>

#### 1. Amazon EC2

: Cloud 에서 application을 실행하는 가상 서버

- Load Balancer 를 구성하여 EC2 instance traffic을 routing 할 수 있음

<br>

#### 2. Amazon EC2 Auto Scaling

: Instance에 장애가 발생하더라도 원하는 수의 instance를 실행하고 instance의 수요가 변경되면 자동으로 instance 수를 늘리거나 줄일 수 있게 해줌

- ELB와 함께 Auto Scaling을 활성화하는 경우,
  - Auto Scaling이 시작한 instance는 자동으로 load balancer에 등록됨
  - Auto Scaling이 종료하는 instance는 자동으로 load balancer에서 등록 취소됨

<br>

#### 3. AWS Certificate Manager

: HTTP listener를 생성할 때 ACM에서 제공한 인증서를 지정할 수 있음

- Load Balancer는 인증서를 사용하여 연결을 종료하고 client의 요청을 암호화 해제함

<br>

#### 4. Amazon CloudWatch

: Load Balancer를 Monitoring하고 필요에 따라 조치를 취할 수 있게 해줌

<br>

#### 5. Amazon EC2

- EC2 instance cluster에서 `Docker container`를 실행, 중단 및 관리 가능함
- Load Balancer를 구성하여 container에 traffic을 routing 할 수 있음

<br>

#### 6. Route 53

- **도메인 이름** (ex. <www.example.com)을> computer를 사용하여 서로 연결해주는 숫자로 된 IP 주소 (ex. 192.0.2.1) 로 변환하여 방문자를 안정적이며, 비용 효율적으로 web site로 routing 하도록 함
- AWS는 load balancer와 같은 사용자의 AWS resource에 URL을 배정함

<br>

#### 7. AWS WAF

: Application Load Balancer와 함께 `AWS WAF`를 사용하여 `Web ACL (Access Control List)`의 규칙에 따라 요청을 허용하거나 차단할 수 있음

<br><br>

## Amazon Auto Scaling

- Amazon EC2 Auto Scaling을 통해 application의 load를 처리할 수 있는 정확한 수의 Amazon EC2 instance를  보유하도록 보장할 수 있음
- `Auto Scaling Group` 이라는 EC2 instance 모음을 생성함
- 각 Auto Scaling Group의 최소/최대 instance 수를 지정할 수 있음
- 원하는 용량을 지정한 경우 group을 생성한 다음에는 언제든지 Amazon EC2 Auto Scaling에서 해당 그룹에서 이만큼의 instance를 보유할 수 있음
- 조정 정책을 지정했다면 Amazon EC2 Auto Scaling에서는 application 의 늘어나거나 줄어드는 수요에 따라 instance를 시작하거나 종료할 수 있음

<br>

### Amazon Auto Scaling 핵심 구성 요소

<br>

#### 1. Group

- EC2 instance는 group에 정리되어 조정 및 관리 목저그이 논리적 단위로 처리할 수 있음
- Group을 생성할 때 EC2 instance 의 최소 및 최대 instance 수와 원하는 instance 수를 지정할 수 있음

<br>

#### 2. 구성 및 Template

- Group은 시작 template 또는 시작 구성을 EC2 instance에 대한 구성 template으로 사용함
- Instance의 AMI (Amazon Machine Image) ID, Instance 유형, key pair, security group, block device mapping 등의 정보를 지정할 수 있음

<br>

#### 3. 조정 Option

- ex) 지정한 조건의 발생 (동적 확장) 또는 일정에 따라 조정하도록 group을 구성 할 수 있음

 <br><br>

### ELB 및 Auto Scaling 구축하기

<br>

![Image result for elb autoscaling](https://jayendrapatil.com/wp-content/uploads/2016/06/Screen-Shot-2016-06-07-at-4.13.10-PM.png)

<br>

1. VPC 구축
2. ELB Target Group 생성
3. Auto Scaling 시작 구성 생성
4. Auto Scaling Group 생성
5. ELB 생성

<br>

<br>

<br>

#### Summary

: Amazon ELB (Elastic Load Balancing) 이 제공하는 세 가지 load balancer인 `Application Load Balancer`, `Network Load Balancer`, `Classic Load Balancer`는 모두 application의 내결함성에 필요한 **고가용성**, **자동 확장/축소**, **강력한 보안** 을 갖추고 있다.
