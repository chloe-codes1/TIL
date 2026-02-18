# Cluster

<br/>

## What is a Cluster?

- When you deploy Kubernetes, you get a Cluster
- A Kubernetes Cluster is a set of worker machines called `nodes` that run containerized applications
- Every cluster has at least one `worker node`

<br/>

## Cluster Architecture

> At the hardware level, a Kubernetes Cluster consists of multiple nodes, which can be divided into two types
>
1. `Master Node`

   Runs the Kubernetes `Control Plane` which controls and manages the entire Kubernetes system

2. `Worker Node`

   Runs the actual deployed container applications

<br/>

## Control Plane

> The Control Plane `controls and operates the cluster`

It consists of the following components that can run on a single master node or be split and replicated across multiple nodes to `ensure high availability`

<br/>

### Kubernetes API Server

> The API Server is the component that exposes the Kubernetes API
>
Communicates with users and Control Plane components

#### kube-apiserver

- kube-apiserver is designed to `scale horizontally`
  - That is, it can be scaled by deploying more instances
- You can run multiple kube-apiserver instances and balance the traffic between them

<br/>

### Scheduler

> A component that detects newly created Pods with no assigned node and `selects a node to run them on`
>
- Responsible for the `deployment` of applications
  - `Assigns` each deployable component of an application to a `worker node`
- Factors considered for scheduling include
  - Individual/aggregate resource requirements
  - Hardware/Software policy constraints
  - Affinity & anti-affinity specifications
  - Data locality
  - Inter-workload interference
  - Deadlines

<br/>

### Controller Manager

> A component that `runs` controller `processes`
>
- Performs cluster-level functions such as replicating components, tracking worker nodes, and handling node failures
- Logically, each controller is a separate process, but to reduce complexity, they are compiled into a single binary and `run within a single process`

#### Controller Types

- `Node controller`
  - Responsible for notifying and responding when a node goes down
- `Job controller`
  - Watches for one-time Job objects and creates Pods to execute those jobs
- `Endpoints controller`
  - Connects Services and Pods
- `Service Account & Token controllers`
  - Creates default accounts and API access tokens for new Namespaces

<br/>

### etcd

> A reliable, key-value structured `distributed data store` that continuously stores the cluster configuration
>

<aside>
The components of the Control Plane maintain and control the cluster state, but they do not run applications.
That is done on the Nodes.

</aside>

<br/>

## Node

> Worker Nodes are systems that `run containerized applications`
>
> Running and monitoring applications, and providing services to applications, is performed by the following components
>

### Container Runtime

> Responsible for running containers
>

Supports `Docker`, `containerd`, `CRI-O`, or any software that implements the [Kubernetes CRI (Container Runtime Interface)](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-node/container-runtime-interface.md)

<br/>

### Kubelet

> Communicates with the API Server and manages containers on the node
>

- An agent that runs on each node in the cluster, managing containers to ensure they run within Pods
- Receives a set of `PodSpecs` through various mechanisms and manages containers to ensure they are running properly according to those Pod specs
- Does not manage containers that were not created through Kubernetes

<br/>

### Kube-proxy

> `Kube-Proxy` load-balances network traffic between application components
>
- A `network proxy` that runs on each node in the cluster, implementing the Kubernetes service concept
- Maintains and manages network rules on the node
  - These network rules allow network communication to pods from internal network sessions or from outside the cluster
