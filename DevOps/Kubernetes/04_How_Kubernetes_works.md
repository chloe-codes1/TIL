# How Kubernetes works

> Reference: [Container부터 다시 살펴보는 Kubernetes Pod 동작 원리](https://speakerdeck.com/devinjeon/containerbuteo-dasi-salpyeoboneun-kubernetes-pod-dongjag-weonri)

<br>

<br>

## What is Container?

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
  - **Docker가 user namespace를 격리하지 않는 이유**
    - `PID`, `Network namespace` **공유 기능**과 **호환 문제**
    - user mapping을 지원하지 않는 외부 volume 또는 driver와의 **호환 문제**
    - 격리된 `user namespace`의 user가 mapping 된 실제 host 상의 uid로부터, host에서 binding 한 file에 접근 권한이 보장되어야 하는 **복잡성**
    - 격리되지 않은 `user namespace`에서 container root가 host root와 거의 대등한 수준의 권한을 가지긴 하지만 전체 root 권한을 의미하는 것은 아니다
  - *Kubernetes 또한 `user namespace` 격리를 아직 지원하지 않는다*
  - **`User namespace` 격리를 사용하지 않을 때**
    - 신뢰할 수 있는 사용자만 container runtime (ex. Docker)을 실행할 수 있도록 제한한다
    - Container의 process가 **root user**로 실행하지 않도록 한다
      - 특정 UID, GID로 실행될 수 있도록 지정한다
    - Host의 directory를 container가 직접 접근할 수 있도록 mount 하지 않는다
  - *Kubernetes에서도 같은 원리의 보안 설정을 제공한다*

<br>

#### 9. Control group (cgroup)

- `Process group`의 **자원 할당**을 제한하고, 격리할 수 있는 Linux Kernel 기능
  - `CPU`
    - ex) CPU 사용량을 제한
  - `Memory`
    - ex) Memory 사용량을 제한
  - `Network`
    - ex) Network Traffic 우선 순위를 설정
  - `Disk`
    - ex) Disk 사용량에 대한 통계를 제공

<br>

#### `Wrap-up`: Container가 격리된 환경을 구현하는 주요 원리

- Container는 **격리된 환경**에서 실행되는 **process**이다
- `namespace`를 통해 process의 **격리된 환경**을 구현한다
- `cgroups`를 통해 process의 **자원 사용량**을 **제한**한다

<br>

<br>

## What is Kubernetes Pod?

- Kubernetes에서 배포할 수 있는 **최소 객체 단위**
- 1개 이상의 `container`로 이루어진 group

<br>

### Pod는 "배포 가능한 최소 객체 단위"이다

K8s application은 `pod` 단위로 배포되고, `pod`는 여러 형태의 resource에 의해 배포된다

- `Job`
  - 한 번 실행되고 작업이 완료되면 종료되는 형태의 pod를 관리
- `ReplicaSet`
  - 명시된 pod 개수가 실행되는 상태를 보장
- `DaemonSet`
  - 각 node마다 하나씩만 실행되는 pod를 관리
- `StatefulSet`
  - **Stateful application**을 실행하는 pod를 관리
- `Deployment`
  - Pod, ReplicaSet의 update에 대한 배포를 관리

*Pod는 Kubernetes에서 **생성**하고 **관리**되는 가장 **기본적인 단위**이다!*

<br>

<br>

### Pod는 1개 이상의 container로 이루어진 group이다

- Pod에는 1개 이상의 container가 존재할 수 있다
  - 단일 container를 실행하는 pod
  - 여러 container를 실행하는 pod

<br>

#### Pod를 여러 container로 구성하는 경우

- Main 역할을 하는 1개의 **Primary Container**
- 1개 이상의 **Sidecar Containers**
  -  Primary Container의 **보완 역할**을 하기 위해 실행되는 container
    - ex) monitoring, logging, etc.

<br>

#### Container에서는 단일 Process를 실행하도록 권장한다

- **Why?**
  - Container는 앞서 언급했듯이, **격리된 환경**에서 실행되는 **process**이다
  - 격리된 PID namespace에서 최초로 실행된 process는 `pid=1`이다
  - 즉, Container에서 **최초로 실행된 process의 state** == **Container의 수명**이다!
