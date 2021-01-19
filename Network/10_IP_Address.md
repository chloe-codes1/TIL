# IP Address

> Reference: [책] IT 엔지니어를 위한 네트워크 입문

<br>

<br>

- OSI 7계층에서 주소를 갖는 계층은 **2계층**과 **3계층**이다
  - 2계층은 **물리 주소**인 **MAC 주소**를 사용하고,
  - 3계층은 **논리 주소**인 **IP 주소**를 사용한다
- 대부분의 Network가 `TCP/IP`로 동작하므로 IP 주소 체계를 이해하는 것이 중요하다
- IP 주소를 포함한 다른 protocol stack의 **3계층 주소**는 아래과 같은 특성을 가진다
  1. 사용자가 **변경 가능**한 **논리 주소**이다
  2. 주소에 **level**이 있다
     - **Group**을 의미하는 `network 주소`와 `host 주소`로 나뉜다

<br>

<br>

## 1. IP 주소 체계

- 우리가 흔히 사용하는 IP 주소는 **32비트**인 **IPv4** 주소이다
  - IP는 **v4**, **v6** 두 체계가 사용되며 **IPv6** 주소는 **128비트**이다
- IPv4 주소를 표기할 때는 4개의 **옥텟 (octet)**이라고 부르는 **8비트 단위**로 나뉘고, 각 octet은 **"."** 으로 구분한다
  - `IPv4 주소`: 8비트 x 4 = 32비트
- 2계층의 `MAC 주소`가 **16진수**로 표기된 것과 달리 `IP 주소`는 **10진수**로 표기하므로 **8비트 옥텟**은 **0 ~ 255**의 값을 가질 수 있다
- 2계층 주소인 `MAC 주소`가 제조업체 코드인 **OUI**와 제조업체별 일련 번호인 **UAA** 두 부분으로 나뉘는 것과 목적이 다르지만, 
  - 3계층 주소인 `IP 주소`도 **네트워크 주소**와 **호스트 주소** 두 부분으로 나뉜다
    - **네트워크 주소**
      - Host들을 모은 network를 지칭하는 주소
      - Network 주소가 동일한 network를 **Local Network**라고 한다
    - **호스트 주소**
      - 하나의 network 내에 존재하는 host를 구분히기 위한 주소
- `MAC 주소`는 24비트씩 절반으로 나뉘지만, `IP 주소`의 **네트워크 주소**와 **호스트 주소**는 이둘을 구분하는 **경계점이 고정되어 있지 않다**
  - 이것이 다른 주소 체계와 IP 주소 체계를 구분하는 가장 큰 특징이다
  - IP 주소 체계는 필요한 **호스트 IP 개수**에 따라 **네트워크의 크기를 다르게 할당**할 수 있는 `Class 개념`을 도입했다
- 네트워크 주소와 호스트주소를 나누는 **구분자**가 **고정**되어 있다면 네트워크가 가질 수 있는 `호스트 IP 주소` 숫자가 같기 때문에 **같은 크기의 네트워크**가 되지만,
  -  **구분자를 이동할 수 있어** 네트워크 크기가 달라질 수 있다
