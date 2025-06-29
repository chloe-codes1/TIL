# Install and config Redis on macOS

> mac에 brew로 redis 설치하기

<br>

<br>

### `brew`로 설치하기

```shell
brew install redis
```

<br>

<br>

### `brew services`로 start, stop, restart 하기

#### start

```shell
brew services start redis
```

<br>

#### stop

```shell
brew services stop redis
```

<br>

#### restart

```shell
brew services restart redis
```

<br>

<br>

### `redis-cli`로 connection 확인하기

**PING** 명령어로 확인할 수 있다

```shell
➜ redis-cli ping
PONG
```
