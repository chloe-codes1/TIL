# Install and config Redis on macOS

> Installing Redis on Mac with brew

<br>

<br>

### Install with `brew`

```shell
brew install redis
```

<br>

<br>

### Start, stop, restart with `brew services`

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

### Check connection with `redis-cli`

You can check the connection using the **PING** command

```shell
➜ redis-cli ping
PONG
```
