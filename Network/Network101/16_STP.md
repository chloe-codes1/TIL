# STP

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

- IT 환경에서는 `SPoF (Single Point of Failure: 단일 장애점)`로 인한 장애를 피하기 위해 다양한 노력을 한다
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
- `3계층 header`에서는 **TTL(Time to Live)**라는 packet 수명을 갖고 있지만, **switch** 가 확인하는 `2계층 header` 에는 3계층의 TTL과 같은 **lifetime mechanism**이 없어서 loop가 발생하면 packet이 죽지 않고 계속 살아남아서 packet 하나가 전체 network 대역폭을 차지할 수 있다
  - 이런 `broadcast storm` 은 network의 **전체 대역폭을 차지**하고 network에 연결된 모든 단말이 broadcast를 처리하기 위해 **system resource를 사용**하면서 switch와 network에 연결된 단말 간 통신이 거의 불가능한 상태가 된다
- `Broadcast storm` 상황이 발생하면
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
    - but, network의 `SPoF`를 예방하기 위해 switch를 두 개 이상 디자인 했는데 다시 수동으로 loop를 찾아 강제로 사용하지 못하게 하는 방법은 바람직하지 않다
      - 먼저 network에서 복잡한 cable 연결을 이용해 loop를 찾아내는 것이 힘들다
      - 찾아내 강제로 port를 사용하지 못하게 하더라도 network에 장애가 발생하면 해당 port를 수동으로 다시 사용하도록 해야한다
    - 사용자가 이렇게 적극적으로 개입하는 방법으로는 network 장애에 적절히 대응할 수 없다
      - 이런 이유로 **loop를 자동 감지**해 **port를 차단**하고 장애 때문에 우회로가 없을 때 **차단된 port를 switch로 다시 풀어주는** `Spanning Tree Protocol`이 개발되었다

<br><br>

## 2. What is STP?

- `STP (Spanning Tree Protocol)`은 **loop를 확인**하고 적절히 **port를 사용하지 못하게** 만들어 **loop를 예방**하는 mechanism이다
  - 용어 그대로 잘 뻗은 나무처럼 **뿌리부터 가지까지 loop가 생기지 않도록 유지** 하는 것이 Spanning Tree Protocol의 목적이다
- STP를 이용해 loop를 예방하려면 **전체 switch**가 어떻게 연결되는지 알아야 한다
  - 전체적인 switch 연결 상황을 파악하라면 **switch 간에 정보를 전달**하는 방법이 필요하다
    - 이를 위해 switch는 `BPDU (Bridge Protocol Data Unit)` 라는 protocol을 통해 switch 간에 정보를 전달하고 이렇게 수집된 정보를 이용해 **전체 network tree**를 만들어 **loop 구간 확인**한다
      - `BPDU`에는 **switch가 갖고 있는 ID**와 같은 고유값이 들어가고 이런 정보들이 **switch 간에 교환**되면서 **loop 파악**이 가능해진다
      - 이렇게 확인된 loop 지점을 **data traffic이 통과하지 못하도록 차단**해 **loop를 예방**한다

<br>

### 2-1. Switch Port의 상태 및 변경 과정

- Spanning Tree Protocol이 동작중인 switch에서는 loop를 막기 위해
  - switch port에 신규 switch가 연결되면 바로 **traffic이 흐르지 않도록 차단**한다
  - 그리고 해당 port로 **traffic이 흘러도 되는지 확인**하기 위해
    - `BPDU` 를 기다려 학습하고,
    - 구조를 파악한 후,
    - Traffic을 흘리거나 loop 구조인 경우 차단 상태를 유지한다

<br>

#### 차단 상태에서 Traffic이 흐를 때까지 switch port의 status

- `Blocking`
  - Packet data를 차단한 상태로 상대방이 보내는 **BPDU (Bridge Protocol Data Unit)**를 기다린다
  - 총 20초인 **Max Age** 기간 동안 상대방 switch에서 BPDU를 받지 못했거나, 후순위 BPDU를 받았을 때 port는 **listening status**로 변경된다
  - BPDU의 기본 교환 주기는 **2초**이고, 10번의 BPDU를 기다린다
- `Listening`
  - 해당 portr가 **전송 상태로 변경** 되는 것을 **결정**하고 **준비**하는 단계이다
    - 이 상태부터는 자신의 BPDU 정보를 상대방에게 전송하기 시작한다
  - 총 **15초** 동안 대기한다
- `Learning`
  - 이미 **해당 port를 forwarding 하기로 결정**하고 실제로 packet forwarding이 일어날 때 switch가 곧바로 동작하도록 **MAC Addess를 learning하는 단계**이다
  - 총 **15초** 동안 대기한다
