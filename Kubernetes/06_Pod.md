# Pod

<br/>

## Pod란?

> Pod는 쿠버네티스에서 생성하고 관리할 수 있는 `배포 가능한 가장 작은 컴퓨팅 단위`이다
>
- Pod는 하나 이상의 컨테이너의 그룹이다
  - 쿠버네티스는 개발 컨테이너들을 직접 다루지 않는다
  - 대신 함께 배치된 다수의 컨테이너라는 개념을 사용하고, 이 컨테이너의 그룹을 `Pod` 라고 한다
- Pod는 하나 이상의 `밀접하게 연관된 컨테이너의 그룹`으로, 같은 워커 노드에서 같은 linux namespace로 함께 실행된다
  - 각 Pod는 자체 IP, 호스트 이름, 프로세스등이 있는 `논리적으로 분산된 머신` 이다
  - 애플리케이션은 단일 컨테이너로 실행되는 단일 프로세스일 수 있고, 개발 컨테이너에서 실행되는 주 어플리케이션 프로세스와 부가적으로 도와주는 프로세스로 이루어질 수도 있다
- Pod가 여러 컨테이너를 가지고 있는 경우에, 모든 컨테이너는 항상 하나의 워커 노드에서 실행되며, 여러 워커 노드에 걸쳐 실행되지 않는다

<br/>

### Pod에서 여러 컨테이너 사용이 필요한 경우

> 컨테이너를 Pod로 묶어 그룹으로 만들 때 (두 개의 컨테이너를 단일 파드로 넣을지 or 두 개의 별도 파드에 넣을지 결정하기 위해) 아래와 같은 질문을 해볼 수 있다
>
1. 컨테이너를 함께 실행해야 하는가 or 서로 다른 호스트에서 실행할 수 있는가?
2. 여러 컨테이너가 모여 하나의 구성 요소를 나타내는가 or 개별적인 구성요소인가?
3. 컨테이너가 함께 or 개별적으로 스케일링되어야 하는가?

기본적으로 특정 이유 때문에 컨테이너를 단일 Pod로 구성해야하지 않는다면, 분리된 Pod에서 컨테이너를 실행하는 것이 좋다

<aside>
💡 컨테이너는 여러 프로세스를 실행하지 말아야한다
Pod를 `동일한 machine`에서 실행할 필요가 없다면, 여러 컨테이너를 포함하지 말아야 한다

</aside>

<br/>

## Pod 정의하기

### Pod를 정의하는 주요 부분

- `Metadata`
  - 이름, namespace, label 및 Pod에 관한 기타 정보를 포함한다
- `Spec`
  - Pod container, volume, 기타 데이터 등 Pod 자체에 관한 실제 명세를 가진다
- `Status`
  - Pod 상태, 각 container 설명과 상세, Pod 내부 IP, 기타 기본 정보 등 Pod에 관한 현재 정보를 포함한다

ex)

```yaml
apiVersion: v1
kind: Pod
metadata:
 name:kubia-mannual
spec:
 containers:
 - image: luksa/kubia
  name: kubia
  ports:
  - containerPort: 8080
   protocol: TCP
```

<br/>

### 컨테이너 포트 지정

- Pod 정의 안에서 port를 지정해둔 것은 단지 정보에 불과하다
  - 생략해도 다른 client에서 port를 통해 연결할 수 있는지의 여부에는 영향을 미치지 않는다
- 하지만 포트를 명시적으로 정의한다면, Cluster를 사용하는 모든 사람이 해당 pod에서 노출한 port를 빠르게 볼 수 있다는 장점이 있다
  - 또한 port를 명시적으로 정의하면 port에 이름을 지정해서 편리하게 사용할 수 있다

<br/>

## Label을 이용한 Pod 구성

> Label을 통해 Pod와 기타 다른 Kubernetes object 간의 조직화가 이루어진다
>
- Label은 Pod와 모든 다른 쿠버네티스 리소스를 `조직화` 할 수 있는 기능이다
- Label은 리소스에 등록하는 `key-value` 쌍으로, 이 쌍은 label selector를 사용해 리소스를 선택할 때 활용된다
  - 리소스는 selector에 지정된 label을 포함하는지 여부에 따라 필터링 도니다
