# Docker Basics

<br>

<br>

## Docker 명령어 정리

> 자꾸 잊어서 정리...

<br>

### Create container

```bash
$ docker container create [옵션] [이미지 이름] [명령] [매개변수] 
```

<br>

### Run container

```bash
$ docker container run [옵션] [이미지 이름] [명령] [매개변수]
```

- `-d` : runs on background

<br>

### Start container

```bash
$ docker container start [컨테이너명]
```

- `start`를 `restart` 로 바꾸면 재시작

<br>

### Stop container

```bash
$ docker container stop [컨테이너명]
```

<br>

### Pause container

```bash
$ docker container pause [컨테이너명]
```

<br>

### Unpause container

```bash
$ docker container unpause [컨테이너명]
```

<br>

### Remove container

```bash
$ docker container rm [컨테이너명]
```

<br>

### Check the log

```bash
$ docker container logs -t webserver
```

- `realtime` : -t 뒤에 `-f` 붙이기!

<br>

### Check container stats

```bash
$ docker container stats [컨테이너명]
```

<br>

### Check process status

```bash
$ docker ps -a
```

<br>

### Connect to container

```bash
$ docker exec -it [container ID] sh
```



<br>

## Docker system prune

> 안 쓰는 data 는 지우자

<br>

```bash
$ docker network prune
$ docker volume prune
$ docker container prune
$ docker image prune
```

