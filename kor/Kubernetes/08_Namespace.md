# Namespace

<br/>

## Namespace란?

- Kubernetes namespace는 object 이름의 `범위` 를 제공한다
- 모든 리소스를 하나의 단일 namespace에 두는 대신에, 여러 namespace로 분할 할 수 있다
- 분리된 namespace는 같은 리소스 이름을 다른 namespace에 걸쳐 여러 번 사용할 수 있게 해준다

<br/>

## Namespace의 필요성

- 여러 namespace를 사용하면 많은 구성 요소를 가진 복잡한 시스템을 좀 더 작은 `개별 그룹으로 분리` 할 수 있다
  - `Multi-tenant` 환경처럼 `리소스를 분리`하는 데 사용된다
  - 리소스 이름은 namespace 안에서만 고유하면 된다
    - 서로 다른 두 namespace는 동일한 이름의 리소스를 가질 수 있다
  - 대부분의 리소스 유형은 namespace 안에 속하지만 일부는 그렇지 않다
    - 그 중 하나는 `node` 인데, node는 `전역`이며 단일 namespace에 속하지 않는다
- namespace를 사용해 서로 관계 없는 리소스를 겹치지 않는 `그룹으로 분리` 할 수 있다
  - 여러 사용자 또는 그룹이 동일한 kubernetes cluster를 사용하고 있고, 각자 자신의 리소스를 관리한다면 각각 고유한 namespace를 사용해야 한다
    - 이렇게 하면 다른 사용자의 리소스를 수정하거나 삭제하지 않도록 주의를 기울일 필요가 없다!
- namespace는 리소스를 격리하는 것 외에도 특정 사용자가 지정된 리소스에 `접근할 수 있도록 허용`하고, 개별 사용자가 사용할 수 있는 컴퓨팅 `리소스를 제한` 하는 데에도 사용된다

<br/>

## Namespace 생성과 오브젝트 관리

### Namespace 생성

> Namespace는 kubernetes resource이기 때문에 YAML 파일을 kubernetes API 서버에 요청해 생성할 수 있다
>

#### 1. YAML 파일에서 namespace 생성

ex) chloe라는 이름의 namespace 생성하기

`chloe-namespace.yaml` 파일 생성

```yaml
apiVersion: v1
kind: Namespace
metadata: 
 name: chloe
```

kubectl 명령어로 해당 파일을 kubernetes API 서버로 전송하기

```bash
kubectl create -f choe-namespace.yaml
```

<br/>

#### 2. `kubectl create namespace` 명령어로 namespace 생성

`kubectl create namespace` 명령어를 사용해 빠르게 namespace를 생성할 수 있다

ex)

```bash
kubectl create namespace chloe
```

<aside>
⚠️ 대부분의 오브젝트 이름은 `RFC1035` 에 지정된 규칙을 준수해야 한다

→ 글자, 숫자, 대시 (-), 점(.) 을 포함할 수 있음을 의미!

but, `namespace`를 비롯한 몇몇 리소스에서는 점(.)을 포함할 수 없다!

→ why? DNS 주소 이름을 포함하면 안 되기 때문!

</aside>

<br/>

## Namespace가 제공하는 격리의 이해

Namespace를 사용하면 오브젝트를 별도 그룹으로 분리해 특정한 namespace 안에 속한 리소스를 대상으로 작업할 수 있게 해주지만, `실행 중인 오브젝트에 대한 격리는 제공하지 않는다`

ex)

- 다른 사용자들이 서로 다른 namespace에 pod를 배포할 때 `해당 pod가 서로 격리돼 통신할 수 없다`고 생각할 수 있지만, **반드시 그런 것은 아니다!**
- namespace에서 네트워크 격리를 제공하는지는 kubernetes와 함께 배포하는 `네트워킹 솔루션`에 따라 다르다
- 네트워크 솔루션이 namespace 간 격리를 제공하지 않는 경우, A namespace 안에 있는 pod가 B namespace 안에 있는 pod의 IP 주소를 알고 있었다면 HTTP 요청과 같은 트래픽을 다른 pod로 보내는 것에 아무런 제약 사항이 없다!

<br/>

### VPC CNI 사용 시

> **[CNI plugin for Kubernetes networking over AWS VPC](https://github.com/aws/amazon-vpc-cni-k8s/blob/master/docs/cni-proposal.md) 참고**
>
