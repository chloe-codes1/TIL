# Kubectl Commands

> `history | grep`을 멈추기 위한 정리

<br>

<br>

### Namespace

#### Namespace 보기

```shell
kubectl get namespace
```

#### Namespace 변경

```shell
kubectl config set-context --namespace=[namespace 이름]
```

<br>

### Execute pod

```shell
kubectl exec -it [pod 이름] [경로]
```

ex)

```shell
k exec -it prism-69b8c846c-gc9zj /bin/sh
```

- `kubectl` 명령어를 `k`로 **alias** 해놨다
- `/bin/sh`가 아니라 `/bin/bash`로 생성한 경우도 있으니 참고

<br>

### Delete 

#### Delete pod

```shell
kubectl delete pod [pod 이름]
```

### Force delete pod

```shell
kubectl delete pod [pod 이름] -grace-period=0 --force
```

- `-grace-period` option을 0으로 주면 즉시 삭제된다
- `--force` option을 통해 강제 삭제가 가능하다

<br>

### Log

#### Pod log 보기

```shell
kubectl logs -f [pod 이름]
```

#### Container 지정하여 log 보기

하나의 pod에 다수의 container가 떠있으면 `-c` option으로 container를 지정한다

```sh
kubectl logs -f [pod 이름] -c [container 이름]
```

<br>

### Events

#### Events 보기

```sh
kubectl get events
```

#### Events timestamp 순으로 보기

```sh
kubectl get events --sort-by=.meta.creationTimestamp
```