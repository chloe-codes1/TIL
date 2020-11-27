# Redis Commands

> 자주 쓰는 Redis 명령어 정리해요

<br>

<br>

### 1. GET

- Key의 Value를 가져오는 명령어
- 만약 Key가 존재하지 않으면, **nil**을 return 한다

<br>

<br>

### 2. SET

- String value를 갖는 Key를 SET 하는 명령어

- 만약 이미 value 값이 설정된 Key라면 overwrite 한다

<br>

#### Options

```bash
SET key value [EX seconds|PX milliseconds|KEEPTTL] [NX|XX] [GET]
```

- `EX seconds`
  - Expire time을 설정할 수 있음 (초 단위)
- `PX milliseconds`
  - Expire time 설정 (millisecond 단위)
- `NX`
  - 해당 Key가 **존재하지 않을 때**에만 SET 하는 설정
- `XX`
  - 해당 Key가 **존재할 때**에만 SET 하는 설정

- `KEEPTTL`
  - 해당 Key가 갖고있는 TTL을 유지하도록 설정
- `GET`
  - 이미 Key가 존재하면, 
    - 설정된 Value 값을 return
  - 존재하지 않은 Key면,
    - **nil**을 Return

<br>

#### Return value

- Key가 정상적으로 SET되면 **OK** 를 return

<br>

#### Examples

```bash
redis> SET haha "hoho"
OK
redis> GET haha
hoho 
```

<br>

<br>

### 3. GETSET

- 