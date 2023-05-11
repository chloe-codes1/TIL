# Node

<br/>

## Node란?

- Kubernetes는 container를 pod 내에 배치하고, node에서 실행함으로써 workload를 구동한다
- node는 cluster에 따라 `가상 or 물리적 머신`일 수 있다
- 각 node는 `control plane` 에 의해 관리되며 pod를 실행하는 데 필요한 서비스를 포함한다
- node의 컴포넌트에는 `kubelet`, `kube-proxy` , `컨테이너 런타임` 이 있다

    → [Cluster](https://www.notion.so/Cluster-ac3f9a7fde0f46b7b1687132f066b511) 참고!

<br/>

## Node의 관리

> Kubernetes API 서버에 node를 추가하는 방법은 크게 두가지가 있다
>
1. Node의 `kubelet`으로 control plane에 자체 등록
2. 사용자 (or 다른 사용자)가 `node object`를 수동으로 추가

Kubelet or node object로 등록한 후 control plane은 `생성된 node object가 유효한지 확인`한다

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

- Kubernetes는 내부적으로 `node object`를 생성한다
- Kubernetes는 `kubelet` 이 node의 `metadata.name` 필드와 일치하는 API 서버에 등록되어 있는지 확인한다
  - node가 정상이면,
    - pod를 실행할 수 있게 된다
  - 정상이 아니면,
    - 해당 node는 정상이 될 때까지 모든 cluster 활동에 대해 무시된다

<aside>
💡 Kubernetes는 유효하지 않은 `node object` 를 `유지` 하고, node가 `정상인지 확인` 한다

→ 상태 확인을 중지하려면 사용자 or 컨트롤러에서 node object를 명시적으로 삭제해야 한다

</aside>

<br/>

### Node 이름의 고유성

- 두 node는 동시에 같은 이름을 가질 수 없다
  - kubernetes는 `같은 이름`의 리소스가 `동일한 객체`라고 가정한다!
- Node의 경우, 동일한 이름을 사용하는 인스턴스가 `동일한 상태` (ex. 네트워크 설정, root disk contents)와 node label과 같은 `동일한 속성` 을 갖는다고 암시적으로 가정한다
  - 만약 인스턴스가 이름을 변경하지 않고 수정된 경우, 이로 인해 불일치가 발생할 수 있다!
  - 때문에 노드를 교체하거나 업데이트해야 하는 경우, `기존 node object를 먼저 API 서버에서 제거`  하고 업데이트 후 다시 추가해야 한다!

<br/>

## Node의 상태

> Node의 상태는 아래의 정보를 포함한다

1. 주소
2. 컨디션
3. 용량과 할당 가능여부
4. 정보
>

Kubectl을 이용하여 node 상태와 세부 사항 확인하기

```bash
kubectl describe node <NODE_NAME>
```

위의 명령어를 사용하여 출력되는 정보는 아래과 같이 주소, 컨디션, 용량과 할당 가능여부, 정보이다.

<br/>

### 주소

> `addresses` 필드는 cloud provider or bare metal 설정에 따라 다르게 나타난다
>
- HostName
  - 노드의 커널에 의해 알려진 호스트명이다
  - `-hostname-override` parameter를 통해 치환될 수 있다
- ExternalIP
  - 일반적으로 노드의 IP 주소는 외부로 라우트 가능하다
  - 즉, 클러스터 외부에서 이용 가능하다
- InternalIP
  - 일반적으로 노드의 IP 주소는 클러스터 내에서만 라우트 가능하다

<br/>

### 컨디션

> `conditions` field는 모든 `Running` 상태의 node를 기술한다
>

| 노드 컨디션 | 설명 |
| --- | --- |
| Ready | 노드가 상태 양호하며 파드를 수용할 준비가 되어 있는 경우 True, 노드의 상태가 불량하여 파드를 수용하지 못할 경우 False, 노드 컨트롤러가 마지막 node-monitor-grace-period (기본값 40 기간 동안 노드로부터 응답을 받지 못한 경우) Unknown |
| DiskPressure | 디스크 사이즈 상에 압박이 있는 경우, 즉 디스크 용량이 넉넉치 않은 경우 True, 반대의 경우 False |
| MemoryPressure | 노드 메모리 상에 압박이 있는 경우, 즉 노드 메모리가 넉넉치 않은 경우 True, 반대의 경우 False |
| PIDPressure | 프로세스 상에 압박이 있는 경우, 즉 노드 상에 많은 프로세스들이 존재하는 경우 True, 반대의 경우 False |
| NetworkUnavailable | 노드에 대해 네트워크가 올바르게 구성되지 않은 경우 True, 반대의 경우 False |

<br/>

### 용량과 할당 가능 여부

- node 상에 `사용 가능한 리소스`를 나타낸다
  - 리소스에는 CPU, 메모리 그리고 node 상으로 스케줄 되어질 수 있는 최대 pod 수가 있다
- 용량 블록의 필드는 `node에 있는 리소스의 총량`을 나타낸다
  - 할당가능 블록은 일반 pod에서 사용할 수 있는 node의 리소스 양을 나타낸다

<br/>

### 정보

- `커널 버전`, `쿠버네티스 버전` (kubelet과 kube-proxy 버전), `컨테이너 런타임 상세 정보` 및 `노드가 사용하는 운영 체제`가 무엇인지와 같은 노드에 대한 일반적인 정보가 기술된다
  - 이 정보는 kubelet이 node에서 수집하여 kubernetes API로 전송한다
