# Redis Commands

> Organizing frequently used Redis commands

<br>

<br>

### 1. GET key

- A command to retrieve the value of a key
- If the key does not exist, it returns **nil**

<br>

<br>

### 2. SET key value

- A command to SET a key with a string value

- If the key already has a value set, it overwrites it

<br>

#### Options

```bash
SET key value [EX seconds|PX milliseconds|KEEPTTL] [NX|XX] [GET]
```

- `EX seconds`
  - Can set the expire time (in seconds)
- `PX milliseconds`
  - Set the expire time (in milliseconds)
- `NX`
  - Setting to SET only when the key **does not exist**
- `XX`
  - Setting to SET only when the key **exists**

- `KEEPTTL`
  - Setting to keep the TTL that the key has
- `GET`
  - If the key already exists,
    - Returns the set value
  - If the key does not exist,
    - Returns **nil**

<br>

#### Return value

- Returns **OK** if the key is successfully SET

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

- SETs a value for the key and returns the previously stored value
- Returns **Error** if the key exists but has no stored string value

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

- Sets a **timeout** on the key
  - When the timeout expires, the key is automatically deleted
- The set timeout is cleared when the key's content is **deleted** or **overwritten**
  - The following commands clear the timeout:
    - DEL
    - SET
    - GETSET
    - All *STORE commands
  - That is, all other commands that **alter** values do **not change** the timeout
    - ex) The INCR command that increments a value does not affect the timeout
- The timeout can be cleared by converting the key to a persistent key through the PERSIST command
- Note that calling the EXPIRE command with a non-positive timeout **deletes** the key rather than expiring it!
  - The key event is del, not expired

<br>

#### Refreshing expires

- You can call the EXPIRE command on a key that already has an expire set to configure a new timeout
  - In this case, the `TTL (Time to Live)` is updated to the newly set value

<br>

#### Return value

- Returns **1** if the timeout is set
- Returns **0** if the key does not exist

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

- Returns the TTL (Time To Live) of the timeout set on the key
  - Returns **-2** if the key does not exist
  - Returns **-1** if the key exists but no expire is set

<br>

<br>

### 6. INCRBY key increment

- Increments the number stored at the key
- If the key does not exist, sets it to **0** before executing the increment

<br>

#### Return value

- Returns the incremented value

- Returns **Error** if the key has a value of the wrong type that cannot be converted to an integer

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

- Decrements the number stored at the key
- If the key does not exist, sets it to **0** before executing the decrement

<br>

#### Return value

- Returns the decremented value

- Returns **Error** if the key has a value of the wrong type that cannot be converted to an integer

<br>

#### Examples

```bash
redis> SET num "10"
OK
redis> DECRBY num 4
6
```

<br>

*More to be added*