- Label의 key가 `unique` 하다면, 하나 이상의 원하는 만큼의 label을 가질 수 있다
- 일반적으로 리소스 생성 시 label을 붙이지만, 나중에 label을 추가하거나 기존 값을 수정할 수도 있다

<br/>

### Label과 Selector를 이용해 Pod 스케줄링 제한하기

- Kubernetes의 전체적인 아이디어는 그  위에 실행되는 어플리케이션으로부터 실제 인프라스트럭처를 숨기는 것에 있기에, Pod가 어떤 node에 스케줄링되어야 하는지 구체적으로 지정하고 싶지 않을 것이다
  - 그로 인해 어플리케이션이 인프라스트럭처에 결합되기 때문이다
- 그래서 Kubernetes는 정확한 node를 지정하는 대신 필요한 node 요구 사항을 기술하고, Kubernetes가 요구 사항을 만족하는 node를 선택하게 한다
  - 이는 `node label` 과 `label selector` 를 통해 가능하다

<br/>

#### 1. 워커 노드 분류에 Label 사용

> Node를 포함한 모든 kubernetes object에 `label`을 부착할 수 있으며,
일반적으로 새 node를 cluster에 추가할 때 node가 제공하는 하드웨어나 pod 스케줄링 시 유용하게 사용할 수 있는 사항을 label로 지정해 node를 분류한다
>

ex)

```bash
kubectl label node [node] gpu=true
```

<br/>

#### 2. 특정 Node에  Pod 스케줄링

> GPU를 필요로 하는 새로운 Pod를 배포해야 한다고 할 때, 스케줄러가 GPU를 제공하는 node를 선택하도록 요청하려면, 해당 Pod의 YAML 파일에 `node selector` 를 추가해야 한다
>

ex)

```yaml
apiVersion: v1
kind: Pod
metadata:
 name: kube-gpu
spec:
 nodeSelector:
  gpu: "true"
 containers:
 - image: luksa/kubia
  name: kubia
  ports:
  - containerPort: 8080
   protocol: TCP
```

위와 같이 설정함으로써 스케줄러는 `gpu=true` label을 가지고 있는 node 중에서 선택하게 된다

<br/>

## Pod를 안정적으로 유지하기

### Liveness Probe

- Kubernetes는 `liveness probe` 를 통해 컨테이너가 살아 있는지 확인할 수  있다
- Pod의 spec에 각 컨테이너의 liveness probe를 지정할 수 있다
- Kubernetes는 주기적으로 probe를 실행하고, probe에 실패할 경우 `컨테이너를 다시 시작` 한다

<br/>

### Probe 실행 매커니즘

> Kubernetes는 세 가지 매커니즘 을 사용해 컨테이너에 Probe를 실행한다
>
1. `HTTP GET Probe`
    - 지정한 IP 주소, port, 경로에 HTTP GET 요청을 수행한다
    - Probe가 응답을 수신하고 응답 코드가 2xx or 3xx인 경우, probe가 성공했다고 간주된다
    - 오류 코드를 반환하거나 응답 자체를 하지 않으면, probe가 실패한 것으로 간주되어 컨테이너를 다시 실행한다
2. `TCP Socket Probe`
    - 컨테이너의 지정된 port에 TCP 연결을 시도한다
    - 연결에 성공하면 probe가 성공한 것이고, 그렇지 않으면 컨테이너가 다시 실행된다
3. `Exec Probe`
    - 컨테이너 내의 임의의 명령을 실행하고, 명령의 종료 상태 코드를 확인한다
    - 상태 코드가 `0` 이면 probe가 성공한 것이다
    - `0` 이외의 다른 모든 코드는 실패로 간주 된다

ex)

```yaml
apiVersion: v1
kind: Pod
metadata:
 name: kube-liveness
spec:
 containers:
 - image: luksa/kubia-unhealthy
  name: kubia
  livenessProbe:
   httpGet:
    path: /
    port: 8080
```

위의 설정에서 pod descriptor는 kubernetes가 주기적으로 `"/"` 경로와 8080 port에 HTTP GET 요청을 보내서 컨테이너가 정상 동작하는지 확인하도록 `httpGet` liveness probe를 정의한다
