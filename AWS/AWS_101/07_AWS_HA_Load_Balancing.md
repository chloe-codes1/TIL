# AWS HA Load Balancing

<br>

#### Contents

- Amazon Elastic Load Balancing
- Amazon Auto Scaling
- ELB 및 Auto Scaling 구축하기

<br>

#### Useful Informations

1. Amazon Elastic Load Balancing은 확장성, 성능 및 보안을 보장하여 application의 내결함성을 확보할 수 있다

   - ELB는 단일 가용 영역 또는 여러 가용 영역에서 다양한 application의 부하를 처리할 수 있다

2. ELB는 application의 요구 사항에 따라 적절한 Load Balancer를 선택할 수 있다

   - `Application Load Balancer`

     :  유연한 application 관리가 필요한 경우

   - `Network Load Balancer`

     : Application에 탁월한 성능 및 고정 IP가 필요한 경우

   - `Classic Load Balancer`

     : 기존 application이 EC2-Classic Network 내에 구축되어 있는 경우

<br>

<br>

## Amazon Elastic Load Balancing

> 확장성, 성능 및 보안을  보장하여 application의 내결함성 확보

<br>

- Elastic Load Balancing은 들어오는 application traffic을 Amazon EC2 instance, container, IP address, Lambda function과 같은 여러 대상에 자동으로 분산시킴
- ELB는 단일 가용 영역 또는 여러 가용 영역에서 다양한 application 부하를 처리할 수 있음
- ELB가 제공하는 세 가지 Load Balancer는 모두 application의 `내결함성`에 필요한 **HA (High Availability)**, **자동 확장/축소**, **강력한 보안**을 갖추고 있음

<br>

### Application 내결함성 향상

- ELB는 대상 (Amazon EC2 instance, container, IP address, Lambda function)과 여러 가용 영역에 traffic을 자동으로 분산시키는 동시에 정상 상태인 대상만 traffic을 수신하도록 함으로써 application의 내결함성을 제공함
- 단일 가용 영역의 모든 대상이 정상 상태가 아닐 경우, ELB는 다른 가용 영역에 있는 정상 상태인 대상으로 traffic을 routing 함
- 대상이 정상 상태로 복구되면 Load Balancing은 자동으로 원래 대상으로 재개됨

<br>

### Container식 application의 자동 Load Balancing

- Elastic Load Balancing의 향상된 Container 지원을 통해 동일한 Amazon EC2 instance의 여러 port에서 Load Balancing이 가능함
- 완전 관리형 container 상품을 제공하는 `Amazon EC2 Container Service (ECS)` 와의 완벽한 통합도 활용할 수 있음
- Service를 Load Balancer에 등록하기만 하면 ECS는 `Docker COntainer` 의 등록 및 등록 취소를 투명하게 관리함
- Load Balancer는 port를 자동으로 탐지하여 동적으로 스스로를 재구성함



3:35부터