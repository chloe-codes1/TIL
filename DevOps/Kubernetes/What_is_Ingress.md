# What is Ingress?

> Kubernetes의 Ingress에 대해 알아보아요
>
> Reference: [Kubernetes docs](https://kubernetes.io/ko/docs/concepts/services-networking/ingress/)

<br>

<br>

## 인그레스 (Ingress)

<br>

- 일반적으로 Network traffic은 `ingress` 와 `engress` 로 구분된다
  - Ingress는 외부로부터 서버 내부로 **유입되는 network traffic**
  - Engress는 서버 내부에서 외부로 **나가는 network traffic**
- Cluster 내의 서비스에 대한 외부 접근을 관리하는 API Object
  - 일반적으로 `HTTPS` 를 관리한다
- Ingress는 **부하 분산**, **SSL 종료**, **명칭 기반의 가상 호스팅** 을 제공할 수 있다

<br>

### Terms

- **Node**
  - Cluster의 일부
  - Kubernetes에 속한 worker machine
- **Cluster**
  - Kubernetes에서 관리되는 **container화 된 application**을 실행하는 **node의 집합**
    - 대부분의 Kubernetes 배포에서 cluster에 속한 node는 `Public Internet`의 일부가 아니다
-  **Edge Router**
  - Cluster에 방화벽 정책을 적용하는 router
    - Cloud provider or physical hardware의 일부에서 관리하는 `Gateway` 일 수 있다
- **Cluster Network**
  - Kubernetes networking model에 따라 cluster 내부에서 통신을 용이하게 하는 논리적 또는 물맂거 링크의 집합
- **Service**
  - `Label selecter`를 사용해서 `pod` 집합을 식별하는 Kubernetes service
    - 달리 언급하지 않으면 service는 `Cluster network` 내에서만 routing 가능한 가상 IP를 가지고 있다고 가정한다

<br>

### What is Ingress?

- Cluster 외부에서 cluster 내부 서비스로 **HTTP** 와 **HTTPS** 경로를 노출한다
- **Traffic routing** 은 Ingress resource에 정의된 규칙에 의해 control 된다

![image-20200929010831268](../../images/image-20200929010831268.png)

- Ingress는 외부에서 service로 접속이가능한 **URL**, **Load balance traffic**, **SSL/TSL** 종료, 그리고 이름 기반의 virtual hosting service를 제공하도록 구성할 수 있다
  - `Ingress controller` 는 일반적으로 load balancer를 사용해서 ingress를 수행할 책임이 있으며, traffic을 처리하는데 도움이 되도록 **edge router** 나 **additional frontend** 를 구성할 수 있다
- Ingress는 임의의 port 또는 protocol 을 노출시키지 않는다
  - HTTP와 HTTPS 이외의 service를 인터넷에 노출하려면 일반적으로 `Service.Type=NodePort` 또는 `Service.Type=LoadBalancer`를 사용한다

<br>

### Prerequisites

- `Ingress Controller` 가 있어야 `Ingress` 를 충족할 수 있다
  - Resource만 생성하는 것은 효과가 없다! controller 가 필요하다
- `ingress-nginx` 같은 **ingress controller** 를 배포해야 하는데, ingress controller의 종류는 다양하다





