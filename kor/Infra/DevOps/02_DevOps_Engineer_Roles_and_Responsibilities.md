# DevOps Engineer Roles and Responsibilities

> DevOps Engineer가 갖추어야할 철학과 기술에 대하여 알아보아요
>
> Reference: [인프런] DevOps : Infrastructure as Code with Terraform and AWS 강좌 by 송주영님

<br>

<br>

## DevOps 엔지니어란?

- 올바른 DevOps 문화를 위해
  - service 혹은 S/W LifeCycle에서 **반복적인 일**들을 **자동화**하고,
  - 기술적 문제 혹은 팀의 차이를 기술적으로 **예방**하고, **해소**시키는 것을 담당하는 사람
- DevOps Engineering에 관련된 공통된 기술들을 다양한 곳에 접목하는 역할을 하는 사람

<br>

<br>

## DevOps Engineer의 요구 스킬

<br>

### Soft skill

- **문제 인식**
  - 문제가 무엇이 있는지,
  - 정확한 원인이 무엇인지 파악해야 한다
- **선택과 집중**
  - 문제를 적합한 방법을 통해 해결하고,
  - 해결의 우선순위를 올바르게 설정한다
- **결정**
  - 수많은 선택지에 대해서, 추측이 아닌 확신을 가지고 빠르게 결정해야 한다
    - 결정에는 기반자료가 있어야 한다
- **업의 속성**
  - 제공하는 서비스의 본질과 가치를 이해해야 한다
- **사용자**
  - 사용자를 이해하고,
  - 요구사항에 대해서 빠르게 피드백 해야한다
    - 빠른 피드백과 적용이 필요하다

<br>

### Technical Skill

- **프로그래밍**
  - Go, Python 등 능숙하게 다를 수 있는 언어는 큰 강점이 된다
    - ex) Go, Python, Node.js 등
      - 아싸 Python!
- **운영체제**
  - Linux와 같은 운영체제를 능숙하게 다루는 것과 개념을 반드시 알아야 한다
    - ex) Shell, OS metrics, File system, 7 layers 등
- **서버 관리**
  - 서버를 관리하는 기수로가 운영 지식을 통해 신뢰할 수 있는 서비스를 구축해야 한다
    - ex) IaC, Ci/CD, API, 가용성, 성능 등
- **오픈소스**
  - 인프라를 이루는 S/W 들을 이해하고, 자동화 도구를 다룰 수 있어야 한다
    - ex) nginx, Tomcat, MySQL, Redis, Ansible, Terraform 등
- **클라우드**
  - Public Cloud를 능숙하게 다루고, 직접 구축 및 설계를 할 수 있어야 한다
    - ex) AWS, Azure, GCP, Alibaba 등

<br>

<br>

### Infrastructure as Code, 코드로써의 인프라

- 인프라를 이루는 server, middleware, service 등 인프라 구성요소들을 code를 통해 구축하는 것
  - IaC는 **코드로써의 장점**
    - **작성 용이성**
    - **재사용성**
    - **유지보수**
    - **문서화** 등의 장점을 가진다

<br>

### IaC 도구 Terraform

- Terraform은 인프라를 만들고, 변경하고, 기록하는 IaC를 위해 만들어진 도구로써,
  - 문법이 쉬워 비교적 다루기 쉽고
  - 사용자가 매우 많아 참고할 수 있는 예제가 많다
- AWS, Azure, GCP 같은 Public Cloud 뿐만이 아니라 다양한 서비스를 지원한다

<br>

<br>

### DevOps 엔지니어의 덕목

- 최대한 상황에 대한 많은 경우의 수를 생각해야 한다
  - 그 이후 코드에 반영하고 실행시에는 **로그**로 남기고 **모니터링**을 꾸준히 길게 해야한다
- 코드 실행 중 최대한 여러번 **점검**이 되어 조건이 다 일치했을 때 실제로 실행이 되도록 코드를 짜는 것도 중요하다
- 테스트 환경을 제대로 구축해야 한다
- 데브옵스 엔지니어가 되려면 특정 제품이나 기술을 아는 것으로는 부족하다
  - 제품과 기술은 산업의 발전에 따라 항상 바뀐다
- 데브옵스 철학과 기반 라이프사이클에 대한 이해도 중요하다
  - 따라서 데브옵스의 핵심인 지속적 배포와 지속적 통합 프로세스(CI/CD), 그리고 여기에 수반되는 소프트웨어 테스트를 이해해야 한다!

<br>

### DevOps 엔지니어 스킬

- 기초 : 리눅스 관리, 파이썬, AWS 또는 다른 클라우드 플랫폼
- 구성 : 테라폼(Terraform) 또는 앤서블(Ansible)
- 버전 관리 : 깃(Git)과 깃허브(GitHub)
- 패키징 : 도커(Docker)
- 배포 : 젠킨스(Jenkins)
- 실행 : 아마존 ECS와 쿠버네티스
- 모니터링 : ELK 스택

<br>

<br>

### DevOps 개발자 로드맵 - 2020

![img](https://media.vlpt.us/images/exploit017/post/53caf20f-feae-47aa-9bcf-f4fb2245b459/image.png)
