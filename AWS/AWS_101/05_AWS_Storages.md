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

### Amazon Elastic File System (EFS)

> Re-sizable and cloud native file system for Linux

- AWS Cloud service와 on-premise resource에서 사용할 수 있는 간단하고 확장 가능하며 탄력적인 Linux 기반 workload용 file system 제공
- 이 제품은 application을 *중단하지 않고* on-demand 방식으로 peta byte(2^15) 까지 확장하도록 구축되었고, 파일을 추가하고 제거 할 때 자동으로 확장/축소되므로 application은 필요할 때 필요한 만큼 storage를 사용할 수 있음
-  수천 개의 Amazon EC2 instance에 대한 병렬 공유 access를 대량으로 제공하도록 설계되었기 때문에 application은 낮은 지연시간을 유지하면서 높은 수준의 집계처리량과 IOPS (Input/Output Operation Per Second)를 달성할 수 있음

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

<br>

### Amazon EBS Snapshot

- 지정 시간 snapshot을 만들어 Amazon S3에 Amazon EBS Volume data를 backup 할 수 있음
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

<br><br>

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

  

