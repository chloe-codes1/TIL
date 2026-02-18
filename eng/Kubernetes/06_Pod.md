# Pod

<br/>

## What is a Pod?

> A Pod is the `smallest deployable computing unit` that can be created and managed in Kubernetes
>
- A Pod is a group of one or more containers
  - Kubernetes does not deal with individual containers directly
  - Instead, it uses the concept of multiple co-located containers, and this group of containers is called a `Pod`
- A Pod is a group of `one or more tightly related containers` that run together in the same Linux namespace on the same worker node
  - Each Pod is a `logically distributed machine` with its own IP, hostname, processes, etc.
  - An application can be a single process running in a single container, or it can consist of a main application process running in one container and additional helper processes in separate containers
- When a Pod has multiple containers, all containers always run on a single worker node and never span across multiple worker nodes

<br/>

### When multiple containers in a Pod are needed

> When grouping containers into a Pod (to decide whether to put two containers in a single pod or in two separate pods), you can ask the following questions
>
1. Must the containers run together, or can they run on different hosts?
2. Do multiple containers together represent a single component, or are they individual components?
3. Should the containers be scaled together or individually?

Fundamentally, unless there is a specific reason to group containers into a single Pod, it is better to run containers in separate Pods

<aside>
Containers should not run multiple processes.
If there is no need to run containers on the `same machine`, they should not be placed in the same Pod with multiple containers.

</aside>

<br/>

## Defining a Pod

### Key parts of a Pod definition

- `Metadata`
  - Contains the name, namespace, labels, and other information about the Pod
- `Spec`
  - Contains the actual specification of the Pod itself, such as Pod containers, volumes, and other data
- `Status`
  - Contains current information about the Pod, including Pod status, description and details of each container, internal IP of the Pod, and other basic information

ex)

```yaml
apiVersion: v1
kind: Pod
metadata:
 name:kubia-mannual
spec:
 containers:
 - image: luksa/kubia
  name: kubia
  ports:
  - containerPort: 8080
   protocol: TCP
```

<br/>

### Specifying container ports

- Specifying ports in the Pod definition is merely informational
  - Omitting them does not affect whether other clients can connect through the port
- However, explicitly defining ports has the advantage that anyone using the cluster can quickly see which ports a Pod exposes
  - Additionally, explicitly defining ports allows you to assign names to them for convenient usage

<br/>

## Organizing Pods with Labels

> Labels enable the organization of Pods and other Kubernetes objects
>
- Labels are a feature that allows you to `organize` Pods and all other Kubernetes resources
- Labels are `key-value` pairs registered on resources, and these pairs are used when selecting resources with a label selector
  - Resources are filtered based on whether they contain the labels specified in the selector
- You can have as many labels as you want, as long as the label `key` is `unique`
- Typically labels are attached when creating a resource, but you can also add labels later or modify existing values

<br/>

### Constraining Pod scheduling with Labels and Selectors

- The overall idea of Kubernetes is to hide the actual infrastructure from the applications running on top of it, so you typically would not want to specify exactly which node a Pod should be scheduled on
  - Doing so would couple the application to the infrastructure
- Instead, Kubernetes lets you describe the required node requirements and lets Kubernetes select a node that satisfies those requirements
  - This is possible through `node labels` and `label selectors`

<br/>

#### 1. Using Labels to categorize worker nodes

> You can attach `labels` to all Kubernetes objects including nodes.
> Typically, when adding a new node to a cluster, you classify the node by labeling it with the hardware it provides or other useful information for pod scheduling
>

ex)

```bash
kubectl label node [node] gpu=true
```

<br/>

#### 2. Scheduling Pods to specific Nodes

> When you need to deploy a new Pod that requires a GPU, to request the scheduler to select a node that provides a GPU, you need to add a `node selector` to the Pod's YAML file
>

ex)

```yaml
apiVersion: v1
kind: Pod
metadata:
 name: kube-gpu
spec:
 nodeSelector:
  gpu: "true"
 containers:
 - image: luksa/kubia
  name: kubia
  ports:
  - containerPort: 8080
   protocol: TCP
```

With this configuration, the scheduler will select from nodes that have the `gpu=true` label

<br/>

## Keeping Pods stable

### Liveness Probe

- Kubernetes can check whether a container is alive through a `liveness probe`
- You can specify a liveness probe for each container in the Pod's spec
- Kubernetes periodically executes the probe, and if the probe fails, it `restarts the container`

<br/>

### Probe execution mechanisms

> Kubernetes uses three mechanisms to execute probes on containers
>
1. `HTTP GET Probe`
    - Performs an HTTP GET request to a specified IP address, port, and path
    - If the probe receives a response and the response code is 2xx or 3xx, the probe is considered successful
    - If it returns an error code or does not respond at all, the probe is considered failed and the container is restarted
2. `TCP Socket Probe`
    - Attempts a TCP connection to a specified port of the container
    - If the connection succeeds, the probe is successful; otherwise, the container is restarted
3. `Exec Probe`
    - Executes an arbitrary command inside the container and checks the exit status code
    - If the status code is `0`, the probe is successful
    - All other codes are considered failure

ex)

```yaml
apiVersion: v1
kind: Pod
metadata:
 name: kube-liveness
spec:
 containers:
 - image: luksa/kubia-unhealthy
  name: kubia
  livenessProbe:
   httpGet:
    path: /
    port: 8080
```

In the configuration above, the pod descriptor defines an `httpGet` liveness probe that Kubernetes periodically sends an HTTP GET request to the `"/"` path on port 8080 to verify that the container is functioning properly
