# Docker Commands

<br>

<br>

## Summary of Docker Commands

> Organizing because I keep forgetting...

<br>

### Create container

```bash
docker container create [options] [image name] [command] [parameters] 
```

<br>

### Run container

```bash
docker container run [options] [image name] [command] [parameters]
```

- `-d` : runs on background

<br>

### Start container

```bash
docker container start [container name]
```

- Change `start` to `restart` for restart

<br>

### Stop container

```bash
docker container stop [container name]
```

<br>

### Pause container

```bash
docker container pause [container name]
```

<br>

### Unpause container

```bash
docker container unpause [container name]
```

<br>

### Remove container

```bash
docker container rm [container name]
```

<br>

### Check the log

```bash
docker container logs -t webserver
```

- `realtime` : add `-f` after -t!

<br>

### Check container stats

```bash
docker container stats [container name]
```

<br>

### Check process status

```bash
docker ps -a
```

<br>

### Connect to container

```bash
docker exec -it [container ID] sh
```

<br>

### List images

```bash
docker image ls
```

or

```bash
$ docker images
REPOSITORY                                                            TAG               IMAGE ID       CREATED        SIZE
docker/getting-started                                                latest            021a1b85e641   4 weeks ago    27.6MB
lambci/lambda                                                         build-python3.8   91a48d7f8dd1   6 weeks ago    1.95GB
alpine                                                                latest            d6e46aa2470d   2 months ago   5.57MB
```

<br>

### Remove image(s)

```bash
docker image rm [OPTIONS] IMAGE [IMAGE ...]
```

- For IMAGE, write the IMAGE ID found with the `docker image ls` command

<br>

<br>

<br>

## Docker system prune

> Let's delete unused data

<br>

```bash
docker network prune
docker volume prune
docker container prune
docker image prune
docker system prune  # Remove all unused containers, networks, images (both dangling and unreferenced), and optionally, volumes.
``` 
