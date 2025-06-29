# AWS Storages

<br>

#### Contents

- Storage
- Data Backup
- Snapshot
- S3 Glacier
- AMI & Market Place

<br>

#### Useful Informations

1. Amazon Elastic Block Store (Amazon EBS)는 Amazon EC2에 대해 가용성이 뛰어나고 일관되며 지연시간이 짧은 block storage를 제공한다
2. EBS는 단일 EC2 instance에서 permanent storage에 access 해야하는 workload에 적합함
3. EBS serves permanent local storage service for Amazon EC2, RDBMS & NoSQL, data warehousing, enterprise application, big data, backup and restore

<br><br>

## Storage

- Storage란?

  - 컴퓨터에 데이터를 저장하는 저장서의 역할을 수행하는 부품
    - 컴퓨터의 하드디스크와 동일한 역할을 수행하는 부품이라고 이해하면 된다!

- 스토리지를 **Server에 직접 연결**할 수 있고, 대용랑의 데이터를 저장하기 위해 별도의 **스토리지용 네트워크**를 구성할 수 있다

  1. **Server에 직접 연결하는 방식**
     - DAS (Direct Attached Storage)

  2. **스토리지를 빠른 속도의 네트워크로 연결하는 방식**
     - NAS (Network Attached Storage)
       - `LAN (Local Area Network)` 을 연결하여 사용하기 때문에 비용이 저렴
       - **파일 단위**로 데이터에 접속
       - OS에 파일 서버로 표시됨
     - SAN (Storage Area Network)
       - 확장이 용이
       - 대규모 enterprise 환경을 구성하기 적합한 **고속**의 **전용 네트워크**를 구성하여 빠른 속도의 스토리지 서비스를 제공
       - **블록 수준**에서 데이터를 저장
       - OS 입장에서 SAN은 일반적으로 디스크로 나타나며 별도로 구성된 스토리지용 네트워크가 존재함

<br>

<br>

## AWS Cloud Storage

> Data를 저장하는 안정적이고, 확장 가능하며, 안전한 장소

- Cloud computing의 매우 중요한 구성 요소로서, application에서 사용하는 정보를 보관
- 모든 big data analysis, data warehouse, Internet of Things(IoT), database, backup, archive application에는 일정 형태의 data storage architecture가 필요함
- Cloud storage는 일반적으로 기존 `on-premise` storage system보다 안정성, 확장성 및 보안성이 뛰어남
- AWS에서는 모든 범위의 cloud storage service를 제공하여 application과 archive 규정 준수 요구 사항을 모두 지원함
- Object, file, block storage service와 cloud data migration option을 선택하여 Cloud IT environment의 기초 설계 시작 가능

<br>

### Amazon Simple Storage Service (Amazon S3)

: User created content, active archive, serverless computing, big data storage, data warehouse, backup & restore를 위해 인터넷에서 data에 access할 수 있도록 지원하는 확장 가능하고 안정적인 platform

- `Object Store`

  - Internet을 통해 모든 유형의 data를 저장하고 access 할 수 있도록 설계된 object storage
  - 안전하고, 99.9999999%의 내구성을 제공하며, 수십조의 객체로 확장 가능

<br>

### Amazon EBS (Elastic Block Store)

> : EC2 에 연결되는 **Block Level**의 Storage service
>
> Server에 장착하는 **Server용 하드디스크** 라고 생각하면 됨!

