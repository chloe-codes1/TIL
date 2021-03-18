# How Kubernetes works

> Reference: [Container부터 다시 살펴보는 Kubernetes Pod 동작 원리](https://speakerdeck.com/devinjeon/containerbuteo-dasi-salpyeoboneun-kubernetes-pod-dongjag-weonri)

<br>

<br>

### What is Kubernetes Pod?

- Kubernetes에서 배포할 수 있는 **최소 객체 단위**
- 1개 이상의 `container`로 이루어진 group
  - Container를 잘 알아야 Pod를 이해할 수 있다!

<br>

<br>

### What is Container?

- Container는 **격리된 환경**에서 실행되는 **Process** 이다

<br>

<br>

### Container가 격리된 환경을 구현하는 주요 원리

#### 1. Root directory 격리 (`chroot`)

- **chroot**

  ```shell
  $ chroot <NEWROOT> <COMMAND>
  ```

  - 입력된 경로 (New root path)가 root directory로 격리된 process (command)를 실행하기 위한 명령어

<br>

#### 2. Linux namespaces

- Process 간 system resources를 격리하기 위한 Linux kernel의 기능 

  ```shell
  $ lsns -p <pid>	
  ```

- **unshare**

  - 특정 `namespace`를 격리한 process를 실행할 수 있는 명령어

  - ex)

    ```shell
    # mount namespace를 격리 (-m)한 /bin/bash process 실행
    $ unshare -m /bin/bash
    
    # mount namespace(-m)와 ipc namespace(-i)를 격리한 /bin/bash process 실행
    $ unshare -m -i /bin/bash
    ```

<br>

#### 3. Mount (`mnt`) namespace

- **mount**

  - Unix 계열 system에서 특정 file system에 접근하기 위해, file system을 `root directory (/)`부터 시작하는 **file tree** 의 특정 directory에 연결하는 것

    ```shell
    mount -t <type> <device> <dir>
    ```

  - ex)

    ```shell
    # tmpfs (temporary file storage) fmf "/root/test" 경로에 mount
    $ mount -t tmpfs tmpfs /root/test
    ```

- **mount namespace**

  - Process 간 서로 다른 `mount point`를 가질 수 있게 함

<br>

#### 4. Process ID (pid) namespace

- Container는 **격리된 환경**에서 실행되는 **Process**이다
  - Container 안에서는 하나의 VM처럼 보이지만, Container 밖 (host)에서는 하나의 Process일 뿐이다
  - 같은 process에 대해,
    - Host에서 확인한 PID와 container 안에서 확인한 PID가 다르다
- PID namespace가 격리된 container에서 최초로 실행된 process (`entrypoint`)는 항상 **PID=1**을 갖는다

<br>

#### 5. Inter-Process Communication (ipc) namespace

- **System V** 기반의 process 간 통신을 격리한다
  - **System V IPC**
    - `shared memory (shm)`
    - `semaphore`
      - 여러 process나 thread가 공유 자원에 접근하는 것을 제어하기 위한 방법
        - 병행 처리를 위한 process 동기화 기법
    - `POSIX message queue`
      - /proc/sys/fs/mqueue
      - System V message queue의 새로운 버전
        - 함수의 이름과 종류는 다르지만, 하는 일은 비슷하다
        - System V 기반 message queue 함수보다 더 직관적이고 쓰기 편하다
  - IPC 객체들은 같은 IPC namespace에 존재하는 process에만 표시된다

<br>

#### 6. Network (net) namespace

- Network interface, routing, 방화벽 규칙들을 격리한다

- ex)

  ```sh
  # "chloe-ns" 라는 이름의 network namespace 생성
  $ ip netns add chloe-ns
  $ ip netns list
  chloe-ns
  ```

  ```sh
  # virtual ethernet interface pair 생성 (veth1, veth2)
  # "veth1"은 chloe-ns에 생성, "veth2"는 PID 1의 network namespace에 생성
  $ ip link add veth1 netns chloe-ns type veth peer name veth2 netns 1
  ```

- Docker의 container network 구조
  - Container는 host와 network namespace가 격리된다
    - Host - container 간 `veth peer`를 생성하여 연결한다
    - Host이 veth는 `docker bridge` 와 연결되어 container 외부로 통신 시 `bridge`를 거쳐간다

<br>

#### 7. Unix Time-Shring (uts) namespace

- `Unix Time-Sharing`이란?
  - Computing resource를 다른 user들과 공유하는 것에서 유래되었다
  - 여려 user가 같은 machine을 사용하고 있지만, 마치 다른 machine을 사용중인 것 처럼 만들고 싶을 때 **hostname**을 격리할 수 있는 공간을 만들어 사용한다

<br>

#### 8. User ID (user) namespace

- Host에서의 `uid`와 Container의 `uid` 를 다르게 mapping 한다
- Docker container는 기본적으로 **user namespace**를 격리하지 않는다
  - *즉, container의 user가 host와 (거의) 같은 uid 권한을 그대로 행사할 수 있다!*
- **Docker가 user namespace를 격리하지 낳는 이유**
  - `PID`, `Network namespace` **공유 기능**과 **호환 문제**
  - user mapping을 지원하지 않는 외부 volume 또는 driver와의 **호환 문제**
  - 격리된 user namespace의 user가 mapping 된 실제 host 상의 uid로부터, host에서 binding 한 file에 접근 권한이 보장되어야 하는 **복잡성**
  - 격리되지 않은 user namespace에서 container root가 host root와 거의 대등한 수준의 권한을 가지긴 하지만 전체 root 권한을 의미하는 것은 아니다