# Cluster

<br/>

## Cluster란?

- Kubernetes를 배포하면 Cluster를 얻는다
- Kubernetes Cluster는 컨테이너화된 애플리케이션을 실행하는 `node` 라고 하는 worker machine들의 집합이다
- 모든 cluster는 최소 하나 이상의 `worker node` 를 가진다

<br/>

## Cluster Architecture

> 하드웨어 수준에서 Kubernetes Cluster는 여러 node로 구성되며, 두 가지 유형으로 나눌 수 있다
>
1. `마스터 노드`

   전체 Kubernetes system을 제어하고, 관리하는 Kubernetes `Control Plane` 을 실행한다

2. `워커 노드`

   실제 배포되는 container application을 실행한다

<br/>

## Control Plane

> Control Plane은 `Cluster를 제어하고 작동`시킨다

하나의 master node에서 실행하거나 여러 node로 분할되고 복제되어 `고가용성을 보장`할 수 있는 아래 요소들로 구성된다
>

<br/>

### Kubernetes API Server

> API Server는 Kubernetes API를 노출하는 component이다
>
사용자, Control Plane 구성 요소와 통신한다

#### kube-apiserver

- kube-apiserver는 `수평으로 확장` 되도록 디자인되었다
  - 즉, 더 많은 인스턴스를 배포해서 확장할 수 있다
- 여러 kube-apiserver 인스턴스를 실행하고, 인스턴스간의 traffic을 균형있게 조절할 수 있다

<br/>

### Scheduler

> Node가 배정되지 않은 새로 생성된 Pod를 감지하고, `실행할 node를 선택`하는 component
>
- Application의 `배포`를 담당한다
  - Application의 배포 가능한 각 구성 요소를 `worker node에 할당`한다
- Scheduling 을 위해 고려되는 요소는 아래와 같다
  - 개별/총체적 Resource requirements
  - Hardware/Software Policy 제약
  - Affinity & anti-affinity 명세
  - Data 지역성
  - Workload 간 간섭
  - Deadline

<br/>

### Controller Manager

> Controller `process를 실행`하는 component
>
- 구성 요소의 복제본, worker node 추적, node 장애 처리 등과 같은 cluster 단의 기능을 수행한다
- 논리적으로 각 controller는 분리된 process 지만, 복합성을 낮추기 위해 하나의 binary로 compile되고, `단일 process 내에서 실행`된다

#### Controller Types

- `Node controller`
  - Node가 다운되었을 때 알리고, 응답하는 것에 대한 책임을 진다
- `Job controller`
  - 일회성 Job object를 추적하고, 해당 작업이 실행될 수 있게 Pod를 생성한다
- `Endpoints controller`
  - Service와 Pod를 연결시킨다
- `Service Account & Token controllers`
  - 새로운 Namespace에 대한 default account와 API access token을 생성한다

<br/>

### etcd

> Cluster 구성을 지속적으로 저장하는 신뢰할 수 있는 key-value 구조의 `분산 데이터 저장소` 이다
>

<aside>
💡 Control Plane의 구성 요소는 Cluster 상태를 유지하고 제어하지만, application을 실행하진 않는다
→ 이것은 Node에서 이루어진다

</aside>

<br/>

## Node

> Worker Node는 container화된 `application을 실행`하는 시스템이다
> 
> Application을 실행하고 모니터링하며, application에 서비스를 제공하는 작업은 아래의 구성요소에 의해 수행된다
>

### Container Runtime

> Container  실행을 담당한다
>

Container를 실행하는 `Docker`, `containerd` , `CRI-O` 또는 [Kubernetes CRI (컨테이너 런타임 인터페이스)](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-node/container-runtime-interface.md) 구현한 소프트웨어를 지원한다

<br/>

### Kubelet

> API Server와 통신하고 node의 container를 관리한다
>

- Cluster의 각 node에서 실행되는 agent이며, Pod에서 container가 동작하도록 관리한다
- 다양한 매커니즘을 통해 `PodSpec` 의 집합을 받아서 container가 해당 Pod 스펙에 따라 정상적으로 동작하는지 관리한다
- Kubernetes를 통해 생성되지 않은 container는 관리하지 않는다

<br/>

### Kube-proxy

> Application 구성 요소 간에 네트워크 트래픽을 로드밸런싱 하는 `Kube-Proxy`
>
- Cluster의 각 node에서 실행되는 `네트워크 프록시` 로, Kubernetes service 개념의 구현부이다
- Node의 네트워크 규칙을 유지/관리한다
  - 네트워크 규칙이 내부 네트워크 session 이나 cluster 밖에서 pod로 네트워크 통신을 할 수 있게 해준다
