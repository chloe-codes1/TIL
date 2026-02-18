# Kubectl Commands

> A cheat sheet to stop doing `history | grep`

<br>

<br>

### Namespace

#### View Namespaces

```shell
kubectl get namespace
```

#### Change Namespace

```shell
kubectl config set-context --namespace=[namespace name]
```

#### Create Namespace

```sh
kubectl create namespace [namespace name]
```

<br>

### Execute pod

```shell
kubectl exec -it [pod name] -- [path]
```

ex)

```shell
k exec -it prism-69b8c846c-gc9zj -- /bin/sh
```

- `kubectl` command is **aliased** to `k`
- Note that some cases use `/bin/bash` instead of `/bin/sh`

#### Execute specific container

```sh
k exec -it [pod name] -c [container name] -- [path]
```



<br>

### Delete

#### Delete pod

```shell
kubectl delete pod [pod name]
```

#### Force delete pod

```shell
kubectl delete pod [pod name] -grace-period=0 --force
```

- Setting the `-grace-period` option to 0 deletes the pod immediately
- The `--force` option enables forced deletion

#### Fully shut down the Deployment

```sh
kubectl delete all --selector app=[APP_IDENTIFIER]
```

#### Delete Service Account

```sh
kubectl delete serviceaccount [service account name]
```

#### Delete Deployment

```sh
kubectl delete deploymnet [deployment name]
```



<br>

### Log

#### View Pod logs

```shell
kubectl logs -f [pod name]
```

#### View logs for a specific container

If multiple containers are running in a single pod, use the `-c` option to specify the container

```sh
kubectl logs -f [pod name] -c [container name]
```

<br>

### Events

#### View Events

```sh
kubectl get events
```

#### View Events sorted by timestamp

```sh
kubectl get events --sort-by=.meta.creationTimestamp
```

<br>

### Get commands w/ basic output

#### List all services

```sh
kubectl get services
```

#### List all pods in all namespaces

```sh
kubectl get pods --all-namespaces
```

#### List all pods in the current namespace w/ more detail

```sh
kubectl get pods -o wide
```

#### List all deployment in all namespaces

```
kubeclt
```