- `IP 주소`가 도입한 **class 개념**은 다른 고정된 네트워크 주소 체계에[ 베히 **주소를 절약할 수 있다**는 장점이 있다
  - 네트워크의 크기가 모두 같은 경우, 
    - 큰 네트워크를 필요로 하는 조직은 네트워크를 **여러개 확보**해야하는 어려움이 있고, **연속된 네트워크**를 할당받기 어렵다
    - 작은 네트워크를 필요로 하는 조직은 **너무 많은 IP**를 가져가므로 **IP가 낭비**된다
- A, B, C Class는 맨 앞의 옥텟의 주소만 보고 구분할 수 있다

<br>

### Classful Network

<br>

#### A Class

- 가장 큰 주소를 갖는다
- 약 1,600만개의 IP 주소를 가질 수 있다
- **첫 번째 옥텟**에 네트워크와 호스트 주소를 나누는 **구분자**가 있다
  - 이 구분자를 `서브넷 마스크`라고 한다!
- `네트워크 주소`를 표현하는 부분이 1개의 옥텟, `호스트 주소`를 나타낼 수 있는 옥텟이 3개이기 때문에 
  - **2^8 (256)**개의 네트워크와
  - 한 네트워크 당 **2^24 (16,666,216)**개의 호스트 주소를 갖는다
- A, B, C class는 맨 앞의 옥텟 주소만 보고도 구분할 수 있는데, 옥텟 주소가 `0 ~ 127` 의 볌위이면 이 주소는 A Class이다
  - 즉, 2진수로 첫 옥텟이 `0 0000000 ~ 0 1111111`인 주소가 A Class가 된다
  - `127`만 예외로 자신을 의미하는 **Loopback 주소**로 사용되므로, 실제로 A Class로 사용할 수 있는 주소는 `1.0.0.0 ~ 126.255.255.255` 까지이다

<br>

<br>

#### B Class

- 약 6만 5천개의 IP 주소를 갖는다 
- **두번째 옥텟**에 **구분자**가 있다
- `네트워크 주소 부분`이 2개의 옥텟, `호스트 주소`가 2개의 옥텟이기 때문에
  - **2^16 (65,536)**개의 네트워크와
  - 1개의 네트워크에 **2^16(65,536)**개의 호스트주소를 갖는다
- 첫 옥텟을 2진수로 표기했을 때 **첫번째 자리가 1**이고, **두번째 자리가 0**인 주소가 B class이다
  - 2진수로 첫 옥텟이 `10 000000 ~ 10 111111` 인 수이고,
  - 10진수로 표현하면 128부터 191까지인 주소가 B Class이다

<br>

<br>

#### C Class

- **세번재 옥텟**에 **구분자**가 있다
- `네트워크 주소 부분`이 3개의 옥텟, `호스트 주소`가 1개의 옥텟이기 때문에
  - **2^24 (16,777,216)**개의 네트워크와
  - 1개의 네트워크 당 **2^8 (256)**개의 호스트를 가질 수 있다
- 첫 옥탯을 2진수로 표기했을 때 2진수 8자리 중 **첫 번째, 두 번째 자리가 1**이고, **세 번째 자리가 0**인 주소가 C Classs이다
  - 첫 옥텟이 2진수로 `110 00000 ~ 110 11111` 이고,
  - 10진수로 192 부터 223까지 IP인 경우 C class이다

<br>

Class 기반의 네트워크 분할 기법은 **과거에 사용했던 개념**으로 현재는 class 기반으로 네트워크를 분할하지 않는다

보다네트워크 주소를 세밀하게 분하랗고 할당하기 위해 **필요한 네트워크의 크기**에 맞추어 **1비트  단위**로 네트워크를 **상세히 분할**하는 방법을 사용한다 

<br>

`+`

### 네트워크에서 사용 가능한 호스트 개수 파악하기

- IP 네트워크에서는 **네트워크 크기가 변경**되므로 **하나의 네트워크에서 사용 가능한** `host의 개수`와 `유효 IP 범위`를 파악하는 것이 중요하다
  - Class 단위로 네트워크가 분할되는 경우, 쉽게 인지할 수 있는 10진수 형태로 표현되어 이해하는데 큰 무리가 없지만 `Classless Network`인 경우, 유효 IP 범위 파악이 매우 중요하다
- 일반적으로 표현할 수 있는 모든 수의 개수는 **진수^자릿수**의 형태로 계산할 수 있다
  - ex) 우리가 사용하는 10진수 4자리가 나타낼 수 있는 총 수는 10^4개이다
    - 0000부터 9999까지 10,000개의 숫자를 표현할 수 있다
- IP는 2진수로 나타내므로 **2^자릿수** 형태로 표현할 수 있는 IP 숫자를 구할 수 있다
  - 한 옥텟이 2진수 8자리이므로 A Class는 2^24개, B Class는 2^16개, C Class는 2^8개의 IP를 표현할 수 있다
  - but, IP 체계에서 **맨 앞의 숫자**를 `네트워크 주소`로, **맨 뒤의 숫자**를 `브로드캐스트 주소`로 사용하므로 실제로 사용할 수 있는 IP는 **A Class** `2^24 - 2`개, **B Class** `2^16 -2` 개, **C Class** `2^8 -2`개이다

<br>

<br>

## 2. Classful and Classless Network

