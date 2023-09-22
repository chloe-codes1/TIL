# AWS Solutions Architect - Associate Prep Workshop

<br>

#### 문항 할당

1. 복원력을 갖춘 아키텍쳐 설계
2. 성능 기준에 맞는 솔루션 정의
3. 안정한 Application 및 Architecture 지정
4. 비용에 최적화된 Architecture 설계
5. 운영면에서 탁월한 Architecture 정의

<br>

<br>

## Overview

<br>

### EC2 Instance Store

- 임시 지원되는 볼륨
- 오직 특성 EC2 instance만
- 고정 용량
- Disk 유형과 용량은 EC2 instance 유형에 따라 결정
- Application 수준 내구성
- I/O가 빠름

<br>

### Elastic Block Store (EBS)

- 다양한 유형
- 암호화
- 스냅샷
- 프로비저닝된 용량
- EC2 Instance와 다르 독립적인 수명 주기
- 대량의 볼륨을 생성할 수 있도록 여러 볼륨이 스트리핑

<br>

![image-20200309134828549](../../images/image-20200309134828549.png)

> 답: B

<br><br>

### Amazon S3

- Object Storage
- 일관성
- Storage class 및 내구성 - Standard, Standard-IA
- 암호화
  - 저장데이터
  - 전송데이터
- 버전 관리
- Access 제어
- Multi-part upload
- Internet / API access 가능
- 사실상 무제한의 용량
- Region 수준 Availability
- 뛰어난 내구성 - 99.9999999999% (nine eleven)

<br>

<br>

### Amazon Glacier

- Data backup 및 Archive storage
- 검색
- 암호화
- 리전 가용성

<br><br>

#### 구성요소의 상태에서 결합 해제

![image-20200309135329574](../../images/image-20200309135329574.png)

- Load Balancer or SQS가 message의 전달률을 높여줌

<br>

<br>

#### 확장성을 위한 결합 해제

![image-20200309135522472](../../images/image-20200309135522472.png)

<br>

<br>

#### 구성 요소의 ID에서 결합 해제

![image-20200309135708110](../../images/image-20200309135708110.png)

<br><br>

![image-20200309135953183](../../images/image-20200309135953183.png)

> 답: B, D

<br><br>

### 내결함성

: 모든것은 실패 할 수 있다  -> 대비가 필요하다!

![image-20200309140033872](../../images/image-20200309140033872.png)

<br>

![image-20200309140344479](/home/chloe/SSAFY/TIL/images/image-20200309140344479.png)

> 답: C

- 고가용성이 나오면 복수의 가용 영역이 필요함!

  - 단일 가용 영역이란 말이 들어가면 답이 아님

- 고가용성은 SLA (Service Level Agreement) 는 갖출 필요 없음

  - `SLA`

    : A service-level agreement (SLA) defines the level of service you expect from a vendor

<br>

![image-20200309140439634](/home/chloe/SSAFY/TIL/images/image-20200309140439634.png)

> 답: D

- 내결함성은 SLA 갖춰야함

<br>

<br>

### Cloud formation

- AWS서비스를 배포하기 위한 선언형 언어

![image-20200309140534063](../../images/image-20200309140534063.png)

<br>

![image-20200309140757315](/home/chloe/SSAFY/TIL/images/image-20200309140757315.png)

> 답: B

<br><br>

### AWS lambda

- 이벤트 또는 시간 기반 간격에 대한 응답으로 상태 비저장 코드(Node.js, Python 등)를 실행하는 완전관리형 컴퓨팅 서비스
- Amazon EC2 instance 및 Auto Scaling 그룹과 같은 인프라를 관리하지 않고도 코드를 실행할 수 있음

<br>

![image-20200309141006364](/home/chloe/SSAFY/TIL/images/image-20200309141006364.png)

> 답: C

<br>

![image-20200309141202930](/home/chloe/SSAFY/TIL/images/image-20200309141202930.png)

> 답: B

- RTO (Recovery Time Objective)

  : 장애 복구 최소 시간

- RPO (Recovery Point Objective)

  : 목표 복구 시점

<br>

![image-20200309141335170](../../images/image-20200309141335170.png)

<br><br>

### 성능이 뛰어난 Architecture 설계

1. 성능이 뛰어난 Storage 및 Database 설계
2. Caching을 적용하여 성능 개선
3. 탄력성과 확장성을 갖춘 솔루션 설계 - `Auto Scaling`, `CloudWatch`

<br>

![image-20200309142239841](../../images/image-20200309142239841.png)

- 하드디스크가 성능이 낮은것만음 아님!
  - 처리량에 최적화됨
- SSD 에서 일반적인 목적이면 => 범용
- 빠른 볼륨당 최대 처리량 필요 /random한 data 에 access 면 => Provisioning된 IOPS

<br>

<br>

### AWS S3 Bucket

![image-20200309142747237](../../images/image-20200309142747237.png)

<br>

<br>

### Amazon S3: 결제 모델

![image-20200309142831070](../../images/image-20200309142831070.png)

<br>

<br>

### Amazon S3: Storage Class