- **If container 안에서 여러 process가 실행 중이라면?**
  - Container가 실행 중이라도, main process를 제외한 다른 process들의 실행 상태를 보장할 수 없다
  - 즉, **Container에서 실행되는 process들의 state** != **Container의 state**
- **If Kubernetes pod의 특정 container가 종료되면?**
  - Kubernetes는 선언된 `restartPolicy`에 따라 container를 재시작한다
    - `restartPolicy` options
      - Always
      - OnFailure 
      - Never

<br>

#### Pod를 구성하는 기준

- Container들이 꼭 같은 node에서 실행되어야 하는가?
  - 같은 pod에 존재하는 container들은 항상 같은 node에 존재한다!
- 해당 container들이 같은 개수로 **수평 확장**되어야 하는가?
  - Pod 단위 == 확장의 단위!
- Container들은 하나의 group으로 함께 배포해야 하는가?

<br>

#### Kubernetes Pod의 container 간 격리

- Pod가 실행중인 node에서 container를 확인해보면,
  -  `cgroup namespace`, `user namespace`는 따로 격리하지 않는다
  - `mnt`, `uts`, `pid` namespace는 각 container 별로 격리한다
    - 같은 pod여도 공유하지 않는다!
  - `ipc`, `net` namespace는 pod의 container간 **공유**한다
    - Container process간 `shared memory` 등의 IPC 가능
    - Container 간 동일한 IP주소, port를 공유한다 (충돌 주의)

**Pause Container란?**

- Pause container는 격리된 IPC, Network namespace를 생성하고 유지한다
  - 나머지 container들은 해당 namespace를 공유하여 사용한다
    - 즉, user가 실행한 특정 container가 비정상 종료되어 container 전체에서 공유되는 namespace에 문제가 발생하는 것을 방지한다!
- 단순히 무한 loop를 돌면서 `SIGINT`, `SIGTERM`을 받으면 종료한다
  - `SIGINT`
    - keyboard로 부터 오는 interrupt signal
      - [CTRL] + [C] 입력 시에 보내지는 signal
    - 실행을 중지시킨다
  - `SIGTERM`
    - Terminate의 약자로, 가능한 정상 종료하도록 하는 signal
    - kill 명령의 기본 signal
- **Zombie Process Reaping** 역할을 한다
  - PID namespace sharing을 하는 경우!

<br>

#### Kubernetes의 PID namespace sharing

- 각 container에서 **Zombie process**가 발생할 우려가 있는 경우, Kubernetes `PID namespace sharing` option을 활성화하여 **Pause container**에 **Zombie process reaping** 역할을 위임할 수 있다
- 활성화 방법
  -  해당 pod yml file의 `spec.template.spec.shareProcessNamespace: true`로 설정한다

<br>

<br>

## Wrap-up

### Kubernetes Pod의 개념

<br>

#### Pod란?

- Kubernetes에서 배포할 수 있는 **최소 객체 단위**
  - Pod는 여러 형태의 resource에 의해 배포된다 (`Job`, `ReplicaSet` 등)
- 1개 이상의 container로 이루어진 group
  - 단일 container를 실행하는 pod
  - 여러 container를 실행하는 pod
    - `Primary Container`
    - `Sidecar containers`

<br>

#### 하나의 container에서 여러 process를 실행하는 것은 권장하지 않는다

- Container가 실행 중이라도 main process를 제외한 다른 process들이 실행 중인 상태를 보장할 수 없기 때문이다!

<br>

#### Kubernetes Pod의 특정 container가 종료되면, `Kubelet`이 `restartPolicy`에 따라 container를 재시작한다

<br>

#### Pod를 어떻게 구성할지 판단 기준

- Container들이 꼭 **같은 node**에서 실행되어야 하는가?
- 해당 container들이 **같은 개수**로 **수평 확장**되어야 하는가?
- Container들을 하나의 group으로 함께 배포해야 하는가?

<br>

#### Pod의 container 간 격리

- Host와 공유되는 namespace
  - `cgroup`
  - `user`
- 같은 pod container 간 공유되는 namespace
  - `ipc`
  - `net`
- Container 별로 격리되는 namespace
  - `mount`
  - `uts`
  - `pid`
    - pid namespace 공유는 optional!

<br>

#### Pause Container란?

- Container 간 공유될 `IPC`, `Network namespace`를 생성하고 유지한다
- `PID namespace` 공유 시 **Zombie process reaping** 역할도 수행한다