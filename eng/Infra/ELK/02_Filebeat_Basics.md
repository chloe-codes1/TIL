# Filebeat Basics

> Let's learn about Filebeat
>
> Reference: [filebeat docs](https://www.elastic.co/guide/en/beats/filebeat/6.0/filebeat-overview.html)

<br>

<br>

## What is Filebeat?

<br>

### Filebeat

- A lightweight `Producer` for **forwarding** and **centralizing** **log data**
- `Filebeat`, installed as an agent on the server,
  1. **Monitors** a directory or specific files,
  2. **Collects** log events, and
  3. Forwards them to `Elasticsearch` or `Logstash` for **indexing**

<br>

![image-20200911205327354](../../kor/images/image-20200911205327354.png)

<br>

<br>

### How it works?

1. When Filebeat starts, it has one or more **prospectors** watching the **log data** specified in the configuration
2. Each time an event occurs in the specified **log file**, `Filebeat` starts a **data harvester**
3. Each **harvester** watching a single **log file** reads new log data and sends it to `libbeat`
4. `libbeat` aggregates events and sends the aggregated data to the output configured in the `Filebeat` settings

<br>

<br>

## How Filebeat works (in detail)

<br>

- Filebeat is composed of `prospectors` and `harvesters`
  - These two components work together to track files and forward **event data** to the specified destination

<br>

### What is a `harvester`?

- A **Harvester** is responsible for reading the contents of a file
- It reads each file line by line and sends the contents
- One Harvester starts and finishes work per file
  - That is, while the Harvester is running, the **file descriptor** is open and the harvester continuously reads the file
    - `Cons`
      - There is a disadvantage of occupying disk space until the harvester finishes its work!

<br>

### What is a `prospector`?

- A **Prospector** is responsible for **managing** **harvesters** and **finding** resources to read

- If the `input` is **log**, the prospector:

  1. Finds all files in the corresponding path and
  2. Runs a **harvester** on each file

- An example of configuring `Filebeat` to read all **log files** from specified paths:

  - ex)

    ```yml
    filebeat.prospectors:
    - type: log
     paths:
      - /var/log/*.log
      - /var/path2/*.log
    ```

- Filebeat currently supports `log` and `stdin` as **prospector** types

- Filebeat **prospectors** can only read **local files**!

  - They cannot connect to a remote host to read files or logs!!

<br>

### How does Filebeat keep the state of files?

- Filebeat tracks the **state** of each file and saves it to a registry file on disk
  - The **state** is used to:
    1. **Remember** where the harvester was last reading, and
    2. Guarantee that all logs have been sent
- While Filebeat is running, **state** information is stored in **memory** by the `prospector`
- When Filebeat restarts:
  1. The information stored in the registry file is used to reset the **state**, and
  2. Filebeat runs each `harvester` from the position where it was last executing

<br>