- EC2 Instance용 영구 블록 수준의 Storage Volume
- **안정적**이고, **지연 시간**이 **짧다**
- 크기는 1GB 단위로 1GB ~ 1TB까지 선택 가능하다
- **크기**/**사용 기간**을 기준으로 비용이 과금된다
  - `마그네틱` 의 경우 발생하는 **I/O 횟수**에도 비용이 과금된다!
- EC2 Instance와 독립적으로 사용 가능하며, 다른 EC2 Instance에 교체 가능하다
- 데이터는 영구적으로 저장되며, 원하는 가용 영역 (Availability Zone, AZ)에 생성 가능하다
- 백업된 Snapshot에서 EBS volume을 **생성/복원** 가능하다
  - 다른 AZ에도 생성 가능하다!

<br>

### Amazon Elastic File System (EFS)

> Re-sizable and cloud native file system for Linux

- AWS Cloud service와 on-premise resource에서 사용할 수 있는 간단하고 확장 가능하며 탄력적인 Linux 기반 workload용 file system 제공
- 이 제품은 application을 *중단하지 않고* on-demand 방식으로 peta byte(2^15) 까지 확장하도록 구축되었고, 파일을 추가하고 제거 할 때 자동으로 확장/축소되므로 application은 필요할 때 필요한 만큼 storage를 사용할 수 있음
- 수천 개의 Amazon EC2 instance에 대한 병렬 공유 access를 대량으로 제공하도록 설계되었기 때문에 application은 낮은 지연시간을 유지하면서 높은 수준의 집계처리량과 IOPS (Input/Output Operation Per Second)를 달성할 수 있음

<br>

### AWS Backup

> AWS Service 전체에 걸쳐 중앙에서 backup 관리 및 자동화

- 완전 관리형 backup service로, cloud 뿐만 아니라 on-premise에서도 AWS Storage Gateway를 사용해 AWS service 전체에서 data backup을 손쉽게 중앙화 하고 자동화 할 수 있음
- AWS Backup을 사용하면 Amazon EBS volume, Amazon RDS databse, Amazon DynamoDB table, Amazon EFS file system 및 AWS Storage Gateway volume과 같은 AWS resources에 대한 backup 활동을 모니터링하고 중앙에서 backup 정책을 구성할 수 있음
- AWS Backup은 *완전 관리형* 정책 기반 backup solution을 제공하여 backup 관리를 간소화하고, 비즈니스 규제상의 backup 규정 준수 요구사항을 충족할 수 있도록 지원

<br>

### AWS Storage Gateway

> 완벽한 통합과 최적화된 데이터 전송을 지원하는 hybrid cloud storage

- on-premise 환경을 Amazon cloud storage에 완벽하게 연결하는 software appliance
- AWS cloud storage에 대한 연결 기능이 고도로 최적화된 local storage를 제공하며, migration, busting 및 storage 계층화 사용에 유용함

<br>

<br>

## AWS Backup

> AWS EC2 Service에는 AMI, EBS, Snapshot 등의 기능들이 있어 backup이 용이하며, instance를 종료하더라도 data를 쉽게 보존할 수 있음

<br>

### AWS EC2 Backup

<br>

![aws backup 이미지 검색결과](https://d1.awsstatic.com/product-marketing/AWS%20Backup/product-page-diagram_aws_backup_how-it-works.aafc7b1324fd4d8b52e9fbcd5c95e14529de27c6.png)

<br>

- EC2 instance를 사용하지 않더라도 켜놓으면 계속 과금이 발생하므로 사용하지 않는 instance는 중지하고 제거해야함
- 언제 다시 사용할지 모르거나, data가 많이 쌓여있는 DB instance의 경우에는 backup이 필요함
- EC2의 대부분의 instance가 root volume을 가지고 있고, 필요하면 추가로 EBS volume을 instance에 붙이는 구조인데, create image를 통해 AMI를 생성하고, 각각의 EBS volume에 대한 snapshot이 필요함
  - `AMI (Amazon Machine Image)`
    - Instance를 시작할 때 필요한 모든 정보를 포함함
    - ex) OS 정보, AMI 접근 권한, EBS volume mapping 정보 등
  - `EBS (Elastic Block Store)`
    - 컴퓨터의 disk drive, 즉 data를 담고 있음
    - 하나의 instance를 정상적으로 backup 및 복원을 하기 위해서는 1개의 AMI와 그에 딸린 n개의 EBS volume이 필요함
  - `Create Image`
    - EC2 console 창에서 snapshot을 뜨고싶은 instance를 우클릭해 'Image' -> 'Create Image'를 클릭하면 instance와 딸려있는 EBS 전체를 한 번에 snapshot을 떠서 저장할 수 있음

<br>

<br>

## Snapshot

- Snapshot은 기술적인 용어로, 특정 시간에 **데이터 저장 장치**의 **상태**를 별도의 파일이나 이미지로 저장하는 기술
- Snapshot 기능을 이용하여 데이터를 저장하면 **유실된 데이터**의 **복원**과 일정 시점의 상태로 데이터를 **복원**할 수 있다
  - `Git` 의 snapshot 을 떠올리자!
- **데이터 분석**, **데이터 보호** 및 **데이터 복제**와 같은 작업을 위해 수행된다
  - **재해 복구 (Disaster Recovery)**와 같은 장애 상황에서도 데이터 복원을 통해 중요하고 긴급한 상황에도 최상의 **데이터 보호 수단**이 될 수 있다!
- **데이터 연속성**을 요구하는 상황에서 데이터를 **보호**할 뿐만 아니라 높은 애플리케이션 **가용성**을 제공하고, 대용량 데이터의 **백업 관리**를 단순화하여 운영 관리 **비용**을 **최소화** 할 수 있다
- Amazon Web Services 는 `EBS (Elastic Block Storage)`에 대한 Snapshot을 제공함으로써 손쉽게 서버의 데이터 **백업/복원** 및 다른 EC2 region으로 EBS **복사** 기능을 통해 Instance의 migration을 지원한다
  - 또한 이를 활용한 다양한 **재해 복구 시나리오**를 제공한다!

<br>

### Amazon EBS Snapshot

> EBS Volume Data를 snapshot으로 만들어 backup 및 보관 할 수 있는 기능
>
> -> 컴퓨터의 하드디스크를 통째로 backup 할 수 있는 기능이라고 생각하면 됨

- 지정 시간 snapshot을 만들어 Amazon S3에 Amazon EBS Volume data를 backup 할 수 있음
- Snapshot 진행 과정 중에도 *EBS나 EC2의 서비스 중단 없이* 기존 서비스를 즉시 사용 가능
- EBS Volume의 크기 조정에 사용될 수 있음
- `Snapshot의 공유 기능`을 활용하여 권한이 있는 다른 사용자에게 공유 할 수 있음
- 다른 Region으로 복사 가능
- Snapshot은 *증분식 backup*이어서 마지막 snapshot 이후 변경된 device의 block만이 저장됨
  - 이로인해 snapshot을 만드는데 필요한 시간이 최소화되며 data를 복제하지 않으므로 storage 비용이 절약됨
- Snapshot을 삭제하면 해당 snapshot에 고유한 data만 제거됨
- 각 snapshot에는 snapshot을 만든 시점의 data를 새 EBS Volume에 복원하는데 필요한 모든 정보가 있음
- Snapshot을 기반으로 EBS Volume을 생성하는 경우, 새 volume은 해당 snapshot을 생성하는데 사용된 원본 volume과 정확히 일치함
- 복제된 volume은 사용자가 즉시 사용할 수 있도록 background에서 data를 load함
- 아직 load되지 않은 data에 access하는 경우, volume은 요청한 data를 Amazon S3에서 즉시 다운로드 한 후 background에서 나머지 data를 계속해서 load함
- `다중 볼륨 스냅샷`
  - Snapshot을 사용하여 여러 EBS Volume에 걸쳐있는 file system 또는 database 등의 중요한 workload backup을 생성할 수 있음
  - 다중 볼륨 스냅샷을 통해 EC2 instance에 연결된 여러 EBS volume에서 특정 시점, data 조정 및 충돌 일치 snapshot을 생성 할 수 있음
  - Snapshot은 여러 EBS Volume에서 자동으로 생성되기 때문에 instance를 중지하거나 중단 일관성 유지를 위해 volume간 조정을 할 필요가 없음!

<br>

#### Amazon EBS 성능과 보안성 높이기

1. `Provisioned IOPS (I/O Operations Per Second)`
   - EBS 생성 시EBS 유형에서 선택 가능한 option으로 Disk의 IOPS 성능을 지정할 수 있음
   - 고성능의 서비스 제공에 적합한 EBS!
2. `EBS-Optimized Instance`
   - EBS의 Disk service를 위한 전용 네트워크의 대역폭을 사용하도록 구성하여, Disk 성능을 최적화 하는 기능
3. `EBS Security`
   - 암호화 키는 AWS의 KMS에서 직접 생성하거나 기본키를 사용할 수 있음
   - 이렇게 암호화된 snapshot은 공유 및 타 AWS 계정에 공유되어도 사용할 수 없음

<br>

<br>

## Amazon S3 (Simple Storage Service)

> 어디서나 원하는 양의 데이터를 저장하고 검색할 수 있도록 구축된 객체 스토리지

<br>

### Amazon S3란?

- 무한대로 저장 가능하고, 사용한 만큼만 지불하는 **인터넷 기반 스토리지 서비스**

- `버킷 (Bucket)`이라는 region 내에서 유일한 영역을 생성하고, 데이터를 **key-value** 형식의 객체(Object)로 저장한다
- 비용이 **매우 저렴**하며, 간단한 정적 web site를 만들 수 있다
- S3 서버는 **스토리지 기술**을 근간으로 하며, **파일 단위**의 접근만 지원하기 때문에 `EBS (Elastic Block Storage)` 서비스를 대체할 수는 없다
- 사용하고 있는 저장 공간만큼 매월 비용을 지불하며, 저장하는 **데이터의 크기**, **Access 요청 횟수**, **데이터 다운로드 (Network Out) 용량** 등으로 전체적인 비용을 산정한다
- URL 을 통해 손쉽게 파일 공유가 가능하다
- 99.999999999% 의 내구성을 자랑한다
- 프리티어 사용 가능 범위
  - 5GB Amazon S3 표준 스토리지
  - `GET` 요청 20,000건, `PUT` 요청 2,000건 사용 가능

<br>

### Amazon S3 활용 분야

| 활용 분야                                               | 내용                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| **백업 및 복구 (Backup & Restore)**                     | - 뛰어난 **내구성**과 **확장성**을 제공한다<br>- 버전 관리 기능을 통한 데이터 보호기능 제공과 **하이브리드 구성**을 통해 기업 내 데이터 **백업/복원** 기능을 제공할 수 있다 |
| **데이터 아카이빙 (Data Archiving)**                    | 고객이 규제 대상 산업 (금융 및 의료)을 위한 규정준수, 아카이브 요구사항 또는 아카이브 데이터에 드물지만 빠르게 access 해야하는 조직을 위한 활성, 아카이브 요구사항을 충족할 수 있도록 다양한 Storage class를 제공한다 |
| **빅데이터 분석을 위한 데이터 레이크 (Data Lake)**      | 제약 또는 재무 데이터, 사진과 비디오와 같은 멀티미디어 파일과 같이 어떤 파일을 저장하든 관계없이 Amazon S3를 **빅데이터 분석**용 `데이터 레이크 (Data Lake)` 로 사용할 수 있다 |
| **하이브리드 클라우드 스토리지 (Hybrid Cloud Storage)** | AWS Storage Gateway와 연계하여 `On-premise` 환경에서 클라우드 스토리지를 활용할 수 있으며, 데이터 백업 및 재해복구를 원활하게 수행할 수 있다 |
| **재해 복구 (Disaster Recovery)**                       | S3의 **내구성** 및 **안정성**이 뛰어난 글로벌 인프라를 활용하여 탁월한 데이터 보호 및 타 region으로 **교차 리전 복제 (CCR)** 서비스를 제공한다 |

<br>

<br>

## Amazon S3 Glacier

> Data archiving을 위한 안전하고 안정적인 장기 객체 스토리지

- Data archive 및 장기 backup을 위한 매우 저렴한 cloud
- 9.999999%의 안정성을 제공하도록 설계됨
- 현재 위치에서 query하는 기능을 제공하므로 저장된 archive data에 직접 분석을 실행 할 수 있음
- 고객은 월별 GB당 0.004 USD의 저렴한 요금으로 data를 저장할 수 있으므로 on-premise solution 대비 상당한 비용절감 가능
- 비용을 낮게 유지하면서 동시에 다양한 검색 요구를 지원하기 위해 archive에 access하는 3가지 option (몇 분에서 몇 시간까지 소요)을 제공함

<br><br>

## AMI & Market Place

<br>

### Amazon Machine Image (AMI)

- Instance를 시작하는 데 필요한 정보를 제공함

- Instance를 시작할 때 AMI를 지정해야 함

- 동일한 구성의 Instance가 여러개 필요할 때는 한 AMI에서 여러 Instance를 시작할 수 있음

- 서로 다른 구성의 Instance가 필요한 경우에는 다양한 AMI를 사용하여 Instance를 시작하면 됨

- `AMI 구성요소`

  - 1개 이상의 EBS Snapshot or Instance root volume에 대한 template (ex. OS, Application Server, Application)

  - AMI를 사용하여 Instance를 시작할 수 있는 AWS 계정을 제어하는 시작 권한

  - 시작될 때 Instance에 연결할 volume을 지정하는 **Block Device Mapping**

<br>

### AWS Marketplace

- 고객이 solution을 개발하여 비즈니스를 운영하는데 필요한 타사 software 및 서비스를 찾아 구매, 배포, 관리까지 할 수 있도록 curation process를 거친 `Digital Catalog`

- Security, Network, Storage, ML, Business Intelligence, Database, DevOps 등 인기있는 category에 속한 software 제품이 수천 개에 이를 정도로 매우 많음

- 고객은 구매자/판매자로서 혹은 둘 다로서 AWS Marketplace 사용 가능
