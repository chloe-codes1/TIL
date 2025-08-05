# Getting Started with Docker

> Conquering Docker!!!!!!!
>
> References: [Book] Troubleshooting Docker

<br>

## Container and Docker

- Docker is an Open source project receiving tremendous attention
- It provides functionality to package applications as `lightweight containers` for **deployment** and **operation**
- **Docker Container** provides functionality to deliver applications in a **consistent** and standardized form like containers used in actual cargo ships!

<br>

### What is a Container?

![VM vs Container](../../../kor/images/image-20200802224306612.png)

- Container is technology that **encapsulates** applications to provide **independent operating environments**
  - Can be used as an alternative to Virtual Machines!
- Container is built on **Linux Container**, which is a **User Space Interface** for Linux Kernel's isolation features!
  - By providing powerful APIs and simple tools, Linux users can create and manage applications as containers
- Container differs from traditional `Hypervisor` in that OS running on Host machine share Linux kernel!
  - **Hypervisor** means?
    - Software that creates and operates Virtual Machines
  - In other words, even when running multiple containers on the same machine, all use the same Kernel
    - Therefore, it's **faster than VM** and has almost **no performance overhead**!

<br>

### OS Container

- OS Container is similar to VM
  - but, it differs in that it provides **user space isolation functionality** while **sharing the Kernel** of Host Machine OS
- Like VM, you can allocate **dedicated resources** to Container and install, configure, and operate applications and libraries
- OS Container is useful for **scalability testing**!
  - You can easily deploy multiple containers composed of various distributions, much **lighter** than VM
- Container is created through **images** or **templates** that define structure and contents
  - Therefore, when building development environments, it's easy to configure to have the same execution environment, version, and package environment as other Containers!
- Currently, various container technologies are available, among which suitable ones for OS Container include `LXC`, `OpenVZ`, `Docker`, `BSD Jail`, etc.

<br>

### Application Container

- While **OS Container** consists of multiple processes, **Application Container** packages and operates one service
  - Application container operates only one process
    - The process that operates is the application process, contrasting with **OS Container** running multiple services on one OS!
- Docker container uses a layer approach, which can **minimize duplication** and increase **reusability**
  - First operate a container for `base image` commonly used by all components,
  - Then add desired elements as separate layers to the file system on top of it
- Using layer-based file system allows easy rollback to previous layers at any desired time!
- Every time a `RUN` command specified in **Dockerfile** executes, a new layer is created in the container
- The main purpose of Application Container is to make various components constituting the application into **separate container-type packages**
  - Application components bundled in container units operate applications through interaction via APIs or services
    - This **distributed multi-component system** deployment approach is core to implementing `microservice architecture`!
      - This way
        - Developers can package applications in their desired container form,
        - IT teams can take full responsibility for deploying containers to various platforms for horizontal or vertical scaling

<br>

<br>

### OS Container vs Application Container

| OS Container                                      | Application Container                        |
| :------------------------------------------------ | -------------------------------------------- |
| Operate multiple services in one OS Container    | Operate one service in one Container        |
| Does not use layered file system                 | Based on layered file system                |
| ex) LXC, OpenVZ, BSD Jail                        | ex) Docker, Rocket                          |

<br>

<br>

### Learning Docker in Detail

- Docker combines various Linux Kernel features with file systems to compose images in **module** form
- Through composed images
  - You can freely configure application virtual environments,
  - Realize **WORA (Write-Once-Run-Anywhere)** principle
- Since applications can be simplified to the level of operating one process
- You can easily build **distributed systems** where multiple processes collaborate,
- And support high **scalability**
- Docker provides four important characteristics for application development
  1. Autonomy
  2. Decentralization
  3. Parallelism
  4. Isolation

- Docker containers can reproduce identical behavior anywhere - development machines, bare metal servers, virtual machines, data centers, etc.
  - From application designer's perspective, all operational matters can be left to **DevOps** team, allowing full concentration on development..!
    - This enables modularizing team workflow, increasing productivity and efficiency

<br>

#### Docker and VM

- Docker provides application-level isolation and security features for applications operating in Container by sharing OS
  - Despite providing strong **isolation** and **security features** through perfect **abstraction** of OS layer, Docker's resource usage is considerably less than VM, making performance and efficiency excellent!

<br>

<br>

### Benefits of Docker

Using Docker Container in Microservice Architecture has the following advantages

- **Fast application deployment**
  - Containers contain only application-related parts, so they are small and can be **quickly deployed** with minimal runtime
- **Portability**
  - `Application` and `operating environment` (dependency information including libraries used by application) can be bundled into one Docker Container, and such containers are **independent** of OS version or deployment model
  - Docker Containers can be transmitted to machines capable of operating docker and executed immediately without worrying about compatibility issues
- **Easy sharing**
  - Pre-made container images can be uploaded to public repos or internal private repos for easy sharing
- **Low resource usage**
  - Docker images are small and use fewer resources when deploying new applications by utilizing other containers
- **Reusability**
  - It's easy to continue versioning Docker containers and easy to roll back to previous versions anytime
  - Since components in existing layers can be reused, tremendous **lightweight** is possible

<br>

<br>

### Lifecycle of Docker Container

<br>

![image-20200809005844880](../../../kor/images/image-20200809005844880.png)

<br>

#### 1. Build

- Write all commands needed to package Container in `Dockerfile` and use it to **build** Docker image

  ```bash
  docker build
  ```

- To tag an image, use **-t** option

  ``` bash
  docker build -t username/image name
  ```

- When `Dockerfile` exists in a different path than current directory, specify Dockerfile path with **-f** option

  ``` bash
  docker build -t username/image name -f /path/Dockerfile
  ```

<br>

#### 2. Run

- After creating image, execute **docker run** command to deploy Container

  ``` bash
  docker run
  ```

- To check the status of running container, execute **docker ps** command

  ```bash
  docker ps
  ```

  - This command shows the list of currently active containers

- To pause all processes, execute **docker pause** command

  ```bash
  docker pause
  ```

  - This command uses `cgroups freezer` to pause all processes currently running in the container
    - Internally sends **SIGSTOP** signal
  - Using this command, you can pause and resume processes anytime

- To execute one or more containers in stop state, use **docker start** command

  ```bash
  docker start
  ```

<br>

#### 3. Stop / Kill

- When done using Docker, stop or kill it

  ```bash
  docker stop
  ``` 