- `Forwarding`
  - packet을 forwarding 하는 단계이다
    - 이 단계에서 정상적인 통신이 가능하다!

<br>

### 2-2. STP 동작 방식

- STP는 loop를 없애기 위해 **나무가 뿌리에서 가지로 뻗어나가는 것**처럼 topology를 구성한다
  - Network 상에서 뿌리가 되는 **가장 높은 switch**를 선출하고, 그 switch를 통해 모든 BDPU가 교환되도록 하는데 이 switch를 `Root Switch` 라고 한다
    - 모든 switch는 처음에 자신을 root switch로 인식해 동작한다
      - BPDU를 통해 2초마다 자신이 root switch임을 광고하는데, 새로운 switch가 들어오면 서로 교환된 BPDU에 들어 있는 **bridge ID값을 비교**한다
      - **Bridge ID값이 더 적은 switch**를 root switch로 선정하고, 선정된 root switch가 BPDU를 다른 siwwtch 쪽으로 보낸다

<br>

#### Loop를 예방하기 위한 STP의 동작 방식

1. 하나의 `Root Switch` 선정

   - 전체 network에서 하나의 root switch를 선정한다
   - 자기 자신을 전체 network의 대표 switch로 적은 `BPDU`를 옆 switch로 전달한다

2. Root가 아닌 switch 중 `Root Port` 선정

   - `Root Switch (Bridge)` 로 가는 **경로가 가장 짧은 port**를 `Root Port` 라고 한다
   - `Root Port`는 `Root Bridge`에서 보낸 BPDU를 받는 port이다

3. 하나의 **segment**에 하나의 `지정 (designated) Port` 선정

   - Switch와 switch가 연결되는 port는 하나의 **지정 포트 (Designated Port)**를 선정한다

   - Switch 간의 연결에서

     1. 이미 root port로 선정된 경우, 그 반대쪽이 designated port로 선정되어 양쪽 모두 **forwarding status** 가 된다

     2. 아무도 root port가 아닐 경우, 한쪽은 **designated port**로 선정디고 다른 한쪽은 **대체 포트 (Alternate, Non-designated)**가 되어 `blocking status`가 된다

   - Designated Port는 **BPDU가 전달되는 port**이다

<br>

#### STP 사용시 대안 - Port Fast

- Port에 새로운 cable이 연결되면 곧바로 **forwarding status** 로 변하는 것이 아니라 상대방이 switch일 수도 있다고 가정하고 **BPDU가 들어오는지 monitoring** 한다
  - but, 이러한 mechanism은 **단말이 network에 연결될 때까지 시간이 지연**되는 문제 때문에 switch가 아닌 일반 PC나 server가 연결되는 port라면 이런 mechanism을 없애거나 좀 더 빠른 시간 안에 **forwarding status**로 변경되어야 한다
    - 이런 경우 해당 port를 `Port Fast` 로 설정하면 BPDU **waiting**, **learning** 과정 없이 **곧바로 forwarding status로 port를 사용**할 수 있다
    - `Port Fast`를 설정한 port에 switch가 접속되면 loop가 생길 수 있어 별도로 해당 port에 BPDU가 들어오자마자 port를 차단하는 **BPDU Guard** 와 같은 기술이 함께 사용되어야 한다

<br>

<br>

### 2-3. 향상된 STP - RSTP, MST

- Spanning Tree Protocol은 **loop를 예방**하기 위해 같은 network에 속한 모든 switch까지 BDPU가 전달되는 시간을 고려한다
  - 그러다보니 **blocking port**가 **forwarding status**로 변경될 때까지 30 ~ 50초가 소요된다
    - 통신에 가장 많이 쓰이는 TCP 기반 application이 network가 끊겼을 때 30초를 기다리지 못하다보니, STP 기반 network에 장애가 생기면 **통신이 끊길 수 있다**
    - 또한, switch에 **여러 개의 VLAN**이 있으면 각 VLAN 별로 STP를 계산하면서 **부하가 발생**하기도 한다
- 위의 문제를 해결하기 위해 향상된 STP를 사용한다

<br>

#### 3-1. RSTP (Rapid Spanning Tree Protocol)

- Spanning Tree Protocol은 이중화된 switch 경로 중 **정상적인 경로**에 문제가 발생할 경우, **backup 경로를 활성화**하는 데 30 ~ 50초가 걸린다
  - 이렇게 backup 경로를 활성화하는 데 시간이 너무 오래 걸리는 문제를 해결하기 위해 `RSTP (Rapid Spanning Tree Protocol)` 가 개발되었다
