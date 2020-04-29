# Algorithm Basics

<br>

### SW 문제 해결 역량이란?

: 프로그램 작성을 위한 많은 제약 조건들과 요구사항들을 이해하고 최선의 방법을 찾아내는 능력

- 프로그래머가 사용하는 언어, 라이브러리, 자료구조, 알고리즘에 대한 지식을 적재적소에 연결하여 큰 그림을 만드는 능력

<br>

### 문제 해결 과정 단계

1. 문제를 읽고 이해
2. 

<br>

## 알고리즘의 효율

### 1. 공간적 효율성과 시간적 효율성

- 공간적 효율성은 얼마나 많은 메모리 공간을 요하는가를 말함
- 시간적 효율성은 얼마나 많은 시간을 요하는가를 말함
- 효율성을 뒤집어 표현하면 복잡도 (`Complexity`) 가 된다
  - 복잡도가 높을수록 효율성은 저하된다

<br>

### 2. 시간적 복잡도 분석

- 하드웨어 환경에 따라 처리시간이 달라진다
- 소프트웨어 환경에 따라 처리시간이 달라진다
- 그래서, 화이러한 환경적 차이로 인해 분석이 어렵다

<br>

### 3. 복잡도의 점근적 표기

- 시간 (또는 공간) 복잡도는 입력 크기에 대한 함수로 표기하는데, 이 함수는 주로 여러갷의 항을 가지는 다항식이다

<br>

<br>

## O (Big-Oh) 표기

### 1. 정의

- T(n): 실행시간
-  T(n) <= c*f(n)이 되는 상수 c, n0가 존재할 때만 T(n) = O(f(n))이라고 한다
- 단, 상수 c와 초기값 n0는 n의 값에 독립적이다

<br>

### 2. 표기

- O-표기
  - 복잡도의 점근적 **상한**을 나타낸다
  - 복잡도가 T(n) = 2n^2 - 7n +4 이라면, T(n)의 O 표기는 O(n^2) 이다
  - T(n)의 단순화된 표현은 n^2이다
  - "최악의 경우에도 이만큼은 나온다"
- Big-Omega 표기
  - 복잡도의 점근적 **하한**을 의미한다
  - "최소한 이만큼은 걸린다"

<br>

*Omega < Theta < Big O*

<br>

<br>

### 자주 사용하는 O-표기

- `O(1)`
  - 상수 시간 (Constant time)
- `O(logn)`
  - 로그(대수) 시간 (Logarithmic time)
- `O(n)`
  - 선형 시간 (LInear time)
- `O(nlogn)`
  - 로그 선형 시간 (Log-linear time)
- `O(n^2)`
  - 제곱 시간 (Quadratic time)
- `O(n^3)`
  - 세제곱 시간 (Cubic time)
- `O(2^n)`
  - 지수 시간 (Exponential time)

<br>

<br>

## 비트 연산

<br>

### 비트 연산자

![image-20200429103824460](../images/image-20200429103824460.png)

<br>

- 정수는 2byte로, 혹은 4byte로 표기하기도 한다
- 범위를 넘어 갈 때
  - 없애버리거나
  - 보정을 해준다
- 정수는 부호 비트가 가장 앞에 들어간다

<br>

### N & 1

- 변수에 저장된 양의 정수 값의 홀수 짝수 판별
  - N%2
- % 연산으로 마지막 비트 값이 1인지 0인지 판단, 짝수 홀수 판별

<br>

### 1 << n

- 2^n의 값을 갖는다
- 원소가 n개일 경우의 모든 부분집합의 수를 의미한다
- `Power set` (모든 부분 집합)
  - 공집합과 자기 자신을 포함한 모든 부분집합
  - 각 원소가 포함되거나 포함되지 않는 2가지 경우의 수를 계싼하면 모든 부분집합의 수가 계산된다

<br>

### i & (1 << j) = (i >> j) &1

- 계산 결과는 i의 j번째 비트가 1인지 아닌지를 의미한다

<br>

### 비트 연산자 ^를 두 번 연산하면 처음 값을 반환한다

<br>

### 비트 연산 예제 1

```python
def Bbit_print(i):
    output = ''
    for j in range(7, -1, -1):
        output += "1" if i&(1<<j) else "0"
    print(output)

for i in range(-5, 6):
    print("%3d = " %i, end='')
    Bbit_print(i)
```

<br>

<br>

## 엔디안 (Endianness)

- 컴퓨터의 메모리와 같은 1차원 공간에 여러 개의 연속된 대상을 배열하는 방법을 의미하며 HW 아키텍처마다 다르다
- `주의!`
  - 속도 향상을 위해 바이트 단위와 워드 단위를 변환하여 연산 할 때 올바로 이해하지 않으면 오류를 발생 시킬 수 있다

<br>

### 빅 엔디안 (Big-endian)

- 보통 큰 단위가 앞에 나옴
- 네트워크
  - ex) internet protocol, IBM z/architecture (대형 컴퓨터 일부만..)

<br>

### 리틀 엔디안 (Little-endian)

- 작은 단위가 앞에 옴
- 대다수 데스크탑 컴퓨터
  - ex) Intel, ARM processor

<br>

### 엔디안 확인 코드

```python
# ver1)
n = 0x00111111
if n&0xff: #0xff = 11111111 이다!
    print("little endian")
else:
    print("big endian")

print('-'*20)

#ver2) python sys library 활용
import sys
if sys.byteorder == "little":
    print("Little endian platform")
else:
    print("Big endian platform")
```

<br>

### Python 에서 엔디안 변환

```python
# Python에서 Endian 변환

import struct #c의 library

num = 27
print(bin(num))
res = struct.pack('i', num)
print('default :', res)

res = struct.pack('> i', num)
print('big endian :', res)

res = struct.pack('< i', num)
print('little endian :', res)

res = struct.pack('! i', num)
print('network :', res)
print('unpack :', struct.unpack('!i',res))
```

<br>

<br>

## 진수

> 2진수, 8진수, 10진수, 16진수

<br>

### 10진수 -> 타 진수로 변환

- 원하는 타 진법의 수로 나눈 뒤 나머지를 거꾸로 읽는다

<br>

### 컴퓨터에서 음의 정수 표현 방법

- 1의 보수
  - 부호와 절대값으로 표현된 값을 부호 비트를 제외 한 나머지 비트들을 0은 1로, 1은 0으로 변환
- 2의 보수
  - 1의 보수방법으로 표현된 값의 최하위 비트에 1을 더한다

<br>