![image-20200309143130329](../../images/image-20200309143130329.png)

- 장기적으로 보관해야하는 data는 `Infrequent Access`에 저장

<br>

#### S3 수명 주기 정책

: Amazon S3 수명 주기 정책을 사용하면 생성 후 기간을 기준으로 객체의 Storage class를 변경 / 삭제 할 수 있음

![image-20200309143358722](../../images/image-20200309143358722.png)

<br>

![image-20200309143504975](../../images/image-20200309143504975.png)

> 답: D

- 교차 리전 access를 사용해서 여러 region에 복사 할 수는 있음

<br>

![image-20200309143709015](../../images/image-20200309143709015.png)

> 답: A, C

<br>

<br>

### Amazon RDS 사용 시기

![image-20200309143810190](/home/chloe/SSAFY/TIL/images/image-20200309143810190.png)

<br>

<br>

### RDS 읽기 전용 복제본

: Select Query만을 위한 복제본

![image-20200309144129531](../../images/image-20200309144129531.png)

<br>

<br>

### DynamoDB: Provisioning 된 처리 용량

> AWS의 대표적인 NoSQL

![image-20200309144250727](../../images/image-20200309144250727.png)

<br>

<br>

### CloudFront 에서 Caching

![image-20200309144742870](../../images/image-20200309144742870.png)

<br>

<br>

### Memcached와 Redis 비교

![image-20200309144934818](../../images/image-20200309144934818.png)

<br>

![image-20200309145317660](../../images/image-20200309145317660.png)

<br><br>

### AWS CloudFront

![image-20200309145420860](../../images/image-20200309145420860.png)

<br><br>

### 확장성있는 설계

![image-20200309145459007](../../images/image-20200309145459007.png)

<br>

<br>

### Auto Scaling

![image-20200309145612245](../../images/image-20200309145612245.png)

<br>

<br>

#### Auto Scaling을 Kick 하는 CloudWatch 경보

![image-20200309145744500](../../images/image-20200309145744500.png)

<br>

![image-20200309145821604](../../images/image-20200309145821604.png)

<br>

![image-20200309145940096](../../images/image-20200309145940096.png)

<br>

<br>

### Auto Scaling 구성 요소

![image-20200309150011191](../../images/image-20200309150011191.png)

<br><br>

### Elastic Load Balancing (ELB) 에 의한 Traffic 분산

<br>

![image-20200309150747880](../../images/image-20200309150747880.png)

> 답: C

<br>

![image-20200309151127936](../../images/image-20200309151127936.png)

> 답: B, E, F

<br>

![image-20200309151309160](../../images/image-20200309151309160.png)

> 답: B,D

<br>

<br>

![image-20200309151343847](../../images/image-20200309151343847.png)

<br><br>

### AWS IAM

![image-20200309152454364](../../images/image-20200309152454364.png)

<br>

#### AWS에서 사용하는 자격 증명

![image-20200309152540848](../../images/image-20200309152540848.png)

<br>

![image-20200309152900595](../../images/image-20200309152900595.png)

> 답: A, C, E

<br>

<br>

### Computing/Network Architecture

![image-20200309152949240](../../images/image-20200309152949240.png)

<br>

#### Virtual Private Cloud (VPC)

![image-20200309153030216](../../images/image-20200309153030216.png)

<br>

<br>

### Subnet 사용 방법

![image-20200309153120772](../../images/image-20200309153120772.png)

<br>

<br>

### 보안 그룹과 Network ACL 비교

![image-20200309153402116](../../images/image-20200309153402116.png)

<br><br>

### 보안 그룹

: 보안 그룹을 사용하여 resource에서 송수신되는 traffic을 제어

![image-20200309153602501](../../images/image-20200309153602501.png)

<br>

<br>

### VPC 연결

![image-20200309153745540](../../images/image-20200309153745540.png)

<br><br>

### Private Instance의 Outbound Traffic

<br>

ex 1)

![image-20200309153856056](../../images/image-20200309153856056.png)

<br>

ex  2)

![image-20200309153943668](/home/chloe/SSAFY/TIL/images/image-20200309153943668.png)

- 성능에 대한 확장성은 NAT Gateway가 더 나음

<br>

![image-20200309154239509](../../images/image-20200309154239509.png)

> 답: A, C, E

- E번은 하나 마나인게 별도로 수정하지 않는이상 Network ACL은 Port 80에서 Inbound access를 항상 허용함...
  - 하지만 틀린말은 아니므로 답..!

<br>

<br>

### 저장 데이터

> S3에 저장된 데이터는 기본적으로 프라입시이고 accessㅏ려면 AWS 자격 증명이 필요하다

![image-20200309154502649](../../images/image-20200309154502649.png)

![image-20200309154523626](../../images/image-20200309154523626.png)

<br><br>

### Key 관리

![image-20200309154613320](../../images/image-20200309154613320.png)

<br>

![image-20200309154826811](../../images/image-20200309154826811.png)

<br>

![image-20200309155010053](../../images/image-20200309155010053.png)

> 답: B, D, E

<br>

![image-20200309155222445](../../images/image-20200309155222445.png)

