# STP

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

- IT 환경에서는 `SPoF (Single Point of Failure: 단일 장애점)` 로 인한 장애를 피하기 위해 다양한 노력을 한다
  - `SPoF`는 **하나**의 시스템이나 구성 요소에서 **고장이 발생**했을 때 **전체 시스템** 의 작동이 멈추는 요소를 말한다
  - Network에서도 하나의 장비 고장으로 전체 network가 마비되는 것을 막기 위해 `이중화`, `다중화`된 network를 디자인하고 구성한다
- Network를 switch 하나로 구성했을 때 그 **switch에 장애가 발생**하면 **전체 network에 장애가 발생**한다
  - 이런 `SPoF`를 피하기 위해 **switch 두 대**로 network를 디자인하지만, 
    - 두 대 이상의 switch로 디자인하면 **packet이 network를 따라 계속 전송**되므로 network를 **마비**시킬 수 있다
      - 이런 상황을 `Network Loop` 라고 한다
  - `Loop`를 예방하려면 별도의 **mechanism**이 필요하다

<br>

<br>

## 1. What is a Network Loop?

- `Loop`는 말 그대로 **network에 연결된 모양**이 고리처럼 **되돌아오는 형태**로 구성된 상황을 말한다
  - Loop 상황이 발생했을 때 network가 마비되고 통신이 안 되는 상황이 발생한다
- `다양한 Loop 구조`
  1. 두 장비 간의 **이중화 연결**
  2. 장비 간의 연결이 **단일 고리** 형태로 연결
  3. 장비 간의 연결이 **중복 고리** 형태로 연결

<br>

### 1-1. Broadcast Storm

- Loop 구조로 network가 연결된 상태에서 단말에서 **Broadcast를 발생**시키면 switch는 해당 packet이 유입된 port를 제외한 모든 port로 **flooding**한다
  - **Flooding**된 packet은 **다른 switch**로도 보내지고, 이 packet을 받은 switch는 packet이 유입된 port를 제외한 모든 port로 다시 **flooding**한다
    - `Loop` 구조 상태에서는 **이 packet이 계속 돌아가는데** 이것을 `Broadcast Storm`이라고 한다
- `3계층 header`에서는 **TTL(Time to Live)**라는 packet 수명을 갖고 있지만, **switch** 가 확인하는 `2계층 header` 에는 3계층의 TTL과 같은 lifetime mechanism이 없어 loop가 발생하면 packet이 죽지 않고 계속 살아남아 packet 하나가 전체 network 대역폭을 차지할 수 있다
  - 이런 `broadcast storm` 은 network의 **전체 대역폭을 차지**하고 network에 연결된 모든 단말이 broadcast를 처리하기 위해 **system resource를 사용**하면서 switch와 network에 연결된 단말 간 통신이 거의 불가능한 상태가 된다
- Broadcast storm 상황이 발생하면
  1. Network에 **접속된 단말의 속도가 느려진다**
     - 많은 Broadcast를 처리해야 하므로 CPU 사용률이 높아진다
  2. Network **접속 속도가 느려진다**
     - 거의 통신 불가능 상태가 된다
  3. Network에 설치된 switch에 모든 LED들이 동시에 빠른 속도로 깜빡인다
- `Netowrk Loop`가 만들어진 상황에서는 cable을 제거하기 전까지 network가 마비된 것 같은 상태가 지속된다

<br>

### 1-2. Switch MAC Running 중복 문제

- Loop 구조 상태에서는 `broadcast` 뿐만 아니라 `unicast`도 문제를 일으킨다
  - 같은 packet이 loop를 돌아 도착지 쪽에서 중복 수신되는 혼란을 일으키기도 하지만, **중간에 있는 switch**에서도 `MAC Running 문제`가 발생한다
    - Switch는 **출발지 MAC 주소를 학습**하는데 **직접 전달되는 packet**과 **switch를 돌아 들어간 packet** 간의 port가 달라 MAC 주소를 정상적으로 학습할 수 없다
    - Switch MAC Address Table에서는 **하나의 MAC 주소**에 대해 **하나의 port만 학습**할 수 있으므로 **동일한 MAC 주소가 여러 port에서 학습**되면 MAC table이 **반복 갱신**되어 정상적으로 동작하지 않는다
      - 이 현상을 `MAC Address Flapping`이라고 부른다
- `MAC Address Flapping` 현상을 방지하기 위해 switch 설정에 따라 경고 메시지를 관리자에게 알려주거나 수시로 일어나는 flapping 현상을 학습하지 않도록 자동으로 조치한다

<br>

- Network에 Loop가 발생할 경우 앞의 문제들 때문에 network가 정상적으로 동작하지 않으므로 loop가 생기지 않도록 미리 network에 조치를 해야한다
  - Loop 구성 port 중 하나의 port만 사용하지 못하도록 **shutdown** 되어 있어도 loop를 예방할 수 있다
    - but, network의 `SPoF`를 예방하기 위해 switch를 두 개 이상 디자인했는데 다시 수동으로 loop를 찾아 강제로 사용하지 못하게 하는 방법은 바람직하지 않다
      - 먼저 network에서 복잡한 cable 연결을 이용해 loop를 찾아내는 것이 힘들다
      - 찾아내 강제로 port를 사용하지 못하게 하더라도 network에 장애가 발생하면 해당 port를 수동으로 다시 사용하도록 해야한다
    - 사용자가 이렇게 적극적으로 개입하는 방법으로는 network 장애에 적절히 대응할 수 없다
      - 이런 이유로 **loop를 자동 감지**해 **port를 차단**하고 장애 때문에 우회로가 없을 때 **차단된 port를 switch로 다시 풀어주는** `Spanning Tree Protocol`이 개발되었다