- `RSTP`는 2 ~ 3초로 절체 시간이 짧아 일반적인 **TCP 기반 application**이 **session을 유지**할 수 있게 된다
- 기본적인 동작 방식은 STP와 같지만, BPDU meassge 형식이 다양해져 여러 가지 상태 message를 교환할 수 있다
  - STP는 일반 topology 변경과 관련된 두 가지 message (TCN: Topology Change Notification, TCA: Topology Change Acknowledgement BPDU)만 있지만
  - RSTP는 **8개 비트를 모두 활용**해 다양한 정보를 주위 switch와 주고받을 수 있다
- 기존 STP에서는 topology가 변경되면 말단 switch에서 root bridge까지 **변경 보고**를 보내고 root bridge가 그에 대한 연산을 다시 완료하고 이후에 **변경된 topology 정보**를 말단 switch까지 보내는 과정을 거쳤다
  - 추가로 이런 정보가 network에 있는 **모든 switch까지 전파**되는 **예비 시간**까지 고려해야 하므로 정보를 확장하는데 **시간이 오래 걸렸다**
- `RSTP`에서는 **topology 변경이 일어난 switch 자신**이 모든 network에 topology 변경을 **직접 전파**할 수 있다
  - Root bridge에 보고하고 전파되는 형식이 아니라 terminal switch가 topology 변화를 다른 bridge에 **직접 알려준다**
- `RSTP`는 다양한 BPDU message, 대체 port 개념, topology 변경 전달 방식의 변화로 일반 STP보다 빠른 시간 내에 **topology 변경을 감지 및 복구** 할 수 있다!
  - 실제로 `RSTP`는 불과 2 ~ 3초 안에 장애 복구가 가능하므로 장애가 발생하더라도 **application session이 끊기지 않아** 보다 **안정적으로 network를 운영**하는데 도움이 된다!

<br>

#### 3-2. MST (Multiple Spanning Tree)

- 일반 Spanning Tree Protocol을 `CST (Common Spanning Tree` 라고 부른다
  - VLAN 개수와 상관없이 **spanning tree 한 개만 동작**하게 된다
    - 이 경우, VLAN이 많더라도 spanning tree는 한 개만 동작하면 되므로 **switch 관리 부하**가 적다
      - but, CST는 loop가 생기는 topology에서 한 개의 port와 회선만 활성화되므로 **자원을 효율적으로 활용할 수 없다**
    - 또한 VLAN마다 최적의 경로가 다를 수 있는데 port 하나만 사용할 수 있다보니 **멀리 돌아 통신**해야 할 경우도 생긴다
- CST의 문제점을 해결하기 위해 `PVST (Per Vlan Spanning Tree)`가 개발되었다
  - VLAN마다 다른 spanning tree process가 동작하므로 VLAN마다 별도의 경로와 tree를 만들 수 있게 되었다
    - 그 결과 **최적의 경로를 디자인**하고 **VLAN마다 별도의 block port를 지정**해 **network load를 sahring**하도록 구성할 수 있게 되었다
      - but, spanning tree protocol 자체가 **switch에 많은 부담을 주는 protocol (2초마다 교환)**인데 PVST는 **모든 VLAN마다 별도의 spanning tree를 유지**해야하므로 더 많은 부담이 되었다

- 이런 CSV와 PVST의 단점을 보완하기 위해 `MST (Multiple Spanning Tree)`가 개발되었다
  - `MST`의 기본적인 아이디어는 **여러 개의 VLAN을 그룹으로 묶고** 그 그룹마다 **별도의 spanning tree가 동작**한다
    - 이 경우, PVST보다 훨씬 적은 spanning tree process가 돌게 되고 PVST의 장점인 **load sharing**기능도 함께 사용할 수 있다
- 일반적으로 **대체 경로**의 개수나 용도에 따라 `MST`의 **spanning tree process** 개수를 정의한다
  - MST에서는 **region 개념**이 도입되어 **여러 개의 VLAN을 하나의 region으로 묶을 수 있다**
    - region 1 == spanning tree 1
    - ex)
      - 11 ~ 50번 VLAN과 101 ~ 150번 VLAN이 있다면
        - 11 ~ 50을 하나의 region으로
        - 101 ~ 150번을 하나의 region으로 묶으면 두 개의 spanning tree로 100개의 VLAN을 관리할 수 있다

<br>

<br>

#### 스위치의 구조와 스위치에 IP 주소가 할당된 이유

- Switch는 관리용 `Control Plane`과 packet을 forwarding 하는 `Data Plane`으로 크게 나뉜다
  - **STP**나 switch 원격 관리용 telnet, SSH, web과 같은 service는 `Control Plane`에서 수행된다
- Switch는 2계층에서 동작하는 장비여서 **MAC 주소만 이해**할 수 있다
  - Switch가 동작하는데 IP는 필요 없지만, 일정 규모 이상의 network에서 운영되는 switch는 **관리 목적**으로 대부분 IP 주소가 할당된다
