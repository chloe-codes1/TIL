# Redis Commands

> 자주 쓰는 Redis 명령어 정리해요

<br>

<br>

### 1. GET key

- Key의 Value를 가져오는 명령어
- 만약 Key가 존재하지 않으면, **nil**을 return 한다

<br>

<br>

### 2. SET key value

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

#### Examples

```bash
redis> SET haha "hoho"
OK
redis> GET haha
hoho 
```

<br>

<br>

### 3. GETSET key value

- Key에 value를 SET하고, 기존에 저장되어 있던 value를 return 한다
- Key만 있고 저장된 string value가 없으면 **Error** 를 return 한다

<br>

#### Examples

```bash
redis> del haha
1
redis> SET haha "hoho"
OK
redis> GETSET haha "yay"
hoho
redis> GET haha
yay
```

<br>

<br>

### 4. EXPIRE key seconds

- Key에 **timeout**을 설정한다
  - timeout이 만료되면, key는 자동으로 삭제된다
- 설정한 timeout은 key의 content가 **삭제**되거나 **overwrite**되면 해제된다
  - 아래의 command들은 timeout을 해제시킨다
    - DEL
    - SET
    - GETSET
    - 모든 *STORE commands
  - 즉, 다른 모든 value값을 **alter** 하는 command들은 timeout을 **변경시키지 않는다**
    - ex) value 값을 증가시키는 INCR command로 timeout은 변동되지 않는다
- Timeout은 PERSIST command를 통해 key를 persistent key로 변환하여 clear 될 수 있다
- EXPIRE command를 non-positive timeout으로 호출하면 해당 key는 expired되는 것이아니라 **삭제**되는 점을 유의하여야 한다!
  - Key event는 expired가 아니라 del된다

<br>

#### Refreshing expires

- 이미 expire가 설정되어있는 key에 EXPIRE command를 호출하여 timeout을 설정할 수 있다
  - 이 경우, `TTL (Time to Live)` 은 새로 설정된 값으로 update된다

<br>

#### Return value

- timeout이 설정되면 **1**을 return 한다
- key가 존재하지 않으면 **0**을 return 한다

<br>

#### Examples

```
redis> EXPIRE haha 10
1
redis> TTL haha
6
redis> del haha
0
redis> SET haha "hoho"
OK
redis> EXPIRE haha 10
1
redis> TTL haha
8
redis> SET haha "hohohoho"
OK
redis> TTL haha
-1
```

<br>

<br>

### 5. TTL key

- Key에 설정된 timeout의 TTL (Time To Live)을 return 한다
  - 만약 key가 없으면 **-2**를 return 한다
  - key는 존재하지만 expire가 설정되어 있지 않으면 **-1**을 return 한다

<br>

<br>

### 6. INCRYBY key increment

- Key에 저장된 숫자를 증가시킨다
- 만약 key가 존재하지 않으면, **0**을 설정한 후에 increment를 실행한다

<br>

#### Return value

- 증가된 value 값을 return 한다

- 만약 key가 integer로 바꿀 수 있는 string이 아닌 잘못된 type의 value를 갖고있으면, **Error**를 return한다

<br>

#### Examples

```bash
redis> SET num 10
OK
redis> INCRBY num 25
35
redis> SET string "10"
OK
redis> INCRBY string 5
15
redis> SET wrong "wrong value"
OK
redis> INCRBY wrong 10
ERR value is not an integer or out of range
```

<br>

<br>

### 7. DECRBY key decrement

- Key에 저장된 숫자를 감소시킨다
- 만약 key가 존재하지 않으면, **0**을 설정한 후에 값을 decrement를 실행한다

<br>

#### Return value

- 감소된 value 값을 return 한다

- 만약 key가 integer로 바꿀 수 있는 string이 아닌 잘못된 type의 value를 갖고있으면, **Error**를 return한다

<br>

#### Examples

```bash
redis> SET num "10"
OK
redis> DECRBY num 4
6
```

<br>

*계속 추가 중*
