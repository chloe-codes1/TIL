# Amazon ElastiCache

> References: [AWS docs](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/WhatIs.html), [sarc.io](https://sarc.io/index.php/aws/656-aws-amazon-elasticache)

<br>

<br>

## What is ElastiCache?

- Amazon ElastiCache는 Cloud에서 **In-memory data store** 또는 **Cache** 를 손쉽게 `배포`, `운영` 및 `확장` 할 수 있게 해주는 서비스이다
- Amazon ElastiCache는 더 느린 disk 기반 database에 전적으로 의존하기보다는, 빠른 관리형 **In-memory data store**에서 **정보를 검색**할 수 있도록 지원하여 web application의 성능을 향상 시킨다
- Aamazon ElastiCache는 두 가지 Open Source In-memory Engine 을 지원한다

<br>

### 1. Redis

- 빠른 open source in-memory data store 및 caching
- Redis 용 Amazon ElastiCache는 Redis 호환 In-memory service로서, Redis의 간편한 사용성 및 능력과 더불어 까다로운 application에 필요한 **가용성** , **안정성** 및 **성능** 을 제공한다
- **단일 node**와 최대 15개의 **샤드 클러스터**가 지원되므로 In-memory data를 3.55TiB 까지 확장할 수 있다
- web, moile app, 게임, 광고 기술 및 IoT 와 같은 고성능 사용 사례에 적합한 서비스다

<br>

### 2. Memcached

- 널리 채택된 memory caching system
- ElastiCache는 Memcached와 protocol이 호환되므로 기존 Memcached 환경에서 사용되는 주요 도구가 ElastiCache에서 문제없이 작동한다

<br>

<br>

## About ElastiCache

- Amazon ElastiCache는
  - 실패한 node를 자동으로 감지한 후 교체하여 **자가 관리형 인프라**와 관련된 **오버헤드** 를 줄이고,
  - **복원력이 뛰어난 시스템을 제공**하여
    - web site 및 application load 시간이 길어지게 하는 database overload의 위험을 완화한다

- Amazon ElastiCache는 `Amazon CloudWatch`와 통합하여 **Redis** 또는 **Memcached** node와 관련된 주요 **성능 지표**의 **가시성**을 향상시킨다

- Amazon ElastiCache에서는 `AWS Managed Console` 을 사용하여 몇 분만에 인프라에 In-memory 계층을 추가할 수 있다

<br><br>

## Amazon ElastiCache for Redis

<br>

### What is Amazon ElastiCache for Redis?

- **Amazon ElastiCache** 는 cloud 내에서 `distributed in-memory data store` 또는 `cache environment` 를 **설정**, **관리** 및 **확장** 할 수 있도록 하는 web service 이다
  - **확장 가능**하고, **비용 효율적**인 **고성능 caching solution** 을 제공한다
  - 분산된 cache 환경의 배포 및 관리와 관련된 복잡성을 해소할 수 있다
- **Redis** 를 사용하는 기존 application은 거의 수정하지 않고 **ElastiCache** 를 사용할 수 있다
  - Application에서는 사용자가 배포한 **ElastiCache** node의 `host name` 과  `port 번호` 에 관한 정보만 필요하다
- **Redis** 용 **ElastiCache** 는 중요한 production 배포를 위해 서비스를 보다 안정적으로 제공하기 위한 여러 가지 기능을 갖추고 있다

<br>
