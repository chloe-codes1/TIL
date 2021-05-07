# How Logstash Works

> Reference: [elastic docs](https://www.elastic.co/guide/en/logstash/current/pipeline.html#:~:text=The%20Logstash%20event%20processing%20pipeline,to%20use%20a%20separate%20filter.)

<br>

<br>

### Before getting started

- Logstash의 event processing pipeline은 3가지 단계로 구성되어 있다
  - `inputs` -> `filters` -> `outputs`
    - **Inputs**는 event를 생성하고, 
    - **Filters**는 그것을 수정하며,
    - **Outputs**는 전송한다

- **Inputs**와 **outputs** 는 수집되거나 pipeline에 존재하는 data를 `filter` 없이 **암호화** 혹은 **복호화** 할 수 있도록 하는 **codec**을 지원한다

<br>

<br>

### Inputs

Inputs를 사용해서 **Logstash** 에 data를 적재할 수 있다. 빈번하게 사용되는 inputs는 아래와 같다.

- **file**
  - filesystem로부터 file을 읽어들인다
  - UNIX command `tail -0F` 와 유사하다
- **syslog**
  - syslog message를 위해 **514 port**를 listen 한다
  - RFC3164를 따라서 message를 parsing 한다
- **redis**
  - Redis channel과 list를 활용하여 server로부터 읽어들인다 
- **beats**
  -  [Beats](https://www.elastic.co/downloads/beats) 로 부터 전송된 event들을 가공한다

<br>

*계속 추가중..*

