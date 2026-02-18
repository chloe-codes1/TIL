# How Kubernetes works

> Reference: [Revisiting Kubernetes Pod internals from Container basics](https://speakerdeck.com/devinjeon/containerbuteo-dasi-salpyeoboneun-kubernetes-pod-dongjag-weonri)

<br>

<br>

## What is Container?

- A Container is a **Process** that runs in an **isolated environment**

<br>

<br>

### Key principles of how containers implement an isolated environment

#### 1. Root directory isolation (`chroot`)

- **chroot**

  ```shell
  $ chroot <NEWROOT> <COMMAND>
  ```

  - A command to run a process (command) isolated with the input path (New root path) as the root directory

<br>

#### 2. Linux namespaces

- A Linux kernel feature for isolating system resources between processes

  ```shell
  $ lsns -p <pid>
  ```

- **unshare**

  - A command that can run a process with specific `namespaces` isolated

  - ex)

    ```shell
    # Run /bin/bash process with mount namespace isolated (-m)
    $ unshare -m /bin/bash

    # Run /bin/bash process with mount namespace(-m) and ipc namespace(-i) isolated
    $ unshare -m -i /bin/bash
    ```

<br>

#### 3. Mount (`mnt`) namespace

- **mount**

  - In Unix-based systems, mounting is the act of connecting a file system to a specific directory in the **file tree** starting from the `root directory (/)` in order to access that file system

    ```shell
    mount -t <type> <device> <dir>
    ```

  - ex)

    ```shell
    # Mount tmpfs (temporary file storage) to the "/root/test" path
    $ mount -t tmpfs tmpfs /root/test
    ```

- **mount namespace**

  - Allows processes to have different `mount points` from each other

<br>

#### 4. Process ID (pid) namespace

- A Container is a **Process** that runs in an **isolated environment**
  - Inside the container, it looks like a standalone VM, but from outside the container (host), it is just a single process
  - For the same process,
    - The PID seen from the host and the PID seen inside the container are different
- The first process executed (`entrypoint`) in a container with an isolated PID namespace always has **PID=1**

<br>

#### 5. Inter-Process Communication (ipc) namespace

- Isolates **System V** based inter-process communication
  - **System V IPC**
    - `shared memory (shm)`
    - `semaphore`
      - A method for controlling access to shared resources by multiple processes or threads
        - A process synchronization technique for concurrent processing
    - `POSIX message queue`
      - /proc/sys/fs/mqueue
      - A newer version of System V message queues
        - Although the function names and types differ, they perform similar tasks
        - More intuitive and easier to use than System V based message queue functions
  - IPC objects are only visible to processes within the same IPC namespace

<br>

#### 6. Network (net) namespace

- Isolates network interfaces, routing, and firewall rules

- ex)

  ```sh
  # Create a network namespace named "chloe-ns"
  $ ip netns add chloe-ns
  $ ip netns list
  chloe-ns
  ```

  ```sh
  # Create a virtual ethernet interface pair (veth1, veth2)
  # "veth1" is created in chloe-ns, "veth2" is created in PID 1's network namespace
  $ ip link add veth1 netns chloe-ns type veth peer name veth2 netns 1
  ```

- Docker's container network architecture
  - Containers have their network namespace isolated from the host
    - A `veth peer` is created to connect between host and container
    - The host's veth is connected to the `docker bridge`, and when communicating outside the container, traffic goes through the `bridge`

<br>

#### 7. Unix Time-Sharing (uts) namespace

- What is `Unix Time-Sharing`?
  - Originated from the concept of sharing computing resources with other users
  - When multiple users are using the same machine but want to make it appear as if they are using different machines, a space is created to isolate **hostnames**

<br>

#### 8. User ID (user) namespace

- Maps the `uid` on the host differently from the `uid` in the container
- Docker containers do not isolate the **user namespace** by default
  - *This means the container's user can exercise nearly the same uid privileges as the host!*
  - **Why Docker does not isolate the user namespace**
    - **Compatibility issues** with `PID` and `Network namespace` **sharing features**
    - **Compatibility issues** with external volumes or drivers that do not support user mapping
    - **Complexity** of ensuring that a user in an isolated `user namespace` has access to files bound by the host, from the actual host uid the user is mapped to
    - Although the container root in a non-isolated `user namespace` has nearly equivalent privileges to the host root, it does not mean full root privileges
  - *Kubernetes also does not yet support `user namespace` isolation*
  - **When not using `user namespace` isolation**
    - Restrict so that only trusted users can run the container runtime (ex. Docker)
    - Ensure that container processes do not run as the **root user**
      - Specify them to run with a particular UID and GID
    - Do not mount host directories for direct access by the container
  - *Kubernetes provides security settings based on the same principles*

<br>

#### 9. Control group (cgroup)

- A Linux kernel feature that can limit and isolate **resource allocation** for `Process groups`
  - `CPU`
    - ex) Limit CPU usage
  - `Memory`
    - ex) Limit memory usage
  - `Network`
    - ex) Set network traffic priority
  - `Disk`
    - ex) Provide statistics on disk usage

<br>

