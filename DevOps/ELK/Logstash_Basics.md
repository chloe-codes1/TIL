# Logstash Basics

> Logstash에 대해 알아보아요우
>
> Reference: [Logstash docs](https://www.elastic.co/guide/en/logstash/current/introduction.html)

<br>

<br>

## What is Logstash?

<br>

### Logstash

- **Real-time pipeline** 기능을 가진 open source data collection engine
- 서로 다른 data source를 dynamic하게 **통합**하고, 지정한 목적지로 data를 **정규화** 할 수 있다

- Data를 **cleanse**하고 **democratize** 할 수 있다

<br>

<br>

## The Power of Logstash

<br>

### 1. Elasticsearch 등을 위한 강력한 수집 기능

시너지 효과를 발휘하는 Elasticsearch와 Kibana를 활용한 수평 확장 가능한 data processing pipeline

<br>

### 2. Pluggable pipeline architecture

다양한 input, filter, output을 mix & match하고 조정하면서 pipeline에서 조화롭게 운용 가능

<br>

### 3. Community-extensible and developer-friendly plugin ecosystem

200여개의 plugin 사용 가능 & 직접 plugin을 만들어 제공할 수도 있는 유연성도 갖고 있음

<br>

![logstash](../../images/image-20201203132913092.png)

<br>

<br>

## Logstash Loves Data

- 더 많은 data를 수집할수록 더 많이 알 수 있다
- Logstash는 모든 형태 및 규모의 data를 다룰 수 있다

<br>

### Logs and Metrics

모든것이 시작되는 곳

- 모든 유형의 logging data 처리 가능
  - 다양한 web log (ex. Apache)  및 appliction log (ex. log4j for Java) 를 수집한다
  - syslog, networking과 firewall log 등 여러 형식의 log를 수집한다
- [Filebeat](https://www.elastic.co/products/beats/filebeat)와 연계하여 보안을 유지하며 log를 전달할 수 있다