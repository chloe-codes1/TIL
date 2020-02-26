# Intro to AWS

<br>

#### Contents for Today

- Cloud Computing
- AWS 
- Main services
- Security
- Architecture



<br>

####  Good to Know

1. On-premise

   : 사용자가 직접 Infra, Platform, Application을 관리하는 모델이다  

2. Saas (Software as a Service)

   : 가장 일반적인 유형의 Cloud Service이며 Service를 제공하는 곳에서 Infra와 Software까지 모두 제공, 즉 Application Level까지 Service로 제공된다

<br>

<br>

## Intro to AWS Cloud

<br>

### What is Cloud Computing?

- `Internet based computing`의 일종으로 정보를 자신의 computer가 아닌 Internet에 연결된 다른 computer로 처리하는 기술
- Served when shared computer manage resources & data are requested 
- `Configurable computer resources` ( ex. Network, Server, Storage, Application, Service)에 대해 어디서나 접근 가능한 주문형 접근을 가능케 하는 모델
- 최소한의 관리 노력으로 빠르게 예비 및 release를 가능케 함
- `Clouding computing`과 `Storage Solution`들은 사용자와 기업들에게 개인 소유나 타사 Data center의 data를 저장, 가공하는 다양한 기능을 제공
- 전기망을 통한 전력망과 비슷한 일관성 및 규모의 경제를 달성하기 위해 자원의 공유에 의존함

![image-20200226112333821](../../../images/image-20200226112333821.png)

<br/>

<br>

### Cloud Computing Services

<br>

#### 1. On-premise (Traditional IT)

- 사용자가 직접 Infra, Platform, Application 관리
- 규모 있는 업체라면 직접 IDC를 구축하고, 일반적인 경우 IDC에 공간을 할당 받아 물리 서버를 설치하고 Hardware, Operating System, Server Application을 모두 관리함

<br>

#### 2. IaaS (Infrastructure as a Service)

- AWS EC2 
- Virtual Server, Data Storage & Hosting Computer, Network 등 IT Infra를 지원해주는 Service로 Hardware를 Service로 제공하는 Cloud Model
- Manage OS & Applications

<br>

#### 3. PaaS (Platform as a Service)

- AWS Elastic Beanstalk

- Serves Fundamental Iaas + Development Tools & Functions + Deployment

  -> They serve pretty much everything you need when you develop & deploy

- Developers only have to write logic to connect their application & served services 

<br>

#### 4. Saas (Software as a Service)

- Google Apps, Office 365

- 가장 일반적인 유형의 Cloud Service이며 Service를 제공하는 곳에서 Infra와 Software까지 모두 제공

   -> Serves `application level service`

- 개발자보다는 실 사용자에게 바로 제공함



4분? 5분 언저리까지 들은듯