- IP 주소 체계를 처음 만들었을 때는 Class 개념을 도입한 것이 **확장성** 있고, 주소 낭비가 적은 쵲거의 조건을 만들 수 있었던 좋은 선택이었따
  - `Classful Network` 에서는 **네트워크 주소**와 **호스트 주소**를 구분짓는 구분자 (`Subnet mask`)가 필요 없었다
  - 맨 앞자리 숫자만 보면 자연스럽게 이 주소가 어느 class에 속해 있는지 구분할 수 있고, 주소 구분자를 적용할 수 있었다

<br>

### Classless Network

- 인터넷이 상용화되면서 인터넷에 연결되는 host 숫자가 폭발적으로 증가했다
  - 기존 `Classful` 기반의 주소 체계는 **확장성**과 **효율성**을 모두 잡는 좋은 주소 체계였지만, 기하급수적으로 늘어나는 IP 주소 요구를 감당하기에는 너무 부족했다
    - 또한 네트워크 주소를 **계층화**하고 **분할**하기 위해 **낭비되는 IP**가 매우 많았다
- IP 주소 부족과 낭비 문제를 해결하기 위해 만든 3가지 보존, 전환 전략은 아래와 같다  
  1. 단기 대책 - `Classless`, `CIDR (Classless Inter-Domain Routing)` 기반의 주소 체계
  2. 중기 대책 - `NAT` 와 `사설 IP 주소`
  3. 장기 대책 - 차세대 IP인 `IPv6`
- `IPv4`의 가장 큰 문제는 주소 자체의 부족도 있지만 상위 Class (A Class)를 할당받은 조직에서 이 주소들을 제대로 사용하지 못하면서 낭비되는 것이었다
  - `Classful`에서는 한 개의 class network가 한 조직에 할당되면 아무리 비어 있는 주소라도 **IP를 분할**해 **다른 기관이 사용하도록 할 수 없다**
    - 이 문제를 해결하기 위해 class 개념 자체를 버리는데 이를 `Classless network`라고 부른다
      - 현재 우리가 사용하는 주소 체계는 Class 개념을 적용하지 않은 **Classless 기반의 주소 체계**이다
- `Classless Network`에서는 별도로 network와 host 주소를 나누는 구분자를 사용해야 하는데, 이 구분자를 **Subnet Mask** 라고 부른다
  - `Subnet Mask`는 **IP 주소**와 **Network 주소**를 구분할 때 사용하는데 2진수 숫자 1은 **Network 주소**, 0은 **Host 주소**로 표시한다
    - 보통 10진수를 이용하여 `255.0.0.0`, `255.255.0.0`, `255.255.255.0`과 같이 표현한다
    - 2진수 11111111을 10진수로 표현하면 255가 되어 255는 **Network 주소**부분, 0은 **Host 주소 부분**으로 구분된다
      - ex) `103.9.32.146` 주소에 `255.255.255.0` subnet mask를 사용하는 IP는
        - Network 주소가 103.9.32.0 이고,
        - Host 주소는 0.0.146이 된다
  - Classless 기반의 IT Network에서는 Netowork를 표현하는 데 반드시 subnet mask가 필요하고 server나 PC에 IP 주소를 부여할 때도 사용되어야 한다

<br>

### Subnet Mask 표현 방법

- Subnet mask를 표현하는 방법은 **비트 단위로 표현**하는 방법과 **10진수로 표현**하는 방법을 사용한다
  - **비트 단위로 표현**하는 방법은 Subnet Mask에서 1 부분이 연속된 자릿수를 표현해주는 것이다
    - A Class를 subnet mask로 나타내면 첫 Octet이 1, 나머지 Octet이 0이므로 `/8`로 표현한다
    - B Class는 `/16`,
    - C Class는 `/24` 로 표기한다
  - **10진수로 표현**할 때,
    - A Class는 `255.0.0.0`,
    - B Class는 `255.255.0.0` ,
    - C Class는 `255.255.255.0` 으로 쓴다

<br>

<br>

## 3. Subnetting

