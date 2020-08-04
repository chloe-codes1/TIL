# Getting Started with Docker

> Docker 정복한다!!!!!!!
>
> References: [책] 트러블 슈팅 도커

<br>

## Container and Docker

- Docker는 엄청난 관심을 받고있는 Open source project
- Application을 `경량 컨테이너`로 packaging 해서 **배포** 하고 **구동**하는 기능을 제공한다
- **Docker Container**는 실제 화물 선박에서 사용하는 컨테이너처럼 application을 **일관성** 있게 표준화된 형태로 전달하는 기능을 제공한다!

<br>

### Container 란?

![VM vs Container](../images/image-20200802224306612.png)

- Container는 application아을 **캡슐화**해 **독립적인 운영 환경**을 제공하는 기술
  - Virtual Machine의 대안으로 사용할 수 있다!
- Container는 Linux Kernel의 격리 기능에 대한 **User Space Interface** 인 **Linux Container**를 기반으로 만든 것!
  - 여기에 강력한 API와 간결한 도구를 제공함으로써 Linux 사용자가 application을 container로 만들어 관리 할 수 있다
- Container는 Host machine에서 구동하는 OS들이 Linux kernel을 서로 공유한다는 점에서 기존 `Hypervisor`와 다르다!
  - **Hypervisor** 란?
    - Virtual Machine을 생성하고 구동하는 소프트웨어
  - 즉, 다시 말해 같은 머신에서 여러 컨테이너를 구동해도 사용하는 Kernel은 모두 같다
    - 그래서 VM보다 **속도가 빠르고**, **성능 오버헤드**도 거의 없다!

<br>

### OS Container

- OS Container는 VM과 비슷하다
  - but, Host Machine OS의 **Kernel을 공유**하면서 **유저 스페이스 격리 기능**을 제공한다는 점이 다르다
- VM과 마찬가지로 Container에 **전용 리소스**를 할당할 수 있고, application과 library 등을 설치, 설정 및 구동 할 수 있다
- OS Container는 **확장성 테스트**를 할 때 유용하다!
  - 다양한 배포판으로 구성된 여러 컨테이너를 쉽게 배포할 수 있는데 VM보다 훨씬 **가볍다** 
- Container는 구조와 내용물을 정의한 **이미지**나 **템플릿**을 통해 생성한다
  - 그래서 개발 환경을 구축할 때 다른 Container와 동일한 실행 환경과 버전, 패키지 환경을 갖추도록 구성하기가 쉽다!
- 현재 다양한 컨테이너 기술이 나와 있는데, 그 중 OS Container로 적합한 것은 `LXC`, `OpenVZ`, `Docker`, `BSD Jain` 등이 있다

<br>

### Application Container

- **OS Container**는 여러 개의 process 로 구성했다면, **Application Container**는 하나의 서비스를 package로 만들어서 구동한다
  - Appllication container는 하나의 process만 구동한다
    - 이 때 구동되는 process는 aaplication process로서 **OS Container** 가 하나의 OS 위에 여러 개의 서비스를 구동하는 방식과 대조적이다!
- Docker container는 계층 (layer) 방식을 사용하는데, 이를 통해 **중복을 최소화**하고 **재사용성**을 높일 수 있다
  - 즉, 모든 구성 요소에서 공통적으로 사용하는 `base image`에 대한 container를 먼저 구동하고, 
  - 그 위에 원하는 요소를 파일 시스템에 별도의 layer로 추가하는 방식으로 구성한다
- Layer 기반 파일 시스템을 사용하면 원하는 시점에 언제든지 예전 레이어로 쉽게 되돌아갈 수 있다!
- **Dockerfile**에 명시된 `RUN`  명령이 실행될 때마다 container에 layer가 새로 생성된다
- Application Container의 주 목적으로는 application을 구성하는 다양한 컴포넌트들을 **별도의 컨테이너 형태의 패키지**로 만드는 데 있다
  - 이렇게 container 단위로 묶인 application의 구성 요소들은 API나 서비스를 통해 상호작용하는 방식으로 application을 구동한다
    - 이러한 **분산 멀티 컴포넌트 시스템** 형태의 배포 방식은 `마이크로서비스 아키텍처` 구현의 핵심이다!
      - 이렇게 하면 
        - 개발자는 자신이 원하는 형태로 application을 container 형태의 package로 만들고, 
        - 이를 수평적으로나 수직적으로 확장하기 위해 다양한 platform에 container를 배포하는 작업은 IT팀이 전담하게 할 수 있다

