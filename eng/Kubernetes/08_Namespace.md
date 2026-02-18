# Namespace

<br/>

## What is a Namespace?

- A Kubernetes namespace provides a `scope` for object names
- Instead of placing all resources in a single namespace, they can be divided into multiple namespaces
- Separate namespaces allow the same resource name to be used multiple times across different namespaces

<br/>

## Why Namespaces are needed

- Using multiple namespaces allows complex systems with many components to be separated into smaller `individual groups`
  - Used to `isolate resources` in `multi-tenant` environments
  - Resource names only need to be unique within a namespace
    - Two different namespaces can have resources with the same name
  - Most resource types belong within a namespace, but some do not
    - One of them is the `node`, which is `global` and does not belong to a single namespace
- Namespaces can be used to separate unrelated resources into non-overlapping `groups`
  - If multiple users or groups are using the same Kubernetes cluster and each manages their own resources, they should use their own unique namespaces
    - This way, there is no need to be careful about modifying or deleting other users' resources!
- In addition to isolating resources, namespaces are also used to `allow` specific users access to designated resources and to `limit` the computing resources available to individual users

<br/>

## Creating Namespaces and Managing Objects

### Creating a Namespace

> Since a namespace is a Kubernetes resource, it can be created by submitting a YAML file to the Kubernetes API server
>

#### 1. Creating a namespace from a YAML file

ex) Creating a namespace named chloe

Create the `chloe-namespace.yaml` file

```yaml
apiVersion: v1
kind: Namespace
metadata:
 name: chloe
```

Send the file to the Kubernetes API server using the kubectl command

```bash
kubectl create -f choe-namespace.yaml
```

<br/>

#### 2. Creating a namespace with the `kubectl create namespace` command

You can quickly create a namespace using the `kubectl create namespace` command

ex)

```bash
kubectl create namespace chloe
```

<aside>
Most object names must comply with the rules specified in `RFC1035`

This means they can contain letters, numbers, dashes (-), and dots (.)!

However, `namespaces` and some other resources cannot contain dots (.)!

Why? Because they must not contain DNS address names!

</aside>

<br/>

## Understanding the isolation provided by Namespaces

Using namespaces allows you to separate objects into distinct groups and work with resources within a specific namespace, but `it does not provide isolation for running objects`

ex)

- When different users deploy pods in different namespaces, you might think that `those pods are isolated from each other and cannot communicate`, but **that is not necessarily the case!**
- Whether a namespace provides network isolation depends on the `networking solution` deployed with Kubernetes
- If the networking solution does not provide isolation between namespaces, and a pod in namespace A knows the IP address of a pod in namespace B, there are no restrictions on sending traffic such as HTTP requests to the other pod!

<br/>

### When using VPC CNI

> **Refer to [CNI plugin for Kubernetes networking over AWS VPC](https://github.com/aws/amazon-vpc-cni-k8s/blob/master/docs/cni-proposal.md)**
>