- 원래 부여된 Class의 기준을 무시하고 새로운 **Network-Host 기준**을 사용자가 정해서 classful 단위의 network보다 더 쪼개 사용하는 것을 **Subnetting**이라고 한다
  - 부여된 주소를 다시 잘라 사용해 **subnetting**이라고 부르는데, classless network의 가장 큰 특징이다
  - Otcet 단위로 구분되는 subnetting은 이해와 운영이 쉽지만, 실제로는 octet 단위보다 더 잘게 network를 쪼개 2진수의 1bit 단위로 network를 분할한다
- 실무에서 subnetting에 대해 고민해야 하는 경우는 두 가지이며, 상황에 따라 고려해야 할 요소와 범위가 달라진다
  1. **네트워크 설계자**가 네트워크를 어떻게 효율적으로 분할할 것인지 계획하는 경우
     - 네트워크 설계 시 네트워크 내에 필요한 단말을 고려한 네트워크 범위 설계
  2. 이미 분할된 네트워크에서 **네트워크 사용자**가 자신의 네트워크와 원격지 네트워크를 구분해야 하는 경우
     - 네트워크에서 사용할 수 있는 IP 범위 파악
     - 기본 Gateway와 Subnet Mask 설정이 제대로 되어있는지 확인

<br>

### 3-1. 네트워크 사용자의 Subnetting

- 네트워크 사용자는 이미 설계되어 있는 네트워크에서 **사용할 수 있는 IP 주소 범위**를 파약해야 한다
  - 주어진 네트워크 범위 밖의 IP를 할당하거나, Subnet mask를 잘못 입력하면
    - Local Network의 특정 범위에 속해있는 단말과 통신에 문제가 생기거나,
    - 외부 Network 전체에 통신하지 못하는 상황이 발생한다
- 대부분의 subnetting은 **bit 단위**로 분할되어 있고, IP 주소 체계는 컴퓨터가 처리하므로 2진수로 되어 있다
  - 2진수에 익숙하거나 subnetting이 octet 단위로 되어 있는 경우, 내가 속한 Network의 크기와 IP 범위를 알아내기 쉽겠지만, 1비트 단위로 subnetting 된 경우 유효한 Network 범위를 알아내기 어렵다
    - 일반적으로 **자신이 속한 Network의 유효 범위**를 파악하는 방법은 아래와 같다
      1. 내 IP를 2진수로 표현한다
      2. Subnet Mask를 2진수로 표현한다
      3. 2진수 AND 연산으로 Subnetting 된 `Network 주소`를 알아낸다
      4. Host 주소 부분을 2진수 1로 모두 변경해 `Broadcast 주소`를 알아낸다
      5. 유효 IP 범위를 파악한다
         - `Subnetting 된 Network 주소 +1` 은 유효 IP 중 가장 작은 IP이다
      6.  `Broadcast 주소 - 1`은 유효 IP 중 가장 큰 IP이다
      7. 2진수로 연산되어 있는 결과값을 10진수로 변환한다
    - 항상 위의 방법으로 Local Netowork의 범위를 알아내기는 어렵다

<br>

#### 간단한  Subnetting 방법

- ex) IP 주소:  `103.9.32.146`, Subnet Mask:  `255.255.255.192`
  1. Subnet Mask를 2진수로 변환한다  
     - ex) `11111111.11111111.11111111.11000000`
  2. 현재의 Subnet이 가질 수 있는 최대 IP 개수 크기를 파악한다
     - ex) 2^6 = 64
  3. 64의 배수로 나열하여 기준이 되는 Network 주소를 파악한다.
     -  첫 Block은 0부터 시작한다 
     - 각 Network의 마지막 주소가 Broadcast 주소가 된다
       - 이 주소는 다음 블록 Network 주소의 -1 수이다
     - ex) `0 ~ 63` / `64 ~ 127` / `128 ~ 191` / `192 ~255`
  4. `103.9.32.146`에서 Host 주소 146이 속한 Network를 선택한다
     - ex) `128 ~ 191`
  5. 필요한 주소를 정리한다
     - **Network 주소**: `103.9.32.128` (첫 번째 숫자)
     - **Broadcast 주소**: `103.9.32.191` (마지막 숫자)
     - **유효 IP 범위**: `103.9.32.129` ~ `103.9.32.190` (Network 주소와 Braodcast 주소 사이)

<br>

위 방법의 핵심은 Subnet Mask를 중심으로 Network 크기를 파악해  Subnetting 된 Network의 크기를 알아내는 것이다!

