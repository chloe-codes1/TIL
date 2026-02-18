# Logstash Basics

> Let's learn about Logstash
>
> Reference: [Logstash docs](https://www.elastic.co/guide/en/logstash/current/introduction.html)

<br>

<br>

## What is Logstash?

<br>

### Logstash

- An open source data collection engine with **real-time pipeline** capabilities
- Can dynamically **unify** different data sources and **normalize** data to a specified destination

- Can **cleanse** and **democratize** data

<br>

<br>

## The Power of Logstash

<br>

### 1. Powerful Ingestion for Elasticsearch and More

A horizontally scalable data processing pipeline leveraging the synergy of Elasticsearch and Kibana

<br>

### 2. Pluggable pipeline architecture

Mix & match and orchestrate various inputs, filters, and outputs harmoniously in the pipeline

<br>

### 3. Community-extensible and developer-friendly plugin ecosystem

Over 200 plugins available & flexible enough to create and provide your own plugins

<br>

![logstash](../../kor/images/image-20201203132913092.png)

<br>

<br>

## Logstash Loves Data

- The more data you collect, the more you can learn
- Logstash can handle data of all shapes and sizes

<br>

### Logs and Metrics

Where everything begins

- Can handle all types of **logging data**
  - Collects various **web logs** (ex. Apache) and **application logs** (ex. log4j for Java)
  - Collects syslog, networking and firewall logs in various formats
- Can securely forward logs in conjunction with [Filebeat](https://www.elastic.co/products/beats/filebeat)

<br>

### The Web

Realizing the true utility of the World Wide Web

- Convert [HTTP requests](https://www.elastic.co/guide/en/logstash/7.10/plugins-inputs-http.html) to events
  - Use Twitter and other **firehoses** for social sentiment analysis
  - **Webhook** support for Github, Jira, and numerous other applications
  - Support for various [Watcher](https://www.elastic.co/products/x-pack/alerting) alerting use cases
- Generate events by polling [HTTP endpoints](https://www.elastic.co/guide/en/logstash/5.4/plugins-inputs-http_poller.html) as needed
  - Collect **status**, **performance**, **metrics**, and other data types from web application interfaces

<br>

### Data Stores and Streams

Discover greater value from data you already have

- Better understand data from related databases or NoSQL stores through the [JDBC](https://www.elastic.co/guide/en/logstash/5.4/plugins-inputs-jdbc.html) interface
- Consolidate various data streams provided by messaging queues such as Apache [Kafka](https://www.elastic.co/guide/en/logstash/5.4/plugins-outputs-kafka.html), [RabbitMQ](https://www.elastic.co/guide/en/logstash/5.4/plugins-outputs-rabbitmq.html), [Amazon SQS](https://www.elastic.co/guide/en/logstash/5.4/plugins-outputs-sqs.html), and [ZeroMQ](https://www.elastic.co/guide/en/logstash/5.4/plugins-outputs-zeromq.html)

<br>

<br>

## Easily Enrich Everything

- Get better knowledge from better data
  - **Clean** and **transform** data during ingestion so you can gain **insights** in near **real-time** at the time of indexing or output
  - Logstash provides various aggregation and mutation capabilities along with **pattern matching**, **geo mapping**, **dynamic lookup** features, and more
