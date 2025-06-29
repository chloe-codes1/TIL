# MAC Address

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

### 1. MAC Address

- MAC 주소는 Media Access Control의 약자로 **2계층 (Data Link Layer)**에서 통신을 위해 NIC에 할당된 **고유 식별자**이다
- MAC 주소는 `Ethernet`과 `Wifi`를 포함한 대부분의 **IEEE 802 network 기술**에서 **2계층 주소**로 싸용된다
- Network에 접속하는 모든 장비는 `MAC 주소`라는 **물리적인 주소**가 있어야 하고, 이 주소를 이용해 서로 **통신**하게 된다

<br>

<br>

### 2. MAC 주소 체계

- MAC 주소는 **변경할 수 없도록** hardware에 고정되어 출하되므로 network 구성 요소마다 다른 주소를 가지고 있다
  - 한 network 장비 제조업체에 하나 이상의 **주소 pool**을 갖고 있으며, 그 pool 안에서 각각의 제조업체가 장비가 **출하**될 때 자체적으로 MAC 주소를 **할당**한다
    - 이렇게 network 장비 제조업체에 주소 pool을 할당하는 것을 **제조사 코드 (Vendor Code)**라고 부르며, 이 주소는 국제기구인 **IEEE**가 **관리**한다
- MAC 주소는 **48비트의 16진수 12자리**로 표현된다
  - 48비트의 MAC 주소는 다시 앞의 24비트와 뒤의 24비트로 나뉘어 구분한다
    - 앞의 24비트가 앞에서 언급한 **제조사 코드 (Vendor Code)**이며 **OUI (Organizational Unique Identifier)** 라고 부른다
    - 뒤의 24비트는 **UAA (Universally Administered Address)** 라고 부르며 각 제조사에서 **자체적으로 할당**하여 network에서 각 장비를 구분할 수 있게 해준다
- NIC나 장비를 생산할 때 **hardware 적으로 정해져 나오므로** MAC 주소를 `BIA (Burned-In Address)`라고도 부른다

<br>

#### 2-1. 유일하지 않은 MAC 주소

- 흔히 MAC 주소는 유일한 값이라고 생각하지만 **유일하지 않을 수 있다**
  - Network 제조 업체는 자신의 제조업체 code 내에서 뒤의 `UAA` 값을 할당하는데 **실수**나 **의도적**으로 MAC 주소가 **중복**될 수도 있다
- MAC 주소는 **동일 network에서만 중복되지 않으면** 동작하는 데 문제가 없다
  - Network 통신을 할 때 network가 달라 `router`의 도움을 받아야 할 경우, `router`에서 **다른 network로 넘겨줄 때** 출발지와 도착지의 MAC 주소가 **변경**되므로 network를 넘어가면 기존 출발지와 도착지 MAC 주소를 유지하지 않는다

<br>

#### 2-2. MAC 주소 변경

- MAC 주소는 **BIA (Burned-In Address)** 상태로 NIC에 할당되어 있다
- 일반적으로 **ROM (Read Only Memory)** 형태로 고정되어 출하되므로 NIC에 고정된 MAC 주소를 **변경하기는 어렵다**
- 하지만 MAC 주소도 memory에 적재되어 구동되므로 여러 방법을 이용해 변경된 MAC 주소로 NIC를 동작시킬 수 있다
  - ex)
    - windows의 경우 **Driver 상세 정보**에서 MAC 주소 변경을 제공하면 쉽게 변경이 가능하다
    - linux는 **GNU MacChanger**나 각 destro의 **network 설정 파일**에 **MAC 주소를 입력** 하면 주소 변경이 가능하다

<br>

<br>

### 3. MAC 주소 동작

- NIC는 자신의 MAC 주소를 가지고 있고, 전기 신호가 들어오면 **2계층 (Data Link Layer)**에서 **data 형태 (packet)**f로 변환하여 내용을 구분한 후 **도착지 MAC 주소**를 확인한다
  - 만약 도착지 MAC 주소가 자신이 갖고 있는 MAC 주소와 다르면 그 `packet`을 **폐기**한다
  - `packet`의 목적지 주소가 자기 자신이거나 `broadcast`, `multicast`와  **같은 그룹 주소**라면 처리해야 할 주소로 인지해 packet 정보를 **상위 계층**으로 넘겨준다

<br>

#### 3-1. 무차별 모드 (Promiscuous Mode)

- 기본적으로 NIC 동작 방식은 packet이 자신의 MAC 주소와 일치하지 안흔 도착지 주소를 가졌을 경우, 자체적으로 **폐기**된다
  - network 상태를 monitor하거나 debug, 분석 용도로 network 전체 packet을 수집해 분석해야 할 경우, NIC가 정상적으로 동작하면 다른 목적지를 가진 packet을 분석할 수 없다
- 다른 목적지를 가진 packet을 **분석**하거나 **수집**해야 할 경우, **무차별 모드**로 NIC를 구성한다
  - 무차별 모드는 **자신의 MAC 주소와 상관 없는 packet**이 들어와도 이를 분석할 수 있도록 **memory에 올려 처리**할 수 잇게 한다
- 무차별 모드를 사용하는 대표적인 application은 **network packet 분석 application**인 `Wireshark`가 있다

<br>

#### 3-2. MAC 주소를 여러 개 갖는 경우

- MAC 주소는 **단말에 종속되지 않고 NIC에 종속**된다
  - 단말은 NIC를 여러개 가질 수 있으므로 MAC 주소도 여러개 가질 수 있다
- `Multi-layer switch`, `router`와 같은 복잡한 network 장비는 NIC가 여러 개이고, MAC 주소도 여러 개가 할당된다
