# How Logstash Works

> Reference: [elastic docs](https://www.elastic.co/guide/en/logstash/current/pipeline.html#:~:text=The%20Logstash%20event%20processing%20pipeline,to%20use%20a%20separate%20filter.)

<br>

<br>

### Before getting started

- Logstash's event processing pipeline consists of 3 stages
  - `inputs` -> `filters` -> `outputs`
    - **Inputs** generate events,
    - **Filters** modify them, and
    - **Outputs** transmit them

- **Inputs** and **outputs** support **codecs** that enable **encryption** or **decryption** of data being collected or residing in the pipeline without a `filter`

<br>

<br>

### Inputs

You can load data into **Logstash** using Inputs. Frequently used inputs include the following:

- **file**
  - Reads files from the filesystem
  - Similar to the UNIX command `tail -0F`
- **syslog**
  - Listens on **port 514** for syslog messages
  - Parses messages following RFC3164
- **redis**
  - Reads from the server using Redis channels and lists
- **beats**
  - Processes events sent from [Beats](https://www.elastic.co/downloads/beats)

<br>

*More to be added..*

