# Router

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

## 1. What is Router?

- `Router`는 **layer 3**에서 동작하는 여러 network 장비의 대표격으로, 이름처럼 **경로를 지정**해주는 장비이다
- `Router`에 들어오는 packet의 **목적지 IP주소**를 확인하고, 자신이 가진 경로(`Route`) 정보를 이용해 packet을 **최적의 경로**로 forwarding한다
- `Router`는 원격지 network와 연결할 때 필수 network 장비이며, network를 구성하는 핵심 장비이다
  - 서로 다른 network 간에 통신할 때 `router`가 반드시 필요하다!

<br>

### Router vs L3 Switch

- `Switch`는 대표적인 2계층 장비이지만, router처럼 3계층에서 동작하는 `L3 Switch`라고 부르는 장비도 많이 사용되고 있다
- 기존에 Router는 software로 구현하고, switch는 hardware로 구현하는 형태로 구분하거나 다양한 기능의 router와 packet을 빨리 보내는 데 최적화 된 switch로 구분했었다
  - 최근에는, 기술 발달로 `Router`와 `L3 switch`를 구분하기는 어렵다
    - 이 문서에서 말하는 내용은 router로 설명하고 있지만, L3 switch로도 모두 동일하게 적용되는 내용이다!

<br>

<br>

