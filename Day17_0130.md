# Day 17 - Algorithm (1/30)

> 박영준 강사님

- Python 수업 내용보다 깊게 공부해라
- Web쪽으로 가려면 Java를 추가로 공부해라
- IT 분야에 특화해서 커리어를 이어나가고 싶으면 Computer Science curriculum 보고 공부해라
- 네트워크 기초 / 자료구조 / 운영체제 



> Algorithm 월말평가 / 과목평가

- 전부 문제풀이 (computational thinking만 주관식)





## APS Python 기본



### 1. 배열 1 (Array 1)



> Algorithm

​	: 어떤 문제를 해결하기 위한 절차나 방법



> 무엇이 좋은 알고리즘인가?

1. 정확성
2. 작업량
3. 메모리 사용량
4. 단순성
5. 최적성



> 알고리즘의 성능은 무엇으로 측정하는가?

: 시간 복잡도 (Time Complexity)

​    -> 입력 대비 연산 횟수





### 배열 

: 일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조

   -> list == array

<br/>



#### 1차원 배열

```python
Arr = list()
Arr = []

# 이 상태에서는 배열을 가리킬 주소공간만 확보하고, 실질적으로 배열을 가리키고 있지 않음
```

<br/>



#### 디버깅하기

: IDE (= Integrated Development Environment) Tool을 사용하여 디버깅



> Break Point 설정하기

![image-20200130112815794](images/image-20200130112815794.png)



> Debugger 실행 해보기

![image-20200130113042317](images/image-20200130113042317.png)				



> 한 줄씩 실행시키기 1 - step over

![image-20200130113815266](images/image-20200130113815266.png)



> 한 줄씩 실행시키기 2 - step into

​	: 사용자 정의 함수 내부로 들어간다는 차이점이 있음

![image-20200130113919303](images/image-20200130113919303.png)



<br/>



#### 완전 검색 (Exhaustive Search = Bruce-force = generate-and-test)

: 우리가 생각 할 수 있는 모든 경우의 수를 확인하는 기법 (접근 방법)

- 모든 경우의 수를 고려하므로 수행 속도 느리지만, 답을 찾을 확률 높음
- A형은 완전 검색으로 가능 ㅎ_ㅎ



<br/>



### 순열 (Permutation)

> 서로 다른것들 중 몇 개를 뽑아서 한 줄로 나열하는 것





#### 탐욕(Greedy) 알고리즘

: 여러 경우 중 하나를 결정해야 할 때 그 순간에 최적이라고 생각되는 것을 선택해 나가는 접근 방식



##### ex) 거스름돈 줄이기 

> "어떻게 하면 손님에게 거스름돈으로 주는 지폐와 동전의 개수를 최소한으로 할 수 있을까? 

​	 -> Greedy algorithm을 무작정 적용하면 안된다는 것을 보여주는 예 





####  탐욕 알고리즘 풀이

> 1의 자리 날리기

```python
data[num % 10] += 1
```



<br/>



### 정렬

> 2개 이상의 자료를 특정 기준에 의해 오름차순 (ascending) or 내림차순 (descending) 으로 재배열 하는 것





#### 버블 정렬 (Bubble Sort)

> 인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식



```python
numbers = [55,7,78,12,42]

for i in range(len(numbers)-1,0,-1 ): #범위의 끝 위치 지정하는 for 문
    for j in range (0,i):
        if numbers[j] > numbers[j+1]:
            numbers[j], numbers[j+1] = numbers[j+1] , numbers[j]

    print(numbers)

print('Bubble Sorted => ', numbers)
```



<br/>



#### 카운팅 정렬 (Counting Sort)

> 항목의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세서 선형 시간에 정렬하는 효율적인 알고리즘



