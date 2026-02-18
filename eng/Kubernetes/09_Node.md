# Node

<br/>

## What is a Node?

- Kubernetes runs workloads by placing containers in pods and running them on nodes
- A node can be a `virtual or physical machine` depending on the cluster
- Each node is managed by the `control plane` and contains the services necessary to run pods
- The components of a node include `kubelet`, `kube-proxy`, and the `container runtime`

    -> Refer to [Cluster](https://www.notion.so/Cluster-ac3f9a7fde0f46b7b1687132f066b511)!

<br/>

## Managing Nodes

> There are two main ways to add a node to the Kubernetes API server
>
1. Self-registration to the control plane via the node's `kubelet`
2. A user (or another user) manually adds the `node object`

After registration via kubelet or node object, the control plane `verifies that the created node object is valid`

ex)

```json
{
  "kind": "Node",
  "apiVersion": "v1",
  "metadata": {
    "name": "10.240.79.157",
    "labels": {
      "name": "my-first-k8s-node"
    }
  }
}
```

<br/>

### Flow

- Kubernetes internally creates a `node object`
- Kubernetes checks whether the `kubelet` is registered with the API server matching the node's `metadata.name` field
  - If the node is healthy,
    - It becomes eligible to run pods
  - If it is not healthy,
    - The node is ignored for all cluster activities until it becomes healthy

<aside>
Kubernetes `retains` invalid `node objects` and `checks whether the node is healthy`

To stop the health check, the user or a controller must explicitly delete the node object

</aside>

<br/>

### Uniqueness of Node names

- Two nodes cannot have the same name at the same time
  - Kubernetes assumes that resources with the `same name` are the `same object`!
- For nodes, it is implicitly assumed that instances using the same name have the `same state` (ex. network settings, root disk contents) and the `same attributes` such as node labels
  - If an instance is modified without changing its name, this can lead to inconsistencies!
  - Therefore, when replacing or updating a node, you must first `remove the existing node object from the API server` and re-add it after the update!

<br/>

## Node Status

> A node's status includes the following information

1. Addresses
2. Conditions
3. Capacity and Allocatable
4. Info
>

Check node status and details using kubectl

```bash
kubectl describe node <NODE_NAME>
```

The information output by the above command includes addresses, conditions, capacity and allocatable, and info as described below.

<br/>

### Addresses

> The `addresses` field varies depending on the cloud provider or bare metal setup
>
- HostName
  - The hostname as reported by the node's kernel
  - Can be overridden via the `-hostname-override` parameter
- ExternalIP
  - Typically, the node's IP address is externally routable
  - That is, it is accessible from outside the cluster
- InternalIP
  - Typically, the node's IP address is only routable within the cluster

<br/>

### Conditions

> The `conditions` field describes all `Running` state nodes
>

| Node Condition | Description |
| --- | --- |
| Ready | True if the node is healthy and ready to accept pods, False if the node is unhealthy and not accepting pods, Unknown if the node controller has not received a response from the node within the last node-monitor-grace-period (default 40 seconds) |
| DiskPressure | True if there is pressure on disk size, meaning disk capacity is low, False otherwise |
| MemoryPressure | True if there is pressure on node memory, meaning node memory is low, False otherwise |
| PIDPressure | True if there is pressure on processes, meaning there are many processes on the node, False otherwise |
| NetworkUnavailable | True if the network for the node is not correctly configured, False otherwise |

<br/>

### Capacity and Allocatable

- Represents the `available resources` on a node
  - Resources include CPU, memory, and the maximum number of pods that can be scheduled on the node
- The capacity block fields represent the `total amount of resources on the node`
  - The allocatable block represents the amount of node resources available for regular pods

<br/>

### Info

- Describes general information about the node such as `kernel version`, `Kubernetes version` (kubelet and kube-proxy versions), `container runtime details`, and `the operating system` the node uses
  - This information is collected by kubelet from the node and sent to the Kubernetes API