<br>

<br>

### 3-2. 네트워크 설계자의 Subnetting

- Network를 새로 구축하는 경우, Network 사용자와 반대로 설계자는 Subnet Mask가 지정되어 주어지는 것이 아니라 **Network의 크기**를 고민해 **Subnet Mask를 결정**하고 설계에 반영해야 한다
  - Network 설계자가 IP를 설계할 때 고민해야 할 부분은 아래와 같다
    1. Subnet 된 하나의 Network에 IP를 몇 개나 할당해야 하는가?
    2. Subnet 된 Network가 몇개나 필요한가?

<br>

ex) 12곳의 지사가 있는 회사의 Network 설계하기

1. Subnet 된 하나의 Network에 12개의 IP를 할당해야 한다
2. Network는 2진수의 배수로 커지므로 4, 8, 16, 32, 64, 128, 256 단위로 Network를 할당할 수 있다
   - 12개 IP를 수용할 수 있는 가장 작은 Network는 16개이므로 16개짜리 Network를 할당한다
     - 단, 16개짜리 Network는 `Network 주소`와 `Broadcast 주소`로 사용할 2개의 IP를 제외해야 하므로 실제로 사용할 수 있는 IP는 14개다
3. 16개짜리 Network 12개를 확보한다
   - 16의 배수를 0부터 나열해 Network 주소를 확인한다
4. 총 16개의 Network 중 12개 Network를 각 지사에 할당한다

<br>

- Network를 설계할 때 가능하면 사설 IP 대역을 사용해 **충분한 IP 대역을 사용**하는 것이 좋다
- 공인 IP를 사용해 여유 없이 Network를 할당하면 **크기가 다른 Network**가 많아진다
  - 그러면 Network 관리자 입장에서도 관리가 힘들어지고, 일반 사용자도 IP를 쉽게 구분하거나 알아볼 수 없게된다
- 최대한 **같은 크기**의 Network를 할당하고, 10진수로 표현해도 쉽게 이해할 수 있는 **C class 단위**인 **24비트로 쪼개 할당**하는 것이 바람직하다

<br>

<br>

## 4. Publilc IP and Private IP

- 인터넷에 접속하려면 IP 주소가 있어야 하고 이 IP는 전 세계에서 유일해야 하는 식별자이다
  - 이런 IP 주소를 **Public IP** 주소라고 한다
- 인터넷에 연결하지 않고 개인적으로 Network를 구성 한다면 공인 IP 주소를 할당받지 않고도 Network를 구축할 수 있다
  - 이 때 사용하는 IP 주소를 **Private IP** 주소 라고 한다
- 인터넷에 접속하려면 `통신 사업자`로부터 IP 주소를 할당받거나 `IP 할당 기관 (한국의 경우 KISA)`에서 **인터넷 독립기관 주소 (Autonomous System Number, ASN)**를 할당받은 후 독립 IP를 할당받아야 하므로 절차가 복잡하다
- 인터넷에 접속하지 않거나 **NAT (Network Address Translation)** 기술을 사용할 경우 (공유기나 회사 방화벽을 사용하는 경우)에는 **private IP**를 사용할 수 있다
  - 이 주소들은 이터넷 표준 문서인 **RFC**에 명시되어 있다
  - **Private IP**를 사용하면 인터넷에 직접 접속하지 못하지만, IP를 변환해주는 **NAT 장비**에서 **public IP**로 변경한 후에는 인터넷 접속이 가능하다 
- 회사 내부에서 Private Network를 구축할 때 NAT를 이용하여 인터넷에 연결하더라도 **다른 사용자에게 할당된 IP**를 private IP로 사용하면 안 된다
  - 다른 기관에서 사용하는 Public IP를 회사 내부에서 사용할 경우,  해당 IP로의 접근이 불가능하다
- `Private IP`는 **A Class 1개**, **B Class 16개**, **C Class 256개**를 사용할 수 있다
  - 규모가 큰 Enterprise network에서는 대부분 A Class 크기인 `10.0.0./8` network를 사용하고,
  - 규모가 작은 network를 위해서는 C Class `198.168. x.0/24`를 사용한다
    - 공유기에서 가장 많이 사용되는 기본 IP가 `192.168.0.1`인 이유이다 