#### `Wrap-up`: Key principles of how containers implement an isolated environment

- A Container is a **process** that runs in an **isolated environment**
- **Isolated environments** for processes are implemented through `namespaces`
- Process **resource usage** is **limited** through `cgroups`

<br>

<br>

## What is Kubernetes Pod?

- The **smallest deployable object unit** in Kubernetes
- A group consisting of one or more `containers`

<br>

### Pod is the "smallest deployable object unit"

K8s applications are deployed in `pod` units, and `pods` are deployed by various types of resources

- `Job`
  - Manages pods that run once and terminate when the task is complete
- `ReplicaSet`
  - Guarantees that a specified number of pods are running
- `DaemonSet`
  - Manages pods that run exactly one per node
- `StatefulSet`
  - Manages pods that run **stateful applications**
- `Deployment`
  - Manages deployment of updates for Pods and ReplicaSets

*A Pod is the most **fundamental unit** that is **created** and **managed** in Kubernetes!*

<br>

<br>

### Pod is a group of one or more containers

- A Pod can contain one or more containers
  - Pods running a single container
  - Pods running multiple containers

<br>

#### Cases where a Pod consists of multiple containers

- One **Primary Container** that serves as the main role
- One or more **Sidecar Containers**
  - Containers that run to **complement** the Primary Container
    - ex) monitoring, logging, etc.

<br>

#### It is recommended to run a single process per container

- **Why?**
  - As mentioned earlier, a Container is a **process** that runs in an **isolated environment**
  - The first process executed in an isolated PID namespace has `pid=1`
  - In other words, **the state of the first process executed in a Container** == **the lifetime of the Container**!
- **If multiple processes are running inside a container?**
  - Even if the container is running, the execution state of processes other than the main process cannot be guaranteed
  - In other words, **the state of processes running in a Container** != **the state of the Container**
- **If a specific container in a Kubernetes pod terminates?**
  - Kubernetes restarts the container according to the declared `restartPolicy`
    - `restartPolicy` options
      - Always
      - OnFailure
      - Never

<br>

#### Criteria for composing a Pod

- Must the containers run on the same node?
  - Containers in the same pod always reside on the same node!
- Do the containers need to be **horizontally scaled** by the same count?
  - Pod unit == unit of scaling!
- Must the containers be deployed together as a single group?

<br>

#### Isolation between containers in a Kubernetes Pod

- When examining containers on the node where a Pod is running,
  - `cgroup namespace` and `user namespace` are not separately isolated
  - `mnt`, `uts`, `pid` namespaces are isolated per container
    - They are not shared even within the same pod!
  - `ipc`, `net` namespaces are **shared** between containers in the pod
    - `shared memory` and other IPC between container processes is possible
    - Containers share the same IP address and port (beware of conflicts)

**What is a Pause Container?**

- The Pause container creates and maintains the isolated IPC and Network namespaces
  - The remaining containers share and use those namespaces
    - This prevents issues where a user-launched container terminates abnormally and causes problems in namespaces shared across all containers!
- It simply runs an infinite loop and terminates when receiving `SIGINT` or `SIGTERM`
  - `SIGINT`
    - An interrupt signal from the keyboard
      - The signal sent when pressing [CTRL] + [C]
    - Stops execution
  - `SIGTERM`
    - Short for Terminate, a signal that requests graceful termination
    - The default signal of the kill command
- It serves the role of **Zombie Process Reaping**
  - When PID namespace sharing is enabled!

<br>

#### PID namespace sharing in Kubernetes

- When there is a risk of **zombie processes** occurring in individual containers, you can enable the Kubernetes `PID namespace sharing` option to delegate the **zombie process reaping** role to the **Pause container**
- How to enable
  - Set `spec.template.spec.shareProcessNamespace: true` in the pod yml file

<br>

<br>

## Wrap-up

### Concepts of Kubernetes Pod

<br>

#### What is a Pod?

- The **smallest deployable object unit** in Kubernetes
  - Pods are deployed by various types of resources (`Job`, `ReplicaSet`, etc.)
- A group of one or more containers
  - Pods running a single container
  - Pods running multiple containers
    - `Primary Container`
    - `Sidecar containers`

<br>

#### Running multiple processes in a single container is not recommended

- Because even if the container is running, the running state of processes other than the main process cannot be guaranteed!

<br>

#### When a specific container in a Kubernetes Pod terminates, `Kubelet` restarts the container according to the `restartPolicy`

<br>

#### Criteria for deciding how to compose a Pod

- Must the containers run on the **same node**?
- Do the containers need to be **horizontally scaled** by the **same count**?
- Must the containers be deployed together as a single group?

<br>

#### Isolation between containers in a Pod

- Namespaces shared with the host
  - `cgroup`
  - `user`
- Namespaces shared between containers in the same pod
  - `ipc`
  - `net`
- Namespaces isolated per container
  - `mount`
  - `uts`
  - `pid`
    - pid namespace sharing is optional!

<br>

#### What is a Pause Container?

- Creates and maintains `IPC` and `Network namespaces` to be shared among containers
- When `PID namespace` is shared, it also performs the **zombie process reaping** role
