# Amazon ElastiCache

> References: [AWS docs](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/WhatIs.html), [sarc.io](https://sarc.io/index.php/aws/656-aws-amazon-elasticache)

<br>

<br>

## What is ElastiCache?

- Amazon ElastiCache is a service that makes it easy to `deploy`, `operate`, and `scale` **In-memory data stores** or **Cache** in the cloud
- Amazon ElastiCache improves web application performance by enabling **information retrieval** from fast managed **In-memory data stores** rather than relying entirely on slower disk-based databases
- Amazon ElastiCache supports two open-source in-memory engines

<br>

### 1. Redis

- Fast open-source in-memory data store and caching
- Amazon ElastiCache for Redis is a Redis-compatible in-memory service that provides the ease of use and capabilities of Redis along with the **availability**, **reliability**, and **performance** required for demanding applications
- Supports **single nodes** and up to 15 **shard clusters**, allowing in-memory data to scale up to 3.55TiB
- A suitable service for high-performance use cases such as web, mobile apps, gaming, advertising technology, and IoT

<br>

### 2. Memcached

- Widely adopted memory caching system
- ElastiCache is protocol-compatible with Memcached, so major tools used in existing Memcached environments work seamlessly with ElastiCache

<br>

<br>

## About ElastiCache

- Amazon ElastiCache
  - Automatically detects and replaces failed nodes to reduce **overhead** associated with **self-managed infrastructure**
  - Provides **highly resilient systems** that
    - Mitigate the risk of database overload that can cause long website and application load times

- Amazon ElastiCache integrates with `Amazon CloudWatch` to improve **visibility** of key **performance metrics** related to **Redis** or **Memcached** nodes

- Amazon ElastiCache allows you to add an in-memory layer to your infrastructure in minutes using the `AWS Management Console`

<br><br>

## Amazon ElastiCache for Redis

<br>

### What is Amazon ElastiCache for Redis?

- **Amazon ElastiCache** is a web service that allows you to **set up**, **manage**, and **scale** `distributed in-memory data stores` or `cache environments` in the cloud
  - Provides **scalable**, **cost-effective**, **high-performance caching solutions**
  - Eliminates the complexity associated with deploying and managing distributed cache environments
- Existing applications using **Redis** can use **ElastiCache** with minimal modifications
  - Applications only need information about the `hostname` and `port number` of the **ElastiCache** nodes you deploy
- **ElastiCache** for **Redis** has several features to provide more reliable services for critical production deployments

<br> 