> 답: B

<br>

<br>

![image-20200309155306646](../../images/image-20200309155306646.png)

- Root 사용자는 최후의 보루
  - Root 사용자로서 access key와 security key를 만드는 것은 절대 금물!
- Role에 의해 application이 권한에 따른 역할을 수행할 수 있도록 하는것이 보안에 좋다

<br>

<br>

### Amazon EC2 요금

![image-20200309160427703](../../images/image-20200309160427703.png)

- 탄력적 IP주소

  : 사용할 때는 비용이 발생하지 않지만, 사용하지 않을 때 IP 주소를 붙잡아두면 비용이 부과됨

  - IP주소 하나 당 월 $3 정도

<br>

#### EC2 요금 요소

- Instance family
- tenancy
- 요금 옵션

<br>

#### EC2: 비용을 절약할 수 있는 방법

![image-20200309160800242](../../images/image-20200309160800242.png)

<br>

![image-20200309161137491](../../images/image-20200309161137491.png)

<br>

<br>

### Amazon EBS 요금

![image-20200309161333929](../../images/image-20200309161333929.png)

<br>

![image-20200309161511103](../../images/image-20200309161511103.png)

> 답: A

<br>

<br>

![image-20200309161549562](../../images/image-20200309161549562.png)

<br>

<br>

### CloudFront를 통한 Caching

![image-20200309161734120](../../images/image-20200309161734120.png)

<br>

<br>

![image-20200309161805190](../../images/image-20200309161805190.png)

<br><br>

### 운영면에서 탁월한 Architecture 정의

<br>

![image-20200309162004529](../../images/image-20200309162004529.png)

<br>

<br>

### 운영 우수성을 지원하는 AWS 서비스

![image-20200309162236340](../../images/image-20200309162236340.png)

<br>

- `AWS Cloud Trail`

  : AWS API 단위로 누가 언제 어떤 명령어를 내렸는지 기록을 남김

<br>

![image-20200309162620668](../../images/image-20200309162620668.png)

> 답: C

<br>

![image-20200309162909909](../../images/image-20200309162909909.png)

> 답: B

<br>

<br>

![image-20200309162947164](../../images/image-20200309162947164.png)

<br>

<br>

### Summary

![image-20200309163259775](../../images/image-20200309163259775.png)

<br>

![image-20200309163436032](../../images/image-20200309163436032.png)

<br>

<br>

<br>

### Q&A

질문:

그럼 시험에서는 유저가 EBS 볼륨을 보존한다는게 default 로 설정했다고 생각하면 되나요?

답변:

EC2 종료시 EBS 볼륨이 삭제 된다 란 명제가 있으면 거짓이 될것입니다. 더 정확하게 실제로는 현재 EC2를 만들때 EBS를 할당할때 루트 볼륨의 경우 default로 같이 삭제 되도록 설정이되고 루트 볼륨을 제외한 다른 볼륨은 default로 삭제 되지 않게 설정이 되긴합니다.(이 과정에서 여러분들이 직접 지정도 가능합니다.)

<br>

질문:

MFA은 무엇인가?

답변:

멀티 팩터 인증을 말하는 겁니다. 예를들어 로그인을 할때 암호에다가 추가적으로 OTP등을 이용해서 인증을 하는것을 말합니다. AWS도 MFA 를 활성화해서 이중보안이 가능합니다. authy 와 같은 소프트 토큰을 사용할 수도 있고 gelmato 같은 물리적인 토큰을 사용할 수도 있습니다.

<br>

질문:

언제 NAT instance를 사용하는 게 적합한가요? NAT Gateway와 비교해서요.

답변:

NAT Gateway는 port forwarding 같은 기능을 제공하지 않는 제약사항들이 있습니다. 이와 같이 NAT Gateway가 제공하지 않는 기능들을 직접 고객이 제어해야 할때 NAT instance를 직접 구성해서 사용해야 하는 필요성이 있을 수 있습니다. 또는 자체적인 보안적인 요소를 구성하기 위해서 사용할 수도 있겠네요. NAT Gateway는 AWS 가 제공하는 관리형 서비스로서 내장된 확장성과 내구성을 갖추고 있어 쉽게 구성해서 사용할 수 있는 장점이 있습니다.

<br>

질문:

EC2 instance storage와 EBS 는 다른 건가요?

답변:

네 인스턴스 스토리지는 호스트에 내장된 스토리지로써 휘발성의 특징을 갖고 있는 스토리지 입니다. 인스턴스 스토리지는 인스턴스 유형에 따라 제공되는 것이 있고 제공되지 않는 것이 있습니다. 제공되는 용량도 인스턴스 유형에 따라 정해져 있습니다. 휘발성이라 함은 인스턴스가 stop 되었다가 다시 기동되었을때 데이터가 보존되지 않음을 의미합니다. 이런 특징이 있는대신 네트워크를 통해 마운트해서 사용하는 EBS에 비해 성능이 뛰어나다는 장점이 있습니다. 이에 비해 EBS는 데이터를 영구적으로 저장할 수 있겠죠